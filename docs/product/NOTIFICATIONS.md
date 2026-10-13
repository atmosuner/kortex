# Bildirimler (E-posta / SMS)

**Versiyon:** 1.0  
**Faz:** 4 (MVP’de opsiyonel minimum)

---

## 1. Kanallar

| Kanal | Faz | Not |
|-------|-----|-----|
| E-posta | 4 | Transactional |
| SMS | 5? | Maliyet — OTP ayrı |
| Push PWA | 5 | |

---

## 2. Transactional e-postalar (zorunlu set)

| ID | Tetikleyici | Konu satırı | İçerik özeti |
|----|-------------|-------------|--------------|
| N1 | booking confirmed | Rezervasyonunuz onaylandı | kort, tarih, tutar |
| N2 | booking cancelled | Rezervasyon iptali | iptal, ceza varsa |
| N3 | payment failed | Ödeme tamamlanamadı | tekrar dene |
| N4 | fix request received | Fix kort talebiniz alındı | — |
| N5 | fix contract active | Fix kortunuz aktif | gün/saat/kort |
| N6 | invite set password | TED Tenis hesabınız | link |
| N7 | password reset | Şifre sıfırlama | link |

---

## 3. Hatırlatmalar (opsiyonel)

| ID | Zamanlama | Amaç |
|----|-----------|------|
| R1 | T-24h | Maç hatırlatma |
| R2 | T-2h | İptal cezası bilgisi |

---

## 4. Staff

| ID | Alıcı | Tetikleyici |
|----|-------|-------------|
| S1 | super_admin | pending_payment stale |
| S2 | field | evening cleaning list ready |

---

## 5. Şablon kuralları

- Türkçe, siz dili  
- Plain text + HTML minimal  
- Footer: kulüp adres, KVKK link  
- Unsubscribe yalnızca pazarlama  

---

## 6. Teknik

- Queue (cron or job table)  
- idempotency key per booking+type  

---

*Copy tonu: [../design/COPY_DECK.md](../design/COPY_DECK.md).*
