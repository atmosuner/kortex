# Kortex — Tenis Ops

Tenis kort **rezervasyonu**, **tahsilat** ve **operasyon** sistemi.

**Durum:** Dokümantasyon v0.2 tamamlandı — **henüz uygulama kodu yok.**

---

## Hızlı başlangıç

| Kim | İlk okuma |
|-----|-----------|
| Yönetim / ürün | [SPECIFICATION.md](./SPECIFICATION.md) |
| Geliştirici (ileride) | [IMPLEMENTATION.md](./IMPLEMENTATION.md) → [PROMPT.md](./PROMPT.md) |
| Tasarım | [docs/UI_DESIGN_PRINCIPLES.md](./docs/UI_DESIGN_PRINCIPLES.md) → [BRANDING.md](./BRANDING.md) |
| Resepsiyon / saha | [docs/operations/RECEPTION_GUIDE.md](./docs/operations/RECEPTION_GUIDE.md) |
| Tüm dosyalar | **[DOCUMENTATION_INDEX.md](./DOCUMENTATION_INDEX.md)** |

---

## Ürün özeti

- **13** tenis kortu (Balon 1–9, Kapalı 1–3, Merkez) + fitness (kiralanamaz)
- Üye: **72 saat** advance, haftada **3** aktif rez, misafir sınırsız (yalnızca üye açar)
- Fix kort, akademi/kış/turnuva blokları, mevsim/balon admin takvimi
- Online ödeme + resepsiyon/oda; muhasebe **Excel export**
- Dil: **Türkçe**

---

## Belge ağacı (özet)

```text
kortex/
├── SPECIFICATION.md          # Ne
├── IMPLEMENTATION.md         # Nasıl
├── TASKS.md                  # İş listesi
├── BRANDING.md               # Görsel kimlik
├── PROMPT.md                 # Agent talimatı
├── DOCUMENTATION_INDEX.md    # Tam indeks
├── CHANGELOG.md
└── docs/
    ├── product/              # Kurallar, fiyat, hatalar, FAQ, tarife şablonu
    ├── technical/            # API, deploy, import/export, ödeme
    ├── operations/           # Runbook'lar (8 kılavuz)
    ├── design/               # Wireframe, bileşen, copy deck
    ├── legal/                # KVKK, koşullar (taslak)
    ├── testing/              # Test case'ler
    ├── acceptance/           # UAT, DoD
    └── legacy/               # Excel geçişi
```

---

## Versiyon

| Bileşen | Versiyon |
|---------|----------|
| Ürün spec | 0.1 |
| Dokümantasyon paketi | 0.2 |
| Kod | — |

Değişiklikler: [CHANGELOG.md](./CHANGELOG.md).

---

## Sonraki adım (kod dışı)

1. [TARIFF_APPENDIX_TEMPLATE.md](./docs/product/TARIFF_APPENDIX_TEMPLATE.md) — Tarife doldur  
2. Legal taslaklar — kulüp hukuk onayı  
3. Resmi logo kullanım onayı — [BRANDING.md](./BRANDING.md)

Kod aşaması: kullanıcı “başla” dediğinde [PROMPT.md](./PROMPT.md) + [TASKS.md](./TASKS.md) Faz 1.
