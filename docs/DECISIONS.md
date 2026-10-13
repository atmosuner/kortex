# TED Tenis Ops — Architecture Decision Records

**Format:** Kısa ADR. Durum: **Kabul** (dokümantasyon aşaması).

---

## ADR-001 — Tek monolit web uygulaması

**Bağlam:** 100+ üye, tek kulüp, küçük ekip.  
**Karar:** Next.js monolit; ayrı mobil app yok (responsive PWA).  
**Sonuç:** Düşük operasyon maliyeti; native push Faz 2.

---

## ADR-002 — PostgreSQL tek kaynak

**Bağlam:** Rezervasyon tutarlılığı kritik.  
**Karar:** PostgreSQL; slot uniqueness DB constraint.  
**Sonuç:** Redis opsiyonel; hold expire cron yeterli MVP.

---

## ADR-003 — Fiyat snapshot

**Bağlam:** Mevsim/tarife sık değişir.  
**Karar:** Her booking’de `price_snapshot_json`.  
**Sonuç:** Muhasebe geçmişe dönük doğru.

---

## ADR-004 — organization_id her tabloda

**Bağlam:** SaaS şimdi yok, ileride belki.  
**Karar:** Tenant kolonu seed tek satır.  
**Sonuç:** Migration maliyeti düşük.

---

## ADR-005 — iyzico birincil ödeme

**Bağlam:** TR kart, 3DS.  
**Karar:** iyzico; PayTR alternatif.  
**Sonuç:** IMPLEMENTATION §12.

---

## ADR-006 — Fix kort runtime expand

**Bağlam:** Recurring slot DB şişirmesin.  
**Karar:** Sözleşme + weekday; availability engine expand.  
**Sonuç:** Cron ile horizon uzatma.

---

## ADR-007 — Türkçe tek dil

**Karar:** i18n altyapısı Faz 2; MVP hardcoded TR.  
**Sonuç:** Basit copy yönetimi.

---

## ADR-008 — Dokümantasyon önce

**Karar:** Kod öncesi SPEC + IMPLEMENTATION + UI + BRANDING tam set.  
**Sonuç:** Bu repo durumu.

---

*Yeni ADR: en alta ekle, tarih ve numara artır.*
