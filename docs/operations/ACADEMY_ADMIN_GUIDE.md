# Akademi Sorumlusu Kılavuzu

**Versiyon:** 1.0  
**Rol:** `academy_admin`

---

## 1. Yetki

Yalnızca `block_type = academy` blok oluşturur/düzenler/siler.  
Turnuva, tarife, üye **yok**.

---

## 2. Tipik blok

- Kort: Balon 1–2 veya Kapalı  
- Gün: Salı–Perşembe  
- Saat: 16:00–18:00 (2 slot)  
- Recurrence: dönem bitiş tarihi  
- Başlık: “Akademi U10”  

---

## 3. Dönem güncelleme

Eski blok `valid_until` kısalt → yeni blok ekle. Silme yerine bitiş tercih (audit).

---

## 4. Çakışma

Mevcut üye rezervasyonu varsa sistem uyarır — koordinasyon resepsiyon.

---

## 5. İletişim

Değişiklikten önce antrenör kadrosu ile teyit.

---

*Kış sporu: aynı mantık `winter_admin` — ayrı hesap.*
