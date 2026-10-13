# Risk Kaydı

**Versiyon:** 1.0  
**Review:** aylık pilot, sonra üç ayda bir

| ID | Risk | Olasılık | Etki | Azaltma | Sahip |
|----|------|----------|------|---------|-------|
| R1 | Çift rezervasyon | D | Yüksek | DB unique + transaction | Tech |
| R2 | Yanlış tarife girişi | O | Orta | Simulate + preview | Admin |
| R3 | Balon geçiş hatası | O | Orta | SEASON_TRANSITION checklist | Yönetim |
| R4 | Düşük üye adaptasyonu | O | Orta | Eğitim, paralel dönem kısa | Kulüp |
| R5 | Ödeme webhook gecikmesi | O | Orta | Reconcile job | Tech |
| R6 | KVKK ihlali | D | Yüksek | Hukuk onay, minimizasyon | Kulüp |
| R7 | Personel tek nokta | Y | Orta | 2 super_admin, runbook | Yönetim |
| R8 | Import kirli veri | O | Düşük | Preview import | Admin |
| R9 | Turnuva override kötüye kullanım | D | Orta | Audit + review | Yönetim |
| R10 | Saha app kullanılmaması | O | Düşük | Basit UI, eğitim | Ops |

Olasılık: D düşük O orta Y yüksek

---

*SPEC riskler: [SPECIFICATION.md](../SPECIFICATION.md) §13.*
