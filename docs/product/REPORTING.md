# Raporlama Gereksinimleri

**Versiyon:** 1.0

---

## 1. Dashboard (super_admin)

| Widget | Metrik |
|--------|--------|
| Bugün doluluk | confirmed slots / available slots |
| Hafta gelir | sum payments completed |
| Aktif üye rez | count distinct members |
| Temizlik | pending items tonight |
| Fix talepleri | count requested |

---

## 2. Operasyonel raporlar

| Rapor | Filtre | Çıktı |
|-------|--------|-------|
| Doluluk kort | date range, group | CSV |
| Doluluk saat | heatmap data | JSON |
| No-show | booking completed without check-in Faz 5 | — |
| Blok özeti | block_type | list |

---

## 3. Finans (muhasebe)

[EXPORT_ACCOUNTING.md](../technical/EXPORT_ACCOUNTING.md) — birincil.

Ek: günlük kanal breakdown online vs reception vs room.

---

## 4. Audit raporu

Override count, manual booking by staff, tariff changes.

---

## 5. Periyot

- Günlük: resepsiyon skim dashboard  
- Haftalık: yönetim doluluk  
- Aylık: muhasebe export archive  

---

## 6. Gizlilik

Raporlarda misafir adı optional mask (Rapor tipine göre).

---

*Kabul metrikleri SPEC §12.*
