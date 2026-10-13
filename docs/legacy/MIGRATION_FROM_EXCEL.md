# Legacy Excel / Kağıt → Sistem Geçişi

**Versiyon:** 1.0

---

## 1. Hedef

Canlı geçişte çift kayıt süresini minimize; “hangi sistem doğru?” dönemini ≤ 2 hafta pilot ile kapat.

---

## 2. Fazlar

### Faz A — Paralel okuma (1–2 hafta)

- Sistem canlı; resepsiyon **hem Excel hem app** kontrol  
- Yeni rezervasyon **yalnızca app** (policy)  
- Eski kağıt rezervasyonlar admin manuel girilir veya import edilmez (geçmiş)

### Faz B — Tek kaynak

- Excel arşiv  
- Muhasebe yalnızca export  

### Faz C — Temizlik

- Fix sözleşmeleri tamamen dijital  
- Akademi blokları yıllık template

---

## 3. Veri taşıma

| Veri | Yöntem |
|------|--------|
| Üye listesi | [IMPORT_MEMBERS.md](../technical/IMPORT_MEMBERS.md) |
| Gelecek rezervasyon | Admin manuel veya bulk CSV (Faz 2 opsiyon) |
| Geçmiş rezervasyon | Opsiyonel arşiv import — raporlama dışı |
| Fix sözleşmeler | Admin tek tek Faz 3 |
| Tarife tablosu | Admin tariff UI |

---

## 4. Gelecek rezervasyon bulk (opsiyonel CSV)

Kolonlar: membership_no, court_group, court_number, starts_at, guest_names

Validation strict; dry-run preview.

---

## 5. Eğitim

- Resepsiyon 2 saat workshop  
- Üye duyuru: web + kulüp sitesi  
- Saha 30 dk `/ops`  

Bkz. operasyon runbook’ları.

---

## 6. Geri dönüş planı

Kritik arıza &gt; 4 saat: resepsiyon kağıt mod (prosedür); veri app’te kalır, sync sonra.

---

## 7. Başarı kriteri geçiş

- 7 gün çift rezervasyon 0  
- ≥ %50 yeni rez online (pilot sonu hedef)

---

*Pilot: [../acceptance/UAT_CHECKLIST.md](../acceptance/UAT_CHECKLIST.md).*
