# Saha Personeli — Akşam Temizlik Kılavuzu

**Versiyon:** 1.0  
**Rol:** `field`

---

## 1. Amaç

Her akşam o gün **kullanılmış** tenis kortlarının temizlik takibi. Rezervasyon bitişinde anlık görev yok — toplu liste.

---

## 2. Cihaz

Kişisel veya kulüp telefonu; mobil tarayıcı. Ana ekrana kısayol (PWA Faz 2).

---

## 3. Adımlar

1. `/ops` veya “Akşam temizlik” linki  
2. Giriş (field hesabı)  
3. Liste — örn. “Balon 3”, “Kapalı 1”  
4. Kort bitince satıra dokun → **Temizlendi**  
5. Tümü bitince çıkış  

---

## 4. Liste nasıl oluşur?

Sistem: bugün `confirmed` veya `completed` booking olan distinct kortlar.  
Booking olmayan kort listede yok.

---

## 5. Sorunlar

| Durum | Ne yap |
|-------|--------|
| Liste boş ama kort kullanıldı | Resepsiyon manuel rez girmiş olabilir — yönetim bildir |
| Uygulama açılmıyor | Yedek: resepsiyon kağıt checklist (geçiş) |
| Yanlışlıkla işaretledim | super_admin geri al (Faz 2) veya yönetim |

---

## 6. Güvenlik

Field hesabı yalnızca ops ekranı — admin yok.

---

*UI: [../UI_DESIGN_PRINCIPLES.md](../UI_DESIGN_PRINCIPLES.md) saha profili.*
