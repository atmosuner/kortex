# TED Tenis Ops — Data Dictionary

**Referans:** [IMPLEMENTATION.md](../IMPLEMENTATION.md) §3  
**Versiyon:** 0.1

Alan tipleri mantıksal; fiziksel tip implementasyonda Prisma ile netleşir.

---

## organization

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| id | UUID | ✓ | |
| name | string | ✓ | TED Spor Kulübü |
| timezone | string | ✓ | Europe/Istanbul |
| settings_json | json | | advance_hours=72, weekly_limit=3, hold_minutes=15 |

---

## court

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| id | UUID | ✓ | |
| organization_id | UUID | ✓ | |
| group_code | enum | ✓ | BALON, KAPALI, MERKEZ, FITNESS |
| number | int | ✓ | Grup içi numara |
| display_name | string | ✓ | UI: "Balon 3" |
| bookable | bool | ✓ | FITNESS false |
| metadata_json | json | | Notlar |

---

## member

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| id | UUID | ✓ | |
| membership_no | string | ✓ | Unique |
| first_name, last_name | string | ✓ | |
| email | string | ✓ | |
| phone | string | | |
| status | enum | ✓ | active, suspended, passive |
| notes | text | | |

---

## user (auth)

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| id | UUID | ✓ | Auth provider id ile eş |
| member_id | UUID | | Null = saf staff |
| role | enum | ✓ | Bkz. ROLES |
| email | string | ✓ | |

---

## booking

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| id | UUID | ✓ | |
| court_id | UUID | ✓ | |
| member_id | UUID | ✓ | Booker |
| starts_at, ends_at | timestamptz | ✓ | UTC store |
| status | enum | ✓ | pending_payment, confirmed, cancelled, completed |
| booking_type | enum | ✓ | normal, admin_manual, override |
| price_snapshot_json | json | ✓ | |
| cancellation_fee_cents | int | | |
| override_reason | text | | Admin only |

---

## booking_guest

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| booking_id | UUID | ✓ | |
| full_name | string | ✓ | |
| phone | string | | |

---

## slot_hold

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| court_id, member_id | UUID | ✓ | |
| starts_at | timestamptz | ✓ | |
| expires_at | timestamptz | ✓ | |

---

## calendar_block

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| block_type | enum | ✓ | academy, winter, tournament, maintenance |
| court_id | UUID | | Null = grup veya global |
| group_code | enum | | |
| starts_at, ends_at | timestamptz | ✓ | |
| title | string | | UI etiket |

---

## season_assignment

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| court_id | UUID | ✓ | |
| season_mode_id | UUID | ✓ | |
| valid_from, valid_to | date | ✓ | |

---

## tariff_rule

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| priority | int | ✓ | Küçük = önce |
| amount_cents | int | ✓ | |
| light_surcharge_cents | int | | |
| light_after_time | time | | |
| court_id, group_code, season_mode_id | | | Filtreler |

---

## payment

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| amount_cents | int | ✓ | |
| channel | enum | ✓ | online, reception, room |
| status | enum | ✓ | pending, completed, failed, refunded |
| provider_ref | string | | iyzico |
| recorded_by_user_id | UUID | | Manuel kanallar |

---

## fixed_court_contract

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| member_id, court_id | UUID | ✓ | |
| weekday | int | ✓ | 0=Paz … 6=Cmt veya ISO |
| start_time | time | ✓ | |
| signed_at | date | ✓ | |
| active_from, active_to | date | ✓ | |
| payment_status | enum | ✓ | pending, paid |
| status | enum | ✓ | requested, active, ended, cancelled |

---

## audit_log

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| actor_user_id | UUID | ✓ | |
| action | string | ✓ | |
| entity_type, entity_id | | ✓ | |
| before_json, after_json | json | | |
| reason | text | | |

---

## evening_cleaning_item

| Alan | Tip | Zorunlu | Açıklama |
|------|-----|---------|----------|
| run_id | UUID | ✓ | Günlük batch |
| court_id | UUID | ✓ | |
| completed_at | timestamptz | | |

---

*Enum değerleri kodda tek kaynak (Prisma) olacak; bu belge ürün dilidir.*
