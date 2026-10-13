# TED Tenis Ops — Roles & Permissions

**Referans:** [SPECIFICATION.md](../SPECIFICATION.md) §2, [IMPLEMENTATION.md](../IMPLEMENTATION.md) §5  
**Versiyon:** 0.1

---

## 1. Rol listesi

| Rol | Kod | Açıklama |
|-----|-----|----------|
| Üye | `member` | Self-servis rezervasyon |
| Resepsiyon | `reception` | Takvim, manuel rez, kasa |
| Saha | `field` | Akşam temizlik |
| Akademi admin | `academy_admin` | Akademi blokları |
| Kış sporu admin | `winter_admin` | Kış sporu blokları |
| Muhasebe | `accounting` | Read + Excel export |
| Süper admin | `super_admin` | Tam yetki |

Bir kullanıcı **tek rol** (MVP); çoklu rol Faz 2.

---

## 2. Yetki matrisi

| Kaynak / eylem | member | reception | field | academy_admin | winter_admin | accounting | super_admin |
|----------------|--------|-----------|-------|---------------|--------------|------------|-------------|
| Kendi rezervasyonu oluştur | ✓ | — | — | — | — | — | ✓ |
| Kendi rezervasyonu iptal | ✓ | — | — | — | — | — | ✓ |
| Tüm rezervasyonları gör | — | ✓ | — | — | — | ✓ | ✓ |
| Manuel rezervasyon | — | ✓* | — | — | — | — | ✓ |
| Override (turnuva slot sat) | — | — | — | — | — | — | ✓ |
| Blok: akademi | — | — | — | ✓ | — | — | ✓ |
| Blok: kış sporu | — | — | — | — | ✓ | — | ✓ |
| Blok: turnuva/bakım | — | — | — | — | — | — | ✓ |
| Kort / mevsim CRUD | — | — | — | — | — | — | ✓ |
| Tarife CRUD | — | — | — | — | — | — | ✓ |
| Üye CRM + import | — | read | — | — | — | read | ✓ |
| Fix sözleşme | — | — | — | — | — | update pay | ✓ |
| Resepsiyon tahsilat kaydı | — | ✓ | — | — | — | — | ✓ |
| Excel export | — | — | — | — | — | ✓ | ✓ |
| Akşam temizlik | — | — | ✓ | — | — | — | ✓ |
| Audit log görüntüle | — | — | — | — | — | — | ✓ |

\* Resepsiyon manuel rez: **gerekçe zorunlu**; haftalık 3 / 72s bypass **kapalı** (super_admin açabilir) — IMPLEMENTATION default.

---

## 3. Üye durumu

| Durum | Giriş | Yeni rezervasyon |
|-------|-------|------------------|
| active | ✓ | ✓ |
| suspended | ✓ | ✗ |
| passive | ✓ | ✗ |

---

## 4. Policy kuralları (authz middleware)

1. `member` → `/app/*`  
2. `reception` → `/app/*` read + `/admin/bookings/manual`, `/admin/members` read  
3. `field` → `/ops/*` only  
4. `academy_admin` → `/admin/blocks?type=academy`  
5. `winter_admin` → `/admin/blocks?type=winter`  
6. `accounting` → `/admin/reports`, payments read  
7. `super_admin` → `/admin/*`  

---

## 5. Audit zorunlu eylemler

- Manuel rezervasyon / iptal (staff)
- Turnuva override satış
- Tarife değişikliği
- Fix sözleşme durum geçişi
- Üye pasife alma

---

## 6. Oturum

- Üye: 30 gün refresh (cihaz hatırla) — ayarlanabilir  
- Staff: 8 saat idle logout önerisi  
- MFA: super_admin için Faz 2 önerilir  

---

*Detay implementasyon: [IMPLEMENTATION.md](../IMPLEMENTATION.md).*
