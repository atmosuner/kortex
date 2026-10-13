# Üye Import — CSV/Excel Spesifikasyonu

**Versiyon:** 1.0

---

## 1. Amaç

TED mevcut Excel/kulüp listesinden ilk CRM doldurma ve periyodik güncelleme.

---

## 2. Dosya formatı

- **Encoding:** UTF-8 (BOM kabul)  
- **Ayraç:** `,` CSV veya `.xlsx` ilk sayfa  
- **Max satır:** 5000 / import batch  
- **Max dosya:** 5 MB  

---

## 3. Kolon şeması

| Kolon | Zorunlu | Format | Örnek |
|-------|---------|--------|-------|
| membership_no | ✓ | string, unique | 12345 |
| first_name | ✓ | string | Ayşe |
| last_name | ✓ | string | Yılmaz |
| email | ✓ | email | ayse@ornek.com |
| phone | | E.164 veya 05xx | +905551234567 |
| status | | active \| passive \| suspended | active |
| notes | | string | |

Ek kolonlar ignore (preview’da uyarı).

---

## 4. Validasyon kuralları

1. `membership_no` boş → satır hata  
2. Duplicate membership_no dosya içi → satır hata  
3. email format invalid → satır hata  
4. status bilinmeyen → default active + warning  
5. phone normalize TR → +90…

---

## 5. Duplicate stratejisi (import wizard)

Admin seçer:

| Mod | Davranış |
|-----|----------|
| skip | Mevcut üye atlanır |
| update | Boş olmayan alanlar güncellenir |
| fail | Tüm import rollback |

Default öneri: **update** email/phone, membership_no key.

---

## 6. Import akışı UI

1. Şablon indir  
2. Dosya yükle  
3. **Preview** — 20 satır + hata listesi  
4. Mod seç  
5. Commit  
6. Özet: created / updated / skipped / errors  

---

## 7. İlk giriş davet

Import sonrası:

- `user` kaydı yok → invite email “Şifre oluştur”  
- Zaten user var → email gönderilmez  

Batch invite rate limit: 50/saat.

---

## 8. Örnek CSV

```csv
membership_no,first_name,last_name,email,phone,status
10001,Mehmet,Demir,mehmet@ornek.com,+905551112233,active
10002,Zeynep,Kaya,zeynep@ornek.com,,active
```

---

## 9. Hata raporu export

`import_errors_{batch_id}.csv`:

```csv
row_number,membership_no,error_code,message
3,10002,DUPLICATE_EMAIL,email already used by 10099
```

---

## 10. Legacy Excel mapping (TED)

Kulüp dosyası farklı başlık kullanıyorsa admin **column mapping** ekranı (Faz 3):

| Dosya başlığı | Sistem alanı |
|---------------|--------------|
| Üye No | membership_no |
| Ad | first_name |
| Soyad | last_name |

Mapping preset kaydet `ted_legacy_v1`.

---

## 11. Audit

Her import: `audit_log` action `members_import`, actor, counts json.

---

*Veri sözlüğü: [../DATA_DICTIONARY.md](../DATA_DICTIONARY.md).*
