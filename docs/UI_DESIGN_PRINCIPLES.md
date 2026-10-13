# TED Tenis Ops — UI Design Principles

**Ürün:** Kort rezervasyon ve kulüp operasyon arayüzü  
**Referans:** [SPECIFICATION.md](../SPECIFICATION.md), [BRANDING.md](../BRANDING.md), [USER_FLOWS.md](./USER_FLOWS.md)  
**Versiyon:** 0.1  
**Dil arayüzü:** Türkçe

Bu belge **nasıl hissettireceğimizi ve nasıl davranacağımızı** tanımlar; piksel-perfect mockup değildir. Görsel token’lar [BRANDING.md](../BRANDING.md) içindedir.

---

## 1. Tasarım felsefesi

### 1.1 Tek cümle

**“Kort bul, öde, oyna — gerisi kulübün işi.”**

Üye arayüzü telefonla 30 saniyede rezervasyon bitirmeye odaklanır. Admin ve resepsiyon **tek gerçek takvimi** hatasız yönetir. Saha arayüzü eldiven / yürürken tek elle kullanılabilir.

### 1.2 Ürün karakteri

| Özellik | Açıklama |
|---------|----------|
| Güvenilir | Dolu/müsait/ blok net; fiyat sürpriz yok |
| Kulüp hissi | Soğuk SaaS değil; TED tenis geleneğine saygılı, sade |
| Operasyonel dürüstlük | Admin override ve cezalar gizlenmez; audit hissi |
| Sakin aciliyet | Turnuva ve son slot baskısı var ama panik UI yok |

### 1.3 Kaçınılacaklar

- Generic “startup dashboard” (mor gradyan, 12 identik kart)
- Takvim yerine sonsuz form adımları
- İngilizce teknik jargon (hold, slot → **müsaitlik**, **saat dilimi**)
- Dekoratif animasyon; her kart hover’da zıplama
- Misafir / üye ayrımını gizleyen belirsiz copy

---

## 2. Kullanıcı bağlamına göre modlar

Aynı design system, **üç yoğunluk profili**:

| Profil | Kullanıcı | Yoğunluk | Birincil cihaz |
|--------|-----------|----------|----------------|
| **Üye** | Tenisçi | Düşük — az karar, büyük hedefler | Telefon |
| **Operasyon** | Resepsiyon, muhasebe | Orta-yüksek — tablo, filtre | Masaüstü + tablet |
| **Saha** | Temizlik | Minimal — liste, toggle | Telefon |

**Kural:** Üye ekranında admin metrikleri yok. Admin ekranında üye pazarlama dili yok.

---

## 3. Bilgi mimarisi (IA)

### 3.1 Üye (`/app`)

```
Giriş
  └── Ana (tarih + grup)
        └── Kort grid
              └── Rezervasyon özeti → Ödeme → Onay
  └── Rezervasyonlarım
  └── Fix kort talebi
  └── Profil (iletişim, şifre)
```

Alt navigasyon (mobil): **Rezervasyon** | **Rezervasyonlarım** | **Profil**

### 3.2 Admin (`/admin`)

```
Dashboard
Takvim (read-only genel görünüm)
Bloklar (akademi / kış / turnuva)
Mevsim & kort ayarları
Tarifeler (+ simülasyon)
Üyeler & import
Fix sözleşmeler
Manuel rezervasyon
Audit kayıtları
Rapor / Excel
```

Sol sidebar (masaüstü); mobilde accordion + “sık kullanılan” kısayol.

### 3.3 Saha (`/ops`)

Tek ekran öncelik: **Bugünkü akşam temizlik** + isteğe bağlı “bugün oynanan kortlar”.

---

## 4. Etkileşim prensipleri

### 4.1 Takvim grid (ürünün kalbi)

- **Eksen:** Satır = kort (grup içinde), sütun = saat (07:00–21:00 başlangıç)
- **Hücre durumları** (renk + ikon + metin — yalnızca renkle yetinme, [BRANDING](../BRANDING.md) semantik renkler):

| Durum | Üye görünümü | Etkileşim |
|-------|--------------|-----------|
| Müsait | Açık zemin, “Seç” | Tap → hold başlat |
| Seçili | Primary border | Özet sayfasına git |
| Dolu | Nötr gri, kilit | Tap → kısa tooltip “Dolu” |
| Blok | Çizgili / ikincil renk, etiket (Akademi, Turnuva…) | Tap → neden (1 cümle) |
| Kapalı (fitness / mevsim) | — | Gösterilmez veya devre dışı satır |

- **72 saat kuralı:** Takvimde seçilemeyen günler disabled; açıklama: “En fazla 3 gün sonrasına rezervasyon yapabilirsiniz.”
- **Hold (15 dk):** Özet ekranında geri sayım; süre bitince nazik uyarı + grid’e dön

### 4.2 Form ve onay

- Kritik işlemler **tek bir birincil buton**; destructive secondary (outline)
- İptal cezası: **2 saat** kuralı modal’da sayı + tutar; onay checkbox veya ikinci “Evet, iptal et”
- Misafir ekleme: satır satır ad; “+ Misafir ekle” — limit yok ama boş satır submit edilemez

### 4.3 Admin override

- Manuel rez / turnuva satışı: **Gerekçe** textarea zorunlu (min 10 karakter)
- Submit sonrası toast değil **kalıcı banner**: “Audit kaydı oluşturuldu”

### 4.4 Ödeme

- Tutar kırılımı her zaman görünür: kort + saat + ışık + toplam
- 3DS / redirect: “Banka sayfasına yönlendiriliyorsunuz” ara ekranı
- Başarısız ödeme: ne oldu + ne yapmalı (tekrar dene / resepsiyon)

---

