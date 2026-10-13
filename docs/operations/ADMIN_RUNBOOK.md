# Süper Admin Runbook

**Versiyon:** 1.0  
**Rol:** `super_admin`

---

## 1. Günlük kontrol listesi

- [ ] Dashboard: bugün doluluk anormal mi?  
- [ ] Bekleyen fix talepleri  
- [ ] Dün akşam temizlik tamamlanmamış kort  
- [ ] pending_payment &gt; 10?  
- [ ] Audit log: override var mı?  

---

## 2. Kort yönetimi

### Yeni kort (nadir)

1. Admin → Kortlar → Ekle  
2. group_code, number, display_name, bookable  
3. Mevsim assignment ekle  
4. Tarife kuralı ekle (Faz 2)  

### Fitness kort

`bookable=false` — asla true yapma tenis rez için.

---

## 3. Mevsim / balon geçişi

Detay: [SEASON_TRANSITION.md](./SEASON_TRANSITION.md)

Özet:

1. Yeni season_mode etiketleri  
2. Kort bazlı tarih aralığı ata  
3. Tarife set valid_from güncelle  
4. Üye duyuru (opsiyonel banner)  

---

## 4. Tarife değişikliği

1. Yeni `tariff_set` oluştur (eskiyi silme)  
2. valid_from = değişim günü 00:00  
3. Simulate birkaç slot  
4. Eski set valid_to kapat  

Geçmiş rezervasyon etkilenmez.

---

## 5. Turnuva

[TOURNAMENT_BLOCKS.md](./TOURNAMENT_BLOCKS.md)

---

## 6. Fix kort

[FIX_COURT_PROCESS.md](./FIX_COURT_PROCESS.md)

---

## 7. Üye import

1. Şablon indir  
2. TED Excel’den kopyala-yapıştır  
3. Preview hataları düzelt  
4. Update modu  
5. Invite batch  

---

## 8. Acil override

Turnuva slot satışı:

1. Takvim → slot → Override  
2. Gerekçe yaz (turnuva — …)  
3. Tutar gir  
4. Audit doğrula  

---

## 9. Incident

Sistem down → [DEPLOYMENT.md](../technical/DEPLOYMENT.md) rollback + kağıt mod duyurusu.

---

## 10. Yetki yönetimi

- En az 2 super_admin  
- Ayrılan personel: user disable same day  

---

*RBAC: [../ROLES_AND_PERMISSIONS.md](../ROLES_AND_PERMISSIONS.md).*
