# TED Tenis — Kort Rezervasyon ve Operasyon Sistemi

**Ürün kodu (çalışma adı):** Kortex / TED Tenis Ops  
**Kulüp:** Tenis Eskrim Dağcılık Spor Kulübü (TED) — [tedclub.org.tr](https://www.tedclub.org.tr/)  
**Merkez:** Tarabya Bayırı Caddesi No:68, 34457 Tarabya, İstanbul  
**Versiyon:** 0.1 (ürün) — dokümantasyon paketi 0.2, indeks: [DOCUMENTATION_INDEX.md](./DOCUMENTATION_INDEX.md)  
**Dil:** Türkçe (yalnızca)  
**Dağıtım modeli:** Tek kulüp (TED); veri modeli ileride çok kiracılı SaaS’a genişletilebilir olacak, şu an SaaS hedefi yok.

---

## 1. Özet ve problem

TED tenis kortlarında rezervasyon, tahsilat ve saha operasyonu Excel, kağıt ve birkaç personele bağımlı yürütülüyor. Bu durum çift rezervasyon riski, tahsilat hataları, akademi/kış sporu/turnuva bloklarıyla çakışma ve raporlama zorluğu yaratıyor.

**Hedef:** Üyelerin web/mobil uyumlu arayüzden kort rezerve edip online ödeme yapabildiği; yönetimin tek gerçek takvimden blok, tarife ve etkinlik yönettiği; resepsiyon ve sahanın tahsilat ile akşam operasyonunu dijitalleştirdiği entegre sistem.

**Kapsam dışı (v0.1):** Eskrim, dağcılık, masa tenisi branşları; kapı/ışık donanım entegrasyonu; Logo/Netsis gibi muhasebe ERP bağlantıları (Excel export yeterli).

---

## 2. Paydaşlar ve personas

| Persona | İhtiyaç |
|---------|---------|
| **Üye** | 72 saat içinde slot arama, rezervasyon (haftada en fazla 3 aktif), misafir ekleme, online ödeme, iptal, geçmiş |
| **Misafir** | Rezervasyon açamaz; yalnızca üyenin davetiyle oyunda yer alır |
| **Resepsiyon** | Takvim görüntüleme, kasa/oda tahsilat kaydı, üye arama, acil admin rezervasyonu (yetkili) |
| **Saha personeli** | Mobil: günlük kort listesi, akşam temizlik checklist |
| **Akademi sorumlusu** | (Kısıtlı admin) Dönemsel akademi blokları girme/güncelleme |
| **Kış sporu sorumlusu** | (Kısıtlı admin) Dönemsel dedike bloklar |
| **Süper admin / yönetim** | Kort, mevsim modu, tarife, turnuva, fix sözleşme, import, override |
| **Muhasebe** | Excel export, fix ödemeleri, online tahsilat mutabakatı |

---

## 3. Kort envanteri ve adlandırma

Sistemde kortlar **grup + numara** ile benzersiz tanımlanır (aynı numara farklı grupta olabilir).

| Grup | Kod | Numaralar | Kiralanabilir |
|------|-----|-----------|---------------|
| Balon | `BALON` | 1–9 | Evet |
| Kapalı | `KAPALI` | 1–3 | Evet |
| Merkez | `MERKEZ` | 1 (tek kort) | Evet |
| Fitness | `FITNESS` | 1 | **Hayır** — takvimde görünür, rezervasyon kapalı |

**Toplam kiralanabilir tenis kortu:** 9 + 3 + 1 = **13**.  
**Fitness:** operasyonel bilgi; tenis rezervasyon akışına dahil değil.

Merkez kort, balon ve kapalı kortlarla **aynı rezervasyon kurallarına** tabidir (tarife farklı olabilir).

---

## 4. Zaman modeli

- **Slot süresi:** 60 dakika (sabit).
- **Günlük pencere:** 07:00–22:00 (son slot 21:00–22:00).
- **Saat dilimi:** Europe/Istanbul.
- **Mevsim / balon modu:** Sabit takvim yok. Admin, kort (veya grup) bazında **tarih aralığı → mevsim modu** atar (ör. yaz açık, kış balon A/B, kapalı). Geçiş haftaları admin tarafından girilir.
- **Işık ücreti:** Admin tanımlı kurallar (hangi saatten itibaren, hangi kortlarda, ek tutar). Karar ve parametreler tamamen admin panelinde.

---

## 5. Rezervasyon kuralları (iş kuralları)

### 5.1 Kim rezervasyon yapabilir?

- Yalnızca **aktif üye** (sistemde doğrulanmış hesap).
- **Misafir** rezervasyon açamaz; üye rezervasyonuna misafir adı/soyadı (ve isteğe bağlı iletişim) eklenebilir; **misafir sayısında üst limit yok**.
- Kulüp üyesi olmayan üçüncü kişilerin kort kiralaması **yasak** (policy + auth).

### 5.2 İleri rezervasyon (advance booking)

- Üye, slot başlangıcından en fazla **72 saat (3 gün)** sonrasına kadar rezervasyon yapabilir.
- Daha ileri tarihler UI’da seçilemez / API reddeder.

### 5.3 Aktif rezervasyon limiti

- Üye başına **takvim haftası** (Pazartesi 00:00 – Pazar 23:59) içinde en fazla **3 aktif** (gelecek) rezervasyon.
- Tamamlanmış veya iptal edilmiş rezervasyonlar sayılmaz.

### 5.4 İptal

- Slot başlangıcına **2 saatten az** kala yapılan iptaller **cezalı** (ceza tutarı ve tahsil yöntemi admin tarife/ayarlardan; MVP’de ceza bakiyesi veya bir sonraki rezervasyonda tahsil).
- 2 saat ve üzeri kala iptal: ceza yok (iade politikası ödeme sağlayıcı kuralları + admin ayarı ile uyumlu).

### 5.5 Çakışma önleme

- Aynı kort + aynı slot için yalnızca bir onaylı rezervasyon.
- Checkout sırasında kısa süreli **slot hold** (önerilen: 15 dakika) ile eşzamanlı seçim engellenir.

### 5.6 Bloklar (rezervasyona kapalı)

| Blok tipi | Kaynak | Üye rezervasyonu |
|-----------|--------|------------------|
| Akademi | Admin (dönemsel) | Kapalı |
| Kış sporu | Admin (dönemsel) | Kapalı |
| Turnuva / etkinlik | Admin | Kapalı (normal satış yok) |
| Bakım | Admin | Kapalı |
| Fix kort sözleşmesi | Sözleşme kaydı | İlgili slot otomatik kilitli |
| Admin acil | Yetkili admin | Diğer kurallar bypass; **audit log zorunlu** |

Turnuva döneminde kort kiralanması üyelere kapalı; süper admin **override** ile slot açabilir (geçiş dönemi esnekliği); her override loglanır.

### 5.7 Fix (sabit) kort

- Üye **talep** eder (kort, gün, saat, süre/yönetim tarafından tanımlı dönem).
- **Sözleşme imzalandıktan sonra** muhasebe ödemeyi kaydeder; sistemde sözleşme **aktif** olunca ilgili tekrarlayan slotlar kilitlenir.
- Fix kort **fiyatlandırması** normal saatlik rezervasyondan **farklı** tarife seti ile yönetilir.
- Fix slotlarında normal üye rezervasyonu açılmaz.

---

## 6. Fiyatlandırma

### 6.1 Boyutlar

Fiyat, rezervasyon anında hesaplanır ve **snapshot** olarak saklanır (sonraki tarife değişiklikleri geçmiş rezervasyonu etkilemez).

- Kort grubu ve/veya tekil kort kimliği (balonlar arası fark desteklenir).
- Mevsim modu (yaz/kış, kapalı/balon varyantları).
- Saat bandı (peak / off-peak — admin tanımlı).
- Işık (admin kuralına göre slot ışıklı sayılıyorsa ek ücret).
- Rezervasyon tipi: **normal** | **fix** (fix aylık/sözleşme; slot başı değil).

### 6.2 Ödeme kanalları

| Kanal | Açıklama |
|-------|----------|
| **Online** | Kart / yerel ödeme sağlayıcı (iyzico veya PayTR — implementasyon aşamasında seçim) |
| **Resepsiyon / oda** | Personel manuel “tahsil edildi” kaydı; rezervasyon onayı ödeme durumuna bağlanabilir |

Hedef: üye rezervasyonlarında **online ödeme** birincil yol. Fix sözleşmelerde muhasebe onaylı kayıt.

### 6.3 Muhasebe

- v0.1: **Excel export** (tarih aralığı, kort, üye, tutar, kanal, rezervasyon id).
- ERP entegrasyonu yok.

---

## 7. Operasyon

### 7.1 Temizlik

- Rezervasyon **sonrası** otomatik görev **yok**.
- **Her akşam** toplu temizlik listesi: o gün kullanılmış / açık kortlar; saha personeli mobil arayüzden tamamlandı işaretler.

### 7.2 Resepsiyon ve acil durum

- Admin/resespsiyon yetkisi: acil rezervasyon oluşturma, slot kapatma, turnuva override.
- Tüm manuel müdahaleler **audit log**: kim, ne zaman, eski/yeni durum, gerekçe (kısa metin).

---

## 8. Mini CRM ve kimlik

### 8.1 Üye kaydı

Minimum alanlar:

- Ad, soyad  
- Telefon, e-posta  
- Üyelik numarası (kulüp)  
- Durum: aktif / pasif / askıda  
- Not (iç kullanım)

İsteğe bağlı: doğum tarihi (gelecekte junior kuralları için).

### 8.2 Import

- **CSV/Excel şablon** ile toplu import.
- Hata raporu: satır numarası, neden.
- Duplicate stratejisi: üyelik no veya telefon eşleşmesi → güncelle veya atla (admin seçimi).

### 8.3 Kimlik doğrulama

- E-posta + şifre veya e-posta/SMS OTP (implementasyon kararı IMPLEMENTATION.md’de).
- Pasif üye giriş yapabilir ancak **yeni rezervasyon açamaz**.

---

## 9. Fonksiyonel gereksinimler (özet)

### 9.1 Üye

- [ ] Giriş / şifre sıfırlama  
- [ ] Kort grubu filtresi, 72 saat penceresinde müsait slot listesi  
- [ ] Rezervasyon oluşturma, misafir ekleme  
- [ ] Online ödeme  
- [ ] Haftalık 3 aktif limit kontrolü  
- [ ] İptal (2 saat kuralı + ceza gösterimi)  
- [ ] Fix kort talebi (form → yönetim onay/sözleşme akışı)  
- [ ] Rezervasyon geçmişi  

### 9.2 Admin

- [ ] Kort CRUD (grup, numara, kiralanabilirlik, metadata)  
- [ ] Mevsim modu takvimi (kort/grup × tarih aralığı)  
- [ ] Blok: akademi, kış sporu, turnuva, bakım  
- [ ] Tarife setleri ve kural satırları (ışık dahil)  
- [ ] Fix sözleşme yaşam döngüsü (talep → imzalı → aktif → bitiş)  
- [ ] Üye CRM + import  
- [ ] Acil rezervasyon / override + audit  
- [ ] Excel rapor export  

### 9.3 Operasyon

- [ ] Günlük akşam temizlik listesi + tamamlama  
- [ ] Resepsiyon: manuel tahsilat, üye arama  

### 9.4 Sistem

- [ ] Rol tabanlı yetki (üye, resepsiyon, saha, akademi admin, süper admin, muhasebe read-only)  
- [ ] Tek organizasyon (`organization_id` sabit veya tek satır; şema genişletilebilir)  
- [ ] Türkçe arayüz metinleri  

---

## 10. Kullanıcı hikayeleri (seçilmiş)

**US-01 — Normal rezervasyon**  
Üye olarak, önümüzdeki 3 gün içinde müsait bir balon kortu seçip misafirlerimi ekleyerek online ödeyebilmek istiyorum; böylece telefon/resepsiyon kuyruğuna gerek kalmaz.

*Kabul:* 72 saat dışı slot seçilemez; ödeme sonrası onay; haftalık 3 limit aşılırsa hata mesajı (TR).

**US-02 — Akademi bloku**  
Akademi sorumlusu olarak, dönem değişince belirli kortlarda Salı 16:00–18:00 aralığını akademi bloku yapmak istiyorum; üyeler bu slotları göremez veya “dolu” görür.

*Kabul:* Blok sonrası üye rezervasyon API 409; mevcut rezervasyon yoksa (veya admin taşımışsa) tutarlı takvim.

**US-03 — Geç iptal cezası**  
Üye olarak, maçtan 1 saat önce iptal edersem ceza tutarını görmek ve onaylamak istiyorum.

*Kabul:* `< 2 saat` → ceza hesaplanır; audit; iade kısmi veya ceza bakiyesi policy’ye uygun.

**US-04 — Fix kort**  
Üye olarak fix kort talebi göndermek; sözleşme imzalandıktan sonra muhasebenin ödemeyi işaretlemesiyle her hafta aynı slotun otomatik ayrılmasını istiyorum.

*Kabul:* Sözleşme `active` olunca recurring lock; normal booking engelli.

**US-05 — Turnuva**  
Admin olarak turnuva hafta sonu 1–9 balon kortlarını kapatmak; gerekirse tek slot için override satmak istiyorum.

*Kabul:* Blok aralığı; override audit’te; üye self-servis o slotta book edemez (override hariç).

**US-06 — Akşam temizlik**  
Saha personeli olarak bugün oynanan kortların listesini akşam telefondan görüp temizlik bitince işaretlemek istiyorum.

*Kabul:* Gün sonu batch; tamamlanmayan kort yönetim dashboard’unda görünür.

**US-07 — Muhasebe export**  
Muhasebe olarak tarih aralığı seçip tüm tahsilatları Excel indirmek istiyorum.

*Kabul:* Kolonlar: tarih, rezervasyon id, üye, kort, tutar, kanal, iptal/ceza flag.

---

## 11. Kural matrisi (hızlı referans)

| Kural | Değer |
|-------|--------|
| Slot | 60 dk, 07:00–22:00 |
| Advance booking | 72 saat |
| Haftalık aktif rez max | 3 |
| İptal cezası | Son 2 saat içinde |
| Misafir limiti | Yok; sadece üye book eder |
| Non-member kiralama | Yasak |
| Fitness kort | Kiralanamaz |
| Temizlik | Akşam toplu |
| Turnuva satış | Kapalı; admin override mümkün |
| Fix ödeme | Sözleşme imza sonrası muhasebe |
| Export | Excel |

---

## 12. Başarı metrikleri (TED)

- Çift rezervasyon vakası: **0** (canlıda ölçüm).
- Üye rezervasyonlarının ≥ **%70**’i online self-servis (3 ay hedef).
- Resepsiyon rezervasyon telefon süresinde **ölçülebilir azalma** (kulüp anketi).
- Gün sonu tahsilat mutabakat süresi: **< 30 dk** (muhasebe geri bildirimi).

---

## 13. Riskler ve varsayımlar

| Risk | Azaltma |
|------|---------|
| Tarife karmaşıklığı | Snapshot + admin simülasyon (“bu slot kaç TL?”) |
| Balon geçişi hatalı girilir | Mevsim preview takvimi; çakışan aralık uyarısı |
| Eski Excel üye verisi kirli | Import preview + satır bazlı düzeltme |
| Ödeme sağlayıcı red / 3DS | Net hata mesajı; hold süresi uzatma politikası |

**Varsayım:** ~100+ aktif üye; eşzamanlı kullanımda tek sunucu yeterli MVP için.  
**Varsayım:** Üyeler akıllı telefon kullanır; responsive web MVP, native app zorunlu değil.

---

## 14. Açık kararlar (IMPLEMENTATION öncesi)

1. Ödeme sağlayıcı seçimi (iyzico vs PayTR) ve iptal/iade API davranışı.  
2. Cezalı iptalde tahsil: anında kart çekimi vs kulüp borcu bakiyesi.  
3. Fix talep → sözleşme: kağıt imza dışında dijital onay gerekir mi?  
4. Peak/off-peak saat bantları (TED yönetiminden tarife tablosu).  
5. Resepsiyon manuel rezervasyonda online ödeme atlanınca onay kuralı.  
6. SMS OTP maliyeti vs yalnızca e-posta.

---

## 15. İlgili dokümanlar

Tam indeks: [README.md](./README.md).

| Doküman | İçerik |
|---------|--------|
| [IMPLEMENTATION.md](./IMPLEMENTATION.md) | Mimari, tech stack, DB, API |
| [TASKS.md](./TASKS.md) | Fazlar ve sprint görevleri |
| [BRANDING.md](./BRANDING.md) | Renk, tipografi, marka |
| [PROMPT.md](./PROMPT.md) | Kod aşaması agent talimatı |
| [docs/UI_DESIGN_PRINCIPLES.md](./docs/UI_DESIGN_PRINCIPLES.md) | UI/UX prensipleri |
| [docs/USER_FLOWS.md](./docs/USER_FLOWS.md) | Kullanıcı akışları |
| [docs/GLOSSARY.md](./docs/GLOSSARY.md) | Terim sözlüğü |
| [docs/ROLES_AND_PERMISSIONS.md](./docs/ROLES_AND_PERMISSIONS.md) | RBAC |
| [docs/DATA_DICTIONARY.md](./docs/DATA_DICTIONARY.md) | Veri sözlüğü |
| [docs/NON_FUNCTIONAL_REQUIREMENTS.md](./docs/NON_FUNCTIONAL_REQUIREMENTS.md) | NFR |
| [docs/SECURITY_AND_PRIVACY.md](./docs/SECURITY_AND_PRIVACY.md) | Güvenlik, KVKK |
| [docs/DECISIONS.md](./docs/DECISIONS.md) | Mimari kararlar |
| [DOCUMENTATION_INDEX.md](./DOCUMENTATION_INDEX.md) | Tüm belgeler (~40) |
| [docs/product/FAQ.md](./docs/product/FAQ.md) | SSS |
| [docs/product/TARIFF_APPENDIX_TEMPLATE.md](./docs/product/TARIFF_APPENDIX_TEMPLATE.md) | Tarife tablosu (TED doldurur) |
| [docs/legal/KVKK_AYDINLATMA.md](./docs/legal/KVKK_AYDINLATMA.md) | KVKK taslak |

---

*Belge, ürün beyin fırtınası oturumları (Ekim 2026) ve TED yönetim girdilerine dayanır. Güncellemeler versiyon notu ile bu dosyada tutulur.*
