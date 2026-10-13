# Resepsiyon Kullanım Kılavuzu

**Versiyon:** 1.0  
**Rol:** `reception`

---

## 1. Giriş

Tarayıcı: masaüstü Chrome/Safari. URL: prod/staging kulüp tarafından iletilir.  
Oturum: kişisel hesap — paylaşımlı şifre yasak.

---

## 2. Günlük işler

### Sabah

- Bugün takvim — turnuva/akademi blokları kontrol  
- pending_payment temiz mi?  

### Gün içi

- Telefon: üye adı/soyad veya üye no ile ara  
- Müsaitlik: admin takvim read-only veya üye gibi grup+ tarih  
- **Yeni rezervasyon kağıda yazılmaz** — sistem zorunlu  

### Akşam

- Kasa: online tahsilatlar otomatik; nakit kayıtları kontrol  
- Saha temizlik listesi başladı mı (22:00 civarı)?  

---

## 3. Manuel rezervasyon

1. Admin → Manuel rezervasyon  
2. Üye seç (aktif olmalı)  
3. Kort + saat  
4. **Gerekçe** zorunlu — örnek: “Telefon — acil maç, sistem erişimi yok”  
5. Tahsilat: resepsiyon veya oda  
6. Onay  

**Not:** Haftalık 3 limit reception için de geçerli (super_admin bypass).

---

## 4. Tahsilat kanalları

| Kanal | Ne zaman |
|-------|----------|
| online | Üye kendi öder — siz dokunmayın |
| reception | Nakit/kart POS kasa |
| room | Ofis/oda ödeme |

Tutar sistemden gelir; manuel indirim yok (super_admin).

---

## 5. Üye sorunları

| Soru | Cevap / aksiyon |
|------|-----------------|
| “3 rezervasyonum var” | Rezervasyonlarım göster; iptal öner |
| “Ödedim onay yok” | pending_payment ara; muhasebe/super_admin |
| “Misafir getiriyorum” | Üye kendi ekler; limit yok |
| “Non-member oynayabilir mi?” | Hayır — sadece üye rez açar |

---

## 6. Fix kort

Resepsiyon talep almaz — yönetim formu. Bilgi: sözleşme + muhasebe.

---

## 7. Oda ödemesi

Aynı manuel akış; channel = `room`.

---

## 8. Yapılmaması gerekenler

- Başka üye adına şifre ile giriş  
- Gerekçesiz manuel rez  
- Excel paralel yeni rez (geçiş sonrası)  

---

*Akış: [../USER_FLOWS.md](../USER_FLOWS.md).*
