# Muhasebe Excel Export Spesifikasyonu

**Versiyon:** 1.0

---

## 1. Amaç

Muhasebenin günlük/aylık mutabakatı; Logo/Netsis yok — manuel Excel.

---

## 2. Export türleri

| Tür | Kod | İçerik |
|-----|-----|--------|
| Tahsilat detay | `payments_detail` | Her ödeme satırı |
| Rezervasyon özet | `bookings_summary` | Rezervasyon + tutar |
| Fix sözleşme | `fixed_contracts` | Dönemsel fix ödemeler |
| İptal ceza | `cancellation_fees` | Cezalı iptaller |
| Günlük kasa | `daily_cash` | reception+room kanalları |

MVP: **payments_detail** zorunlu; diğerleri Faz 3.

---

## 3. payments_detail kolonları

| # | Kolon adı | Tip | Açıklama |
|---|-----------|-----|----------|
| A | export_generated_at | datetime | |
| B | payment_id | UUID | |
| C | payment_date | date | completed_at Istanbul |
| D | payment_time | time | |
| E | channel | enum | online / reception / room |
| F | amount_try | decimal | 2 hane |
| G | currency | TRY | sabit |
| H | payment_status | string | |
| I | provider_ref | string | iyzico ref |
| J | booking_id | UUID | |
| K | booking_starts_at | datetime | |
| L | booking_ends_at | datetime | |
| M | court_display | string | Balon 3 |
| N | court_group | string | BALON |
| O | member_membership_no | string | |
| P | member_name | string | |
| Q | booking_type | string | normal / admin_manual / override |
| R | price_snapshot_total | decimal | |
| S | cancellation_fee | decimal | |
| T | recorded_by | string | staff email if manual |
| U | notes | string | |

---

## 4. Filtreler (API)

- `from`, `to` (date inclusive)  
- `channel[]`  
- `court_group`  
- `include_cancelled` default false  

---

## 5. Dosya adı

`TED_Tenis_Tahsilat_{from}_{to}_{timestamp}.xlsx`

Sayfa adı: `Tahsilat`

---

## 6. Formatting

- Header row bold, freeze panes row 1  
- amount columns number format `#.##0,00`  
- Tarih TR locale  

---

## 7. Fix export (Faz 3)

Kolonlar: contract_id, member, court, weekday, start_time, signed_at, active_from, active_to, fee, payment_status, paid_at.

---

## 8. Mutabakat prosedürü

1. Muhasebe ay sonu export  
2. iyzico panel CSV ile provider_ref eşleştir  
3. reception satırları kasa defteri ile  
4. Fark → admin audit  

Bkz. [../operations/ACCOUNTING_GUIDE.md](../operations/ACCOUNTING_GUIDE.md)

---

## 9. Güvenlik

- Export sadece accounting + super_admin  
- Log: who exported when, row count  
- PII — dosya kulüp içi, email ile gönderilmez (Faz 4)

---

## 10. Performans

90 gün &lt; 30 sn — NFR. Stream write ExcelJS.

---

*API: [API_REFERENCE.md](./API_REFERENCE.md) §13.*
