# Mevsim ve Balon Geçiş Prosedürü

**Versiyon:** 1.0

Balon geçiş tarihi **sabit değil** — yönetim + hava koşulu. Sistem admin girdisi ile yansıtır.

---

## 1. Roller

- **Karar:** tenis komitesi / baş antrenör + yönetim  
- **Sistem girişi:** super_admin  
- **Duyuru:** kulüp iletişim  

---

## 2. Zaman çizelgesi (tipik)

| T-14 gün | Geçiş hedef tarih netleşir |
| T-7 | Tarife setleri hazır |
| T-3 | season_assignment girilir, simulate |
| T-1 | Üye e-posta/banner |
| T-0 00:00 | Yeni assignment aktif |
| T+1 | Doluluk ve şikayet monitor |

---

## 3. Admin adımları

1. **season_modes** — gerekirse yeni kod (ör. `kis_balon_a_2027`)  
2. **season_assignments** — her kort için `valid_from`, `valid_to`  
   - Balon 1–3 → mod A  
   - Balon 4–9 → mod B  
   - Kapalı 1–3 → kapali  
   - Merkez → merkez_kis  
3. **tariff_sets** — valid dates hizala  
4. **Preview takvim** — 1 hafta slot fiyat simülasyon  
5. Çakışan assignment **yasak** — UI red  

---

## 4. Yarım hafta geçiş

Örnek: Çarşamba 00:00 balon kapanır.

- Salı günü son slot hâlâ yaz modu fiyat  
- Çarşamba 07:00 kış modu  

Assignment `valid_from = 2026-11-05 00:00:00 +03`.

---

## 5. DST günü

Saat dilimi geçişinde slot grid **yerel saat** 07–22 sabit.  
Sorun olursa super_admin o gün için bakım bloku + manuel iletişim.

---

## 6. Rezervasyon etkisi

Advance max 72 saat — geçişten önce alınan rezervasyonlar **snapshot fiyat** ile kalır; mevsim modu snapshot içinde etiketlenir.

---

## 7. Rollback

Yanlış mod girildi:

1. Assignment valid_to düzelt  
2. Yeni doğru assignment  
3. Etkilenen üyelere tel (operasyon)  

---

## 8. Checklist

- [ ] Tüm 13 kort assignment var  
- [ ] Tarife boşluk yok  
- [ ] Akademi blokları hâlâ geçerli  
- [ ] Fix sözleşmeler court hâlâ doğru  

---

*Fiyat: [../product/PRICING_ENGINE.md](../product/PRICING_ENGINE.md).*
