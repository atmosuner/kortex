# Turnuva ve Etkinlik — Kort Kapatma

**Versiyon:** 1.0

---

## 1. Politika (SPEC)

- Turnuva süresince **üye self-servis satış kapalı**  
- **super_admin override** ile tek slot satılabilir (audit zorunlu)  
- Geçiş döneminde esneklik — sistem audit ile disipline eder  

---

## 2. Blok oluşturma

1. Admin → Bloklar → Yeni  
2. Tip: `tournament`  
3. Başlık: “8-9-10 Yaş Turnuvası”  
4. Kortlar: çoklu seçim Balon 1–9 veya grup  
5. `starts_at`, `ends_at` — çok günlük  
6. Kaydet  

Overlap uyarısı: mevcut rezervasyon varsa admin iptal/taşıyıp devam.

---

## 3. Tekrarlayan turnuva günleri

Recurrence `weekly` + until — akademi benzeri.

---

## 4. Override satış

1. Turnuva bloğu aktif slot  
2. super_admin → Override rezervasyon  
3. Gerekçe: “Final maçı — yönetim onayı”  
4. Tutar manuel  
5. Audit kaydı kontrol  

Resepsiyon override yapamaz.

---

## 5. Üye UI

Bloklu hücre etiketi: **Turnuva** — tooltip kısa açıklama.

---

## 6. Akademi vs turnuva

Akademi: `academy_admin` girebilir.  
Turnuva: yalnız super_admin (önerilen).

---

## 7. İletişim

Turnuva takvimi kulüp sitesi ile uyum — aynı gün/saat.

---

*Blok algoritması: [../product/AVAILABILITY_RULES.md](../product/AVAILABILITY_RULES.md).*
