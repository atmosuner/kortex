# Muhasebe Kılavuzu

**Versiyon:** 1.0  
**Rol:** `accounting`, `super_admin`

---

## 1. Veri kaynağı

Tek doğruluk: uygulama export + iyzico panel. Kağıt rezervasyon geçiş sonrası arşiv.

---

## 2. Günlük rutin

1. Önceki gün `payments_detail` export (channel=all)  
2. iyzico settlement ile `provider_ref` eşleştir  
3. reception/room satırları kasa defteri ile  
4. Fark notu + super_admin  

---

## 3. Fix kort

- Sözleşme ödemesi `fixed_contracts` export (Faz 3)  
- Saatlik rezervasyon tarifesinden **ayrı**  

Aktivasyon: imza + ödeme işaretlenmeden slot kilitlenmez.

---

## 4. İptal cezaları

Export kolonu `cancellation_fee`.  
Tahsil: borç bakiyesi veya ayrı ödeme — yönetim policy.

---

## 5. KDV / fatura

Uygulama fatura kesmez. Tutarlar export’ta; fatura süreci kulüp mevcut prosedür.

`prices_include_vat` setting — etiket export not satırı.

---

## 6. Ay kapanışı

1. Ay ilk-son gün export  
2. booking_summary cross-check  
3. Arşiv klasör: `TED_Tenis_2026_10/`  

---

## 7. Excel kolonları

Tam liste: [../technical/EXPORT_ACCOUNTING.md](../technical/EXPORT_ACCOUNTING.md)

---

## 8. Erişim

Hesap pasif edilince export yapılamaz. Hesap paylaşılmaz.

---

*Güvenlik: [../SECURITY_AND_PRIVACY.md](../SECURITY_AND_PRIVACY.md).*
