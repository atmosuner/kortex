# TED Tenis Ops — Test Strategy

**Referans:** [IMPLEMENTATION.md](../IMPLEMENTATION.md) §10, [SPECIFICATION.md](../SPECIFICATION.md)  
**Versiyon:** 0.1

---

## 1. Katmanlar

| Katman | Araç | Kapsam |
|--------|------|--------|
| Domain unit | Vitest | Availability, pricing (Faz 2), cancel penalty |
| Integration | Vitest + test DB | Booking transaction, constraints |
| E2E | Playwright | Üye happy path (Faz 1 sonu) |
| Manual | Checklist | Resepsiyon pilot |

---

## 2. Zorunlu domain senaryoları

1. Aynı court+slot eşzamanlı confirm → biri başarı, biri SLOT_TAKEN  
2. Hold expire → slot tekrar müsait  
3. Akademi bloku overlap → member book red  
4. 4. aktif rezervasyon aynı ISO hafta → WEEKLY_LIMIT  
5. Slot starts_at = now + 73h → ADVANCE_LIMIT  
6. FITNESS court → NOT_BOOKABLE  
7. İptal T-90min → cancellation_fee uygulanır  
8. İptal T-150min → fee yok  
9. Admin manual → audit_log satırı  
10. Turnuva block → member red; super_admin override → audit  

---

## 3. Fiyat (Faz 2)

- Season mode + light rule → snapshot tutarlılığı  
- Tarife değişimi sonrası eski booking snapshot değişmez  

---

## 4. Regresyon

- PR: unit + integration zorunlu  
- E2E: main branch nightly (opsiyonel)  

---

## 5. Pilot kabul (TED)

- [ ] Resepsiyon 5 dk manuel rez  
- [ ] Üye grid 3 gün penceresi  
- [ ] Muhasebe export kolonları doğru  
- [ ] Çift rezervasyon denemesi başarısız  

---

*Performans hedefleri: [NON_FUNCTIONAL_REQUIREMENTS.md](./NON_FUNCTIONAL_REQUIREMENTS.md).*
