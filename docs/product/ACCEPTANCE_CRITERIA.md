# Kabul Kriterleri (Acceptance Criteria)

**Versiyon:** 1.0 — Faz bazlı

Her madde **Given / When / Then** formatında test edilebilir.

---

## Faz 1 — Takvim doğru

### AC-1.1 Kort seed
- **Given** boş DB  
- **When** seed çalışır  
- **Then** 13 bookable + 1 fitness court; display_name “Balon 1” … “Merkez Kort”

### AC-1.2 72 saat penceresi
- **Given** aktif üye, now = 2026-10-12 10:00 +03  
- **When** 2026-10-15 11:00 slot book dener  
- **Then** OUTSIDE_ADVANCE_WINDOW

### AC-1.3 Haftalık 3 limit
- **Given** üyede Pazartesi haftası 3 confirmed gelecek rez  
- **When** 4. rezervasyon  
- **Then** WEEKLY_LIMIT

### AC-1.4 Çift booking
- **Given** A ve B aynı court+slot confirm  
- **When** paralel istek  
- **Then** biri confirmed, diğeri SLOT_TAKEN

### AC-1.5 Akademi bloku
- **Given** blok Balon 3 14:00–16:00  
- **When** üye 15:00 book  
- **Then** BLOCKED

### AC-1.6 Fitness
- **When** üye FITNESS book  
- **Then** NOT_BOOKABLE

### AC-1.7 Manuel rez audit
- **When** reception manuel rez without reason  
- **Then** OVERRIDE_REASON_REQUIRED  
- **When** reason OK  
- **Then** audit_log satırı

### AC-1.8 Hold TTL
- **Given** hold 15 dk  
- **When** 16 dk sonra confirm  
- **Then** HOLD_EXPIRED

---

## Faz 2 — Para

### AC-2.1 Snapshot
- **When** confirm  
- **Then** booking.price_snapshot_json.total_cents = ödeme tutarı

### AC-2.2 Işık
- **Given** rule light_after 18:00, surcharge 50 TL  
- **When** slot 18:00  
- **Then** breakdown light_surcharge_cents = 5000

### AC-2.3 İptal ceza
- **Given** confirmed, starts in 1h  
- **When** cancel confirm  
- **Then** cancellation_fee assessed

### AC-2.4 iyzico webhook
- **When** signed success callback  
- **Then** booking confirmed + payment completed

### AC-2.5 Resepsiyon
- **When** reception payment recorded  
- **Then** booking confirmed, channel reception

---

## Faz 3 — CRM + fix

### AC-3.1 Import
- **When** CSV 100 satır, 2 hatalı  
- **Then** 98 member, error report 2 satır

### AC-3.2 Fix active
- **Given** contract active Salı 18:00 Balon 1  
- **When** üye aynı slot  
- **Then** FIXED_CONTRACT / BLOCKED

### AC-3.3 Excel export
- **When** accounting export 1–31 Oct  
- **Then** tüm confirmed + payments kolonları SPEC

---

## Faz 4 — Ops

### AC-4.1 Evening cleaning
- **Given** 3 courts had bookings today  
- **When** cron 22:05  
- **Then** 3 cleaning items pending

### AC-4.2 Field complete
- **When** field marks court done  
- **Then** completed_at set

---

## Non-functional

### AC-NF-1 Grid p95 &lt; 500ms (1 gün 9 kort)  
### AC-NF-2 WCAG: grid status text+color  
### AC-NF-3 Türkçe tüm üye mesajları  

---

*UAT: [../acceptance/UAT_CHECKLIST.md](../acceptance/UAT_CHECKLIST.md).*
