# Seed Data ve Ortam Kurulum Verisi

**Versiyon:** 1.0

---

## 1. Organization

```json
{
  "id": "00000000-0000-4000-8000-000000000001",
  "name": "Tenis Eskrim Dağcılık Spor Kulübü",
  "timezone": "Europe/Istanbul",
  "settings_json": {
    "advance_booking_hours": 72,
    "weekly_active_booking_limit": 3,
    "hold_minutes": 15,
    "slot_duration_minutes": 60,
    "daily_start": "07:00",
    "daily_end": "22:00",
    "cancellation_fee_hours": 2,
    "cancellation_fee_cents": 0,
    "light_after_time": "18:00",
    "prices_include_vat": true,
    "guest_affects_price": false
  }
}
```

`cancellation_fee_cents` TED yönetim doldurur.

---

## 2. Courts (13 + 1)

| group_code | number | display_name | bookable |
|------------|--------|--------------|----------|
| BALON | 1–9 | Balon {n} | true |
| KAPALI | 1–3 | Kapalı {n} | true |
| MERKEZ | 1 | Merkez Kort | true |
| FITNESS | 1 | Fitness | false |

UUID: deterministic v5 veya random — test için fixed UUID listesi implementasyonda.

---

## 3. Season modes (örnek etiketler)

| code | name |
|------|------|
| yaz_acik | Yaz — açık |
| kis_balon_a | Kış — balon grup A |
| kis_balon_b | Kış — balon grup B |
| kapali | Kapalı kort |
| merkez_yaz | Merkez yaz |
| merkez_kis | Merkez kış |

Admin gerçek takvimi girer — seed sadece örnek 1 haftalık assignment.

---

## 4. Test users

| Rol | email | Not |
|-----|-------|-----|
| super_admin | admin@ted-test.local | |
| reception | reception@ted-test.local | |
| field | field@ted-test.local | |
| member | member1@ted-test.local | membership_no 90001 |
| member | member2@ted-test.local | limit test |

Şifre: env `SEED_PASSWORD` — prod seed yok.

---

## 5. Demo blocks

- Akademi: Balon 1–2, next Tue 16:00–18:00 weekly  
- Turnuva: Balon 3–5, next Sat 08:00–20:00 once  

---

## 6. Tariff seed (Faz 2)

Placeholder rules 0 TL veya 100 TL — sadece dev.

---

## 7. Staging vs production

| | Staging | Production |
|---|---------|------------|
| Seed users | ✓ | ✗ |
| Real members | anonymized subset | import only |
| iyzico | sandbox | live |

---

## 8. Seed komutu (gelecek)

```bash
pnpm prisma db seed
```

---

*Kort envanter SPEC §3 ile birebir.*
