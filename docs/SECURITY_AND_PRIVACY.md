# TED Tenis Ops — Security & Privacy

**Versiyon:** 0.1  
**Not:** KVKK metinleri kulüp hukuk danışmanı onayı ile yayınlanır.

---

## 1. Veri sınıfları

| Sınıf | Örnek | Koruma |
|-------|-------|--------|
| Kimlik | ad, email, telefon | Auth + RBAC |
| Finans | ödeme ref, tutar | Şifreli transit; kart PAN saklanmaz |
| Operasyon | audit, gerekçe | Staff only |
| Misafir | ad (üye rezervasyonunda) | Üye + staff |

---

## 2. Kimlik doğrulama

- MVP: email + güçlü şifre (min 10 karakter, breach list check önerilir)  
- Oturum: httpOnly cookie veya secure token  
- Şifre sıfırlama: time-limited link  
- Brute force: rate limit login  

---

## 3. Yetkilendirme

- Rol tabanlı ([ROLES_AND_PERMISSIONS.md](./ROLES_AND_PERMISSIONS.md))  
- Üye yalnızca `member_id = self` rezervasyon  
- IDOR test: booking UUID enumerate  

---

## 4. Ödeme güvenliği

- Kart verisi uygulama DB’sine **yazılmaz**  
- Webhook imza doğrulama  
- Tutar sunucuda `price_snapshot` ile karşılaştırılır (client manipülasyon)  

---

## 5. Admin riskleri

- Override + manuel rez: audit zorunlu  
- super_admin sayısı minimum (2 kişi)  
- MFA roadmap Faz 2  

---

## 6. KVKK (Türkiye)

- **Veri sorumlusu:** TED Spor Kulübü  
- **İşleme amacı:** kort rezervasyonu, tahsilat, operasyon  
- **Hukuki sebep:** sözleşme + meşru menfaat (güvenlik logları)  
- **Saklama:** NFR belgesi  
- **Haklar:** erişim, düzeltme, silme talebi kanalları (info@tedclub.org.tr yönlendirme)  
- **Alt işleyici:** hosting, ödeme sağlayıcı — DPA/sözleşme  

Üye arayüzünde kayıt/girişte **aydınlatma metni** linki.

---

## 7. Loglama

- PII loglara düşmemeli (tam kart, şifre)  
- Audit log değiştirilemez (append-only)  

---

## 8. Yedekleme ve felaket

- Günlük DB backup, şifreli depolama  
- RTO/RPO kulüp IT ile tanımlanır (öneri RPO 24s)  

---

## 9. Güvenlik testi

- Faz 1 sonu: OWASP top 10 checklist  
- Pen test: pilot öncesi opsiyonel  

---

*Teknik kontroller implementasyonda [IMPLEMENTATION.md](../IMPLEMENTATION.md) ile uyumlu uygulanır.*
