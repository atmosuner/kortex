# TED Tenis Ops — Sözlük

Arayüz ve dokümantasyonda **terim tutarlılığı** için. Üye arayüzünde Türkçe kolon kullanılır.

| Terim (TR) | EN (kod) | Açıklama |
|------------|----------|----------|
| Rezervasyon | booking | Onaylı veya ödeme bekleyen kort kullanım hakkı |
| Saat dilimi | slot | 60 dk; örn. 14:00–15:00 |
| Hold / Bekletme | slot_hold | Ödeme öncesi 15 dk geçici kilitleme |
| Kort grubu | court_group | BALON, KAPALI, MERKEZ, FITNESS |
| Fix kort | fixed_court | Belirli gün/saat tekrarlayan sözleşmeli kort |
| Blok | calendar_block | Akademi, kış, turnuva, bakım — rezervasyona kapalı |
| Mevsim modu | season_mode | Yaz açık, kış balon vb.; fiyat ve etiket |
| Misafir | guest | Üye olmayan oyuncu; rezervasyonu üye açar |
| Üye | member | Aktif kulüp üyeliği + hesap |
| Tarife | tariff | Fiyat kural seti |
| Fiyat snapshot | price_snapshot | Rezervasyon anındaki dondurulmuş tutar |
| Işık ek ücreti | light_surcharge | Admin saat/kort kuralına göre |
| Override | admin_override | Turnuva vb. normal kural bypass; audit zorunlu |
| Aktif rezervasyon | active_booking | Gelecek, iptal edilmemiş, confirmed |
| Takvim haftası | calendar_week | Pazartesi–Pazar (limit hesabı) |
| Advance booking | — | En fazla 72 saat ileri |
| İptal cezası | cancellation_fee | Son 2 saat içinde iptal |
| Akşam temizlik | evening_cleaning | Günlük toplu ops görevi |
| Resepsiyon tahsilatı | reception_payment | Manuel kasa/oda kaydı |
| Audit kaydı | audit_log | Kim, ne, ne zaman, gerekçe |

**Kort adlandırma UI:** “Balon 3”, “Kapalı 2”, “Merkez Kort”.

---

## Ek terimler

| Terim | Açıklama |
|-------|----------|
| Hold | Ödeme öncesi geçici slot kilidi (15 dk) |
| Snapshot | Rezervasyon anı fiyat dondurması |
| Override | Turnuva vb. admin istisna satış |
| Pilot | Staging paralel Excel dönemi |
| Channel | online / reception / room |
| Season assignment | Kort × tarih aralığı × mevsim modu |
| Tariff set | Dönemsel fiyat kural paketi |
| Priority (tariff) | Küçük numara önce eşleşir |
| Pending payment | Ödeme bekleyen rezervasyon |
| Cleaning run | Günlük akşam temizlik batch |
| organization_id | Tenant kolonu (TED tek satır) |
| Advance window | 72 saat ileri limit |
| Calendar week | Pazartesi–Pazar limit hesabı |

---

## Kısaltmalar

| Kısaltma | Anlam |
|----------|-------|
| UAT | Kullanıcı kabul testi |
| NFR | Fonksiyonel olmayan gereksinim |
| ADR | Mimari karar kaydı |
| RBAC | Rol tabanlı erişim |
| KVKK | 6698 kişisel veri kanunu |
| PCI | Ödeme kartı güvenlik standardı |
| PWA | Progressive web app |
| API | Uygulama programlama arayüzü |

---

*SSS: [product/FAQ.md](./product/FAQ.md).*
