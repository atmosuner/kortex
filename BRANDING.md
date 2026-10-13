# Kortex / TED Tenis Ops — Branding Guide

**Not:** Bu uygulama TED Spor Kulübü tenis operasyonu içindir. Resmi TED logosu ve marka kılavuzu kulüpten ayrı onay gerektirir; aşağıdaki palet **tenis + kulüp geleneği** ile uyumlu **iç ürün** önerisidir.

**Referans:** [UI_DESIGN_PRINCIPLES.md](./docs/UI_DESIGN_PRINCIPLES.md)

---

## 1. Ad ve kimlik

### 1.1 Proje adları

| Bağlam | Ad |
|--------|-----|
| Kod / repo | `kortex` |
| İç ürün | **TED Tenis Ops** veya **TED Kort Rezervasyon** |
| Üye-facing (öneri) | **TED Tenis** — alt başlık: “Kort rezervasyonu” |

### 1.2 Tagline

- **Birincil:** “Kortunuz birkaç dokunuş uzağınızda.”
- **Operasyon:** “Tek takvim, net tahsilat.”

### 1.3 Elevator pitch

TED tenis üyeleri kortlarını telefonlarından rezerve eder ve güvenle öder. Kulüp personeli aynı sistemde akademi, turnuva ve fix kortları yönetir; muhasebe Excel’e değil, tek kaynağa güvenir.

---

## 2. Logo (konsept — uygulama aşamasında üretim)

### 2.1 Konsept

Stilize **kort çizgisi** + **T** harfi birleşimi; veya sadece wordmark “TED Tenis”. Favicon: yeşil zemin üzerinde beyaz top izi veya minimal kort köşesi.

### 2.2 Kullanım

- Üye PWA: icon mark
- Admin: wordmark + “Yönetim” etiketi
- TED resmi logosu varsa header’da **kulüp logosu + uygulama adı** yan yana (yönetim onayı ile)

### 2.3 AI logo prompt (taslak)

> Flat minimal logo icon, tennis court top-down lines forming letter T, deep forest green #1B4332 and white, no gradient, no text, square 1:1, professional sports club, timeless not trendy.

---

## 3. Renk paleti

### 3.1 Marka renkleri

| Rol | Ad | Hex | Kullanım |
|-----|-----|-----|----------|
| Primary | Kort yeşili | `#1B4332` | Birincil buton, header, link |
| Primary hover | | `#2D6A4F` | Hover |
| Secondary | Kulüp lacivert | `#1D3557` | Admin sidebar, sekme |
| Accent | Top sarısı | `#F4D03F` | Vurgu, aktif sekme (ölçülü) |
| Clay (opsiyonel) | Kiremit | `#BC4749` | Turnuva badge, dikkat |

### 3.2 Nötrler

| Rol | Hex | Kullanım |
|-----|-----|----------|
| Text primary | `#212529` | Gövde, başlık |
| Text secondary | `#6C757D` | Alt metin, placeholder |
| Background | `#F8F9FA` | Sayfa |
| Surface | `#FFFFFF` | Kart, panel |
| Border | `#DEE2E6` | Çizgi, input |

### 3.3 Semantik (UI durum)

| Rol | Hex | Kullanım |
|-----|-----|----------|
| Success | `#198754` | Onay, müsait (alternatif açık zemin `#D1E7DD`) |
| Error | `#DC3545` | Hata, iptal cezası |
| Warning | `#FFC107` | Son 2 saat uyarısı |
| Info | `#0DCAF0` | Bilgi banner |

### 3.4 Grid slot renkleri (açık tema)

| Durum | Arka plan | Border / metin |
|-------|-----------|----------------|
| Müsait | `#FFFFFF` | `#1B4332` seçimde |
| Dolu | `#E9ECEF` | `#6C757D` |
| Blok | `#FFF3CD` | `#856404` etiket |
| Seçili | `#D1E7DD` | `#1B4332` |

### 3.5 CSS değişkenleri (referans)

```css
:root {
  --color-primary: #1b4332;
  --color-primary-hover: #2d6a4f;
  --color-secondary: #1d3557;
  --color-accent: #f4d03f;
  --color-bg: #f8f9fa;
  --color-surface: #ffffff;
  --color-text: #212529;
  --color-text-muted: #6c757d;
  --color-border: #dee2e6;
  --color-success: #198754;
  --color-error: #dc3545;
  --color-warning: #ffc107;
  --radius-sm: 6px;
  --radius-md: 10px;
  --shadow-card: 0 1px 3px rgb(0 0 0 / 8%);
}
```

### 3.6 Dark mode (Faz 2)

- Background `#121212`, surface `#1E1E1E`, primary `#40916C`
- Grid kontrastları yeniden test (AA)

---

## 4. Tipografi

| Rol | Font (öneri) | Yedek |
|-----|--------------|-------|
| UI / gövde | **DM Sans** | system-ui, sans-serif |
| Rakamlar / grid | DM Sans `font-variant-numeric: tabular-nums` | |
| Alternatif (daha kurumsal) | **Source Sans 3** | |

- H1: 1.75rem / 700  
- H2: 1.375rem / 600  
- Body: 1rem / 400  
- Caption: 0.875rem  

Google Fonts lisansı uygun; offline kulüp ağı için self-host planlanabilir.

---

## 5. İkonografi

- **Lucide** veya **Heroicons** — stroke 1.5–2px, köşe yuvarlak
- Anlam: kort (grid), takvim, kullanıcı, misafir (+), kilit, uyarı üçgeni, dosya (export)

---

## 6. Layout ve bileşen stili

- **Köşe:** `--radius-md` kartlarda; grid hücre `--radius-sm`
- **Gölge:** hafif; floating panel admin filtrelerinde
- **Yoğunluk:** üye airy; admin compact toggle
- **Fotoğraf:** stock tenis görseli hero’da zorunlu değil; üye app direkt grid

---

## 7. Ses ve görsel uyum

Metin tonu [UI_DESIGN_PRINCIPLES.md](./docs/UI_DESIGN_PRINCIPLES.md) §7 ile aynı: resmi **siz**, kısa cümleler.

---

## 8. Örnek ekran hiyerarşisi (üye header)

```
[ TED Tenis ]                    [ Profil ]
──────────────────────────────────────────
  Balon | Kapalı | Merkez
  ◀ 12 Eki Cum ▶
┌─────────────────────────────────────┐
│  Kort grid …                        │
└─────────────────────────────────────┘
```

---

## 9. Marka yasakları

- Playtomic / generic neon mor-mavi palet
- Agresif kırmızı birincil buton (destructive hariç)
- ALL CAPS navigasyon
- Ödeme ekranında üçüncü parti markadan büyük logo

---

*Resmi TED marka materyalleri kulüpten temin edildiğinde §2–3 güncellenir.*
