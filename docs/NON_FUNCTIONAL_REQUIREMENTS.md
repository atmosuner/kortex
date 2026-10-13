# TED Tenis Ops — Non-Functional Requirements

**Versiyon:** 0.1

---

## 1. Performans

| Metrik | Hedef (MVP) |
|--------|-------------|
| Availability grid API (1 gün, 9 kort) | p95 &lt; 500 ms |
| Booking confirm | p95 &lt; 2 s (ödeme hariç) |
| Eşzamanlı üye | ~50 peak (100+ üye toplam) |
| Excel export 90 gün | &lt; 30 s |

---

## 2. Kullanılabilirlik

- Responsive 320px+  
- UI prensipleri: [UI_DESIGN_PRINCIPLES.md](./UI_DESIGN_PRINCIPLES.md)  
- Türkçe; tarih formatı `12 Eki 2026 Cum`, saat `14:00`  

---

## 3. Erişilebilirlik

- WCAG 2.1 AA hedef  
- Grid renk + metin  

---

## 4. Güvenilirlik

- Booking transaction: çift rezervasyon 0  
- Hold expire job: en geç 1 dk gecikme  
- DB günlük yedek  

---

## 5. Güvenlik

Özet: [SECURITY_AND_PRIVACY.md](./SECURITY_AND_PRIVACY.md)

- HTTPS zorunlu  
- Staff RBAC  
- Ödeme PCI: sağlayıcı hosted / token  
- KVKK: aydınlatma metni kulüp hukuk onayı  

---

## 6. Bakım

- Structured logging (request id)  
- Hata izleme (Sentry vb.) Faz 1 sonu  
- Feature flag gerekmez MVP  

---

## 7. Uyumluluk

- Tarayıcı: son 2 versiyon Chrome/Safari/Edge  
- iOS Safari öncelikli (üye)  

---

## 8. Veri saklama

- Rezervasyon + ödeme: min 7 yıl (muhasebe teyit)  
- Audit log: min 2 yıl  
- Hold kayıtları: 30 gün  

---

*Operasyonel SLA kulüp içi; 7/24 destek zorunlu değil.*
