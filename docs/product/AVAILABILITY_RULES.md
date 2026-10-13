# Availability Engine — Kurallar ve Kenar Durumları

**Versiyon:** 1.0  
**Referans:** [SPECIFICATION.md](../../SPECIFICATION.md) §4–5, [IMPLEMENTATION.md](../../IMPLEMENTATION.md) §2.1

---

## 1. Amaç

`AvailabilityService` tek otorite: bir `(court_id, starts_at)` çifti için üyenin rezervasyon açıp açamayacağını ve UI’da hangi **görsel durumun** gösterileceğini belirler.

---

## 2. Girdiler ve çıktılar

### 2.1 Fonksiyon imzası (mantıksal)

```text
evaluateSlot(
  courtId: UUID,
  slotStart: Instant,        // slot başlangıcı, Europe/Istanbul duvar saati ile hizalı
  context: {
    actorRole: Role,
    memberId?: UUID,
    purpose: 'display' | 'hold' | 'confirm' | 'admin_manual'
  }
) → SlotEvaluation
```

### 2.2 SlotEvaluation

| Alan | Tip | Açıklama |
|------|-----|----------|
| `status` | enum | Aşağıdaki §3 |
| `bookable` | boolean | Üye self-servis için true/false |
| `publicLabel` | string | UI kısa metin (TR) |
| `internalReason` | string | Log / debug |
| `blockType` | enum? | Blok kaynaklıysa |
| `pricePreview` | Money? | display+member ise (Faz 2) |

---

## 3. Durum enum (öncelik sırası)

Değerlendirme **ilk eşleşmede durur** (yüksekten düşüğe):

| Öncelik | status | bookable (member) | publicLabel örneği |
|---------|--------|-----------------|---------------------|
| 1 | `NOT_BOOKABLE` | false | Bu kort rezervasyona kapalıdır. |
| 2 | `OUTSIDE_HOURS` | false | — (grid’de sütun yok) |
| 3 | `OUTSIDE_ADVANCE_WINDOW` | false | En fazla 3 gün sonrasına rezervasyon yapabilirsiniz. |
| 4 | `PAST` | false | Geçmiş saat. |
| 5 | `FIXED_CONTRACT` | false | Fix kort — ayrılmış. |
| 6 | `BLOCKED` | false | Akademi programı / Turnuva / … |
| 7 | `BOOKED` | false | Dolu |
| 8 | `HELD_BY_OTHER` | false | Başka üye işlemde (opsiyonel gösterim) |
| 9 | `HELD_BY_SELF` | true | Seçili (checkout) |
| 10 | `AVAILABLE` | true | Müsait |

**Admin `purpose=admin_manual`:** `BLOCKED` turnuva iken super_admin override path ayrı endpoint; evaluateSlot yine BLOCKED döner, override API farklı policy.

---

## 4. Zaman grid üretimi

### 4.1 Slot başlangıçları

Günlük `date` (Istanbul) için:

```text
slots = [07:00, 08:00, …, 21:00]  // 15 slot/gün/kort
ends   = starts + 60 dakika
```

### 4.2 Yaz saati (DST)

- Tüm `starts_at` **UTC timestamptz** saklanır.
- Grid render Istanbul duvar saati ile; geçiş günlerinde 07:00–22:00 penceresi **kulüp yerel saati** ile sabit (eksik/fazla saat dilimi gününde admin manuel müdahale prosedürü: [SEASON_TRANSITION.md](../operations/SEASON_TRANSITION.md)).

### 4.3 Advance window (72 saat)

```text
maxStart = now(Istanbul) + 72 hours
slotStart <= maxStart  → inside window
```

**Strict:** slot başlangıcı tam 72:00:00 sonrası ilk saniye dahil değil (≥72h red). Dokümantasyon netliği: `slotStart > now + 72h` → red.

**Örnek:** Şimdi Pazartesi 10:00 → en geç Perşembe 10:00 başlangıçlı slot book edilebilir; Perşembe 11:00 red.

---

## 5. Haftalık 3 aktif limit

### 5.1 Tanım

```text
active(booking) =
  status IN (pending_payment, confirmed)
  AND starts_at > now
  AND NOT cancelled
```

