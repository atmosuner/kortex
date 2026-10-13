# Tarife Ek Tablosu — TED Doldurulacak

**Versiyon:** 0.1 (boş şablon)  
**Talimat:** Her satır bir `tariff_rule` seed/import satırına dönüşür.  
**Para birimi:** TRY, kuruş hassasiyeti implementasyonda.

---

## A. Balon kortlar

### A1 — Kış balon grup A (Balon 1–3)

| season_mode | gün | saat_from | saat_to | base_tl | isik_ek_tl | not |
|-------------|-----|-----------|---------|---------|------------|-----|
| kis_balon_a | Pzt–Paz | 07:00 | 17:59 | | | |
| kis_balon_a | Pzt–Paz | 18:00 | 21:59 | | | ışık |
| | | | | | | |

### A2 — Kış balon grup B (Balon 4–9)

| season_mode | gün | saat_from | saat_to | base_tl | isik_ek_tl | not |
|-------------|-----|-----------|---------|---------|------------|-----|
| kis_balon_b | | | | | | |

### A3 — Yaz açık (Balon 1–9)

| season_mode | gün | saat_from | saat_to | base_tl | isik_ek_tl | not |
|-------------|-----|-----------|---------|---------|------------|-----|
| yaz_acik | | | | | | |

---

## B. Kapalı kortlar (1–3)

| season_mode | kort | saat_from | saat_to | base_tl | isik_ek_tl |
|-------------|------|-----------|---------|---------|------------|
| kapali | 1 | | | | |
| kapali | 2 | | | | |
| kapali | 3 | | | | |

---

## C. Merkez kort

| season_mode | saat_from | saat_to | base_tl | isik_ek_tl |
|-------------|-----------|---------|---------|------------|
| merkez_yaz | | | | |
| merkez_kis | | | | |

---

## D. Fix kort (dönemlik — saatlik değil)

| plan_adı | süre | toplam_tl | ödeme | not |
|----------|------|-----------|-------|-----|
| Fix yıllık std | 12 ay | | peşin/taksit | |
| | | | | |

---

## E. İptal cezası

| parametre | değer |
|-----------|-------|
| cancellation_fee_tl | |
| cancellation_fee_percent | opsiyonel |

---

## F. Işık global

| parametre | değer |
|-----------|-------|
| light_after_time | örn. 18:00 |
| kortlar_ışıksız | liste |

---

## G. Onay

| Rol | Ad | Tarih |
|-----|-----|-------|
| Tenis komitesi | | |
| Muhasebe | | |

---

*Motor: [PRICING_ENGINE.md](./PRICING_ENGINE.md).*
