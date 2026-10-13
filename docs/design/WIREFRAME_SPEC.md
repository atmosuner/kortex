# Wireframe Spesifikasyonu — Ekran Ekran

**Versiyon:** 1.0  
**Referans:** [UI_DESIGN_PRINCIPLES.md](../UI_DESIGN_PRINCIPLES.md), [BRANDING.md](../../BRANDING.md)

Figma zorunlu değil; bu belge implementasyon ve tasarım için **canonical layout**.

---

## Ekran indeksi

| ID | Ekran | Rol | Öncelik |
|----|-------|-----|---------|
| M1 | Giriş | all | P0 |
| M2 | Ana rezervasyon grid | member | P0 |
| M3 | Rezervasyon özeti | member | P0 |
| M4 | Ödeme / redirect | member | P1 |
| M5 | Onay başarı | member | P0 |
| M6 | Rezervasyonlarım | member | P0 |
| M7 | İptal modal | member | P0 |
| M8 | Fix talep | member | P2 |
| M9 | Profil | member | P1 |
| A1 | Admin dashboard | admin | P1 |
| A2 | Blok listesi / form | admin | P0 |
| A3 | Manuel rezervasyon | reception | P0 |
| A4 | Üye arama | reception | P1 |
| A5 | Tarife editör | super_admin | P2 |
| A6 | Mevsim timeline | super_admin | P1 |
| A7 | Audit log | super_admin | P1 |
| A8 | Export | accounting | P2 |
| O1 | Akşam temizlik | field | P1 |

---

## M2 — Ana rezervasyon grid (mobil)

```text
┌─────────────────────────────────────┐
│ ☰  TED Tenis          Profil avatar │
├─────────────────────────────────────┤
│  [ Balon ] [ Kapalı ] [ Merkez ]    │  ← segment control
├─────────────────────────────────────┤
│  ◀   14 Eki 2026 Salı   ▶          │  ← max +3 gün ok disabled
├─────────────────────────────────────┤
│       07  08  09 ... 21             │  ← horizontal scroll time
│ B1    ·   ·   ■   ·   ○             │
│ B2    ○   ○   ○   ■   ·             │
│ ...                                 │
│ B9    ░   ░   ░   ░   ░   Akademi   │
└─────────────────────────────────────┘
○ müsait  ■ dolu  · seçili  ░ blok
```

**Sticky:** grup sekmesi + tarih.  
**Tap müsait:** → M3.

---

## M3 — Rezervasyon özeti

```text
┌─────────────────────────────────────┐
│ ← Geri                              │
├─────────────────────────────────────┤
│ Balon 3                             │
│ 14 Eki 2026 · 18:00 – 19:00         │
├─────────────────────────────────────┤
│ Misafirler                          │
│ [ Ad Soyad            ] [−]         │
│ [ + Misafir ekle ]                  │
├─────────────────────────────────────┤
│ Kort ücreti          450,00 ₺       │
│ Işık                  50,00 ₺       │
│ ─────────────────────────────       │
│ Toplam               500,00 ₺       │
├─────────────────────────────────────┤
│ ⏱ 14:32 kaldı (hold)                │
├─────────────────────────────────────┤
│ [      Ödemeye geç      ]           │
└─────────────────────────────────────┘
```

---

## M6 — Rezervasyonlarım

Kart listesi: kort, tarih, durum badge, “İptal et” (secondary).

---

## M7 — İptal modal

- &lt; 2 saat: sarı banner ceza tutarı  
- [Vazgeç] [İptali onayla]  

---

## A2 — Blok formu

Alanlar: tip select, başlık, kort multiselect veya grup, başlangıç/bitiş datetime, tekrar (opsiyonel).  
Kaydet / Sil.

---

## A3 — Manuel rezervasyon

Üye autocomplete, kort, slot picker, gerekçe textarea (min 10 char counter), kanal select, [Oluştur].

---

## A5 — Tarife editör (Faz 2)

Sol: tariff set listesi. Sağ: kural tablosu + [Simüle] panel.

---

## O1 — Akşam temizlik

Büyük satırlar (min 56px):

```text
[ ] Balon 3
[✓] Kapalı 1
```

Alt: “3 / 5 tamamlandı”

---

## Responsive breakpoint notları

- M2 masaüstü: grid tam genişlik, saatler wrap değil scroll  
- Admin A*: sidebar 240px  

---

## Erişilebilirlik wireframe

- Her hücre `aria-label`  
- Modal focus trap  

---

*Bileşen detay: [COMPONENT_SPEC.md](./COMPONENT_SPEC.md).*