### 5.2 Hafta sınırı

ISO hafta **değil** — SPEC: **Pazartesi 00:00 – Pazar 23:59:59** Europe/Istanbul.

```text
weekStart = date_trunc_week_monday(slotStart)
count = active bookings where member_id = M
        AND starts_at in [weekStart, weekStart + 7 days)
```

### 5.3 Hold sayılır mı?

**Hayır.** Hold rezervasyon değil; confirm anında limit kontrolü tekrarlanır.

### 5.4 Limit dolu iken hold

Hold oluşturulabilir (opsiyonel product choice). **Önerilen:** hold da red — `WEEKLY_LIMIT` — UX netliği.

---

## 6. Blok overlap algoritması

```text
block_applies(block, court, slotStart, slotEnd) =
  slotStart < block.ends_at AND slotEnd > block.starts_at
  AND (block.court_id IS NULL OR block.court_id = court.id)
  AND (block.group_code IS NULL OR block.group_code = court.group_code)
```

Çoklu blok: en yüksek öncelikli `block_type` etiketi UI’da (turnuva > bakım > akademi > kış) — config tablosu Faz 2; MVP ilk bulunan.

---

## 7. Fix kort genişletme

Aktif sözleşme:

```text
contract.weekday matches slotStart.dayOfWeek
AND contract.start_time = slotStart.localTime
AND contract.status = active
AND slotStart.date in [active_from, active_to]
AND contract.court_id = court.id
```

→ `FIXED_CONTRACT`, bookable false.

---

## 8. Hold ve booking çakışması

Geçerli hold:

```text
expires_at > now
```

Aynı court+starts_at:

- Başka member hold → `HELD_BY_OTHER` veya `BOOKED` (ürün: “İşlemde”)
- Kendi hold → checkout devam

Confirm:

```text
BEGIN TRANSACTION
  SELECT ... FOR UPDATE -- court_id + starts_at
  re-evaluate availability
  INSERT booking
  DELETE hold
COMMIT
```

---

## 9. Fitness kort

`bookable=false` → grid’de gösterim modu:

- **Üye app:** satır gizli (önerilen) veya gri “Fitness — tenis rezervasyonu yok”
- **Admin:** görünür, etiket

---

## 10. Merkez / balon / kapalı

Availability aynı; fiyat farkı PricingService’te.

---

## 11. Kenar durumları tablosu

| # | Senaryo | Beklenen |
|---|---------|----------|
| E1 | Üye pasif | Auth OK, book API 403 MEMBER_INACTIVE |
| E2 | pending_payment eski 20 dk | Cron cancel + slot açılır |
| E3 | Admin manuel confirmed | BOOKED |
| E4 | Blok 14:00–16:00, slot 15:00–16:00 | BLOCKED |
| E5 | Blok 14:00–15:00, slot 15:00–16:00 | AVAILABLE |
| E6 | İki blok overlap | BLOCKED, birincil etiket |
| E7 | Fix Salı 18:00, üye Salı 18:00 dener | FIXED_CONTRACT |
| E8 | Turnuva + super_admin override booking | BOOKED, type override |
| E9 | Hold expire anında confirm | SLOT_TAKEN |
| E10 | Sunucu saati drift | NTP zorunlu; max drift 2s |
| E11 | Rezervasyon hafta sınırında Pazar 22:00 | Hafta Pazar bitiş; sayım doğru |
| E12 | Üye 3 confirmed, biri iptal, yeni rez | İzin var |
| E13 | reception manuel, limit dolu | Policy: red (super_admin bypass) |

---

## 12. API tüketimi

- `GET /api/availability?date=YYYY-MM-DD&group=BALON` → tüm kortlar × slotlar matrix
- Her hücre `status` + `bookable`
- Performans: tek sorguda blocks, bookings, holds, contracts cache (in-memory request scope)

---

## 13. Test vektörleri

Dosya: [../testing/TEST_CASES.md](../testing/TEST_CASES.md) § Availability

---

*Fiyat önizleme: [PRICING_ENGINE.md](./PRICING_ENGINE.md).*