## 5. Görsel sistem (BRANDING’e bağlı)

### 5.1 Tipografi

- **Okunabilirlik > karakter.** Spor sonrası parlak güneşte telefon senaryosu düşünülür.
- Gövde metni **sans-serif**; başlıklarda aynı aile veya tek display eşlik (BRANDING’de tanımlı)
- Minimum gövde **16px** mobil (iOS zoom önleme)
- Tablo/saat grid: **tabular nums** (rakamlar hizalı)

### 5.2 Renk kullanımı

- Primary: eylem (rezervasyon, öde)
- Semantik: success / warning / error — yalnızca durum için
- Grid’de **5’ten fazla renk yok**; blok tipleri ikon + kısa etiket ile ayrılır

### 5.3 Boşluk ve dokunma

- Minimum dokunma hedefi **44×44 px** (üye + saha)
- Grid hücreleri mobilde yatay kaydırma kabul edilir; dikey kaydırma kort listesi için
- Admin tablolarında satır yüksekliği compact mod (toggle)

### 5.4 Dark mode

- Faz 2 opsiyonel; MVP **açık tema** (dış saha kullanımı)
- Hazırlık: token’lar CSS variable ([BRANDING](../BRANDING.md))

---

## 6. Erişilebilirlik (WCAG 2.1 AA hedef)

- Kontrast metin / zemin ≥ 4.5:1 (normal metin)
- Durum: renk + metin/ikon (“Müsait”, “Dolu”)
- Klavye: grid’de ok tuşları ile hücre gezinme (masaüstü admin)
- `:focus-visible` belirgin halka
- `prefers-reduced-motion`: animasyon kapalı; hold sayacı anlık güncelleme yeter
- Form hataları `aria-describedby` ile alana bağlı
- Ekran okuyucu: slot “Balon 3, 14:00–15:00, müsait”

---

## 7. Metin ve ton (UX writing)

### 7.1 Ses

- **Siz** dili (kulüp formalitesi)
- Kısa, aktif: “Rezervasyonu onayla”, “Ödemeye geç”
- Hata: özür değil, yön — “Bu saat artık müsait değil. Başka bir saat seçin.”

### 7.2 Terim sözlüğü (tutarlılık)

| Kullan | Kullanma |
|--------|----------|
| Rezervasyon | Booking |
| Saat dilimi | Slot |
| Fix kort | Sabit kort (parantez ile ilk kullanım) |
| Misafir | Guest user |
| Kort grubu | Court cluster |

Tam liste: [GLOSSARY.md](./GLOSSARY.md)

### 7.3 Mikrocopy örnekleri

- Haftalık limit: “Bu hafta en fazla 3 aktif rezervasyonunuz olabilir. İptal edilen rezervasyonlar sayılmaz.”
- Blok: “Bu saat akademi programına ayrılmıştır.”
- Fix: “Talebiniz alındı. Sözleşme süreci kulüp tarafından yürütülür.”

---

## 8. Responsive davranış

| Breakpoint | Davranış |
|------------|----------|
| &lt; 640px | Üye grid yatay scroll saat; sticky grup sekmesi |
| 640–1024px | 2 sütun admin mümkün değilse tek sütun |
| ≥ 1024px | Admin sidebar sabit; grid tam genişlik |

**Saha:** Tek kolon, alt sabit “Tümünü tamamlandı işaretle” (onay dialoglu).

---

## 9. Geri bildirim ve sistem durumu

| Olay | Pattern |
|------|---------|
| Hold başladı | Inline sayaç |
| Rezervasyon onay | Tam ekran başarı + takvime ekle (ics Faz 2) |
| Ağ hatası | Banner + yeniden dene |
| Eşzamanlı çakışma | Modal: “Başka bir üye bu saati aldı” |
| Admin kayıt | Toast 5 sn + audit link |

Yükleme: grid skeleton; buton içi spinner + disabled.

---

## 10. Güven ve gizlilik (UI)

- Ödeme sayfasında kulüp adı + iletişim
- Profilde yalnızca kendi rezervasyonları; admin rolü badge (staff hesapları)
- Oturum timeout uyarısı (admin): 15 dk hareketsizlik

Detay: [SECURITY_AND_PRIVACY.md](./SECURITY_AND_PRIVACY.md)

---

## 11. Bileşen envanteri (implementasyon öncesi checklist)

| Bileşen | Varyantlar |
|---------|------------|
| Button | primary, secondary, destructive, ghost |
| Date picker | max +3 gün kısıtlı |
| Court grid cell | 6 durum |
| Guest list editor | add/remove row |
| Price breakdown | satır + toplam |
| Block badge | akademi, kış, turnuva, bakım |
| Audit reason field | zorunlu |
| Cleaning checklist row | large checkbox |
| Data table | sort, filter, export trigger |
| Empty state | CTA ile |

---

## 12. Doğrulama (tasarım review)

Pilot öncesi TED paydaşlarından sign-off:

1. Resepsiyon: admin takvim + manuel rez 5 dk içinde yapılabiliyor mu?
2. Üye (60+ yaş simülasyonu): grid okunuyor mu?
3. Saha: akşam listesi tek elle tamamlanıyor mu?
4. Renk körlüğü simülasyonu: grid durumları ayırt ediliyor mu?

---

## 13. İlişkili belgeler

- Görsel kimlik: [BRANDING.md](../BRANDING.md)
- Akışlar: [USER_FLOWS.md](./USER_FLOWS.md)
- Yetkiler: [ROLES_AND_PERMISSIONS.md](./ROLES_AND_PERMISSIONS.md)

---

*Güncelleme: UI kararları bu dosyada versiyonlanır; uygulama kodu başlamadan önce Figma isteğe bağlı eklenti.*
