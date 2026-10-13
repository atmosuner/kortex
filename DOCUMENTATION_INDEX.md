# Dokümantasyon Tam İndeks

**Proje:** Kortex / TED Tenis Ops  
**Son güncelleme:** 2026-10-12 (doc v0.2)

---

## Kök

| Dosya | Açıklama |
|-------|----------|
| [README.md](./README.md) | Giriş |
| [CHANGELOG.md](./CHANGELOG.md) | Belge değişim günlüğü |
| [SPECIFICATION.md](./SPECIFICATION.md) | Ürün şartnamesi |
| [IMPLEMENTATION.md](./IMPLEMENTATION.md) | Mimari ve teknik plan |
| [TASKS.md](./TASKS.md) | Uygulama görevleri |
| [BRANDING.md](./BRANDING.md) | Marka ve token |
| [PROMPT.md](./PROMPT.md) | Coding agent prompt |

---

## docs/product/

| Dosya | Açıklama |
|-------|----------|
| [AVAILABILITY_RULES.md](./docs/product/AVAILABILITY_RULES.md) | Müsaitlik motoru |
| [PRICING_ENGINE.md](./docs/product/PRICING_ENGINE.md) | Tarife motoru |
| [STATE_MACHINES.md](./docs/product/STATE_MACHINES.md) | Durum makineleri |
| [ERROR_CATALOG.md](./docs/product/ERROR_CATALOG.md) | Hata kodları |
| [ACCEPTANCE_CRITERIA.md](./docs/product/ACCEPTANCE_CRITERIA.md) | Kabul kriterleri |
| [EDGE_CASES.md](./docs/product/EDGE_CASES.md) | Kenar durumlar |
| [NOTIFICATIONS.md](./docs/product/NOTIFICATIONS.md) | E-posta/SMS |
| [REPORTING.md](./docs/product/REPORTING.md) | Raporlar |
| [FAQ.md](./docs/product/FAQ.md) | SSS |
| [TARIFF_APPENDIX_TEMPLATE.md](./docs/product/TARIFF_APPENDIX_TEMPLATE.md) | TED tarife şablonu |

---

## docs/technical/

| Dosya | Açıklama |
|-------|----------|
| [API_REFERENCE.md](./docs/technical/API_REFERENCE.md) | API |
| [IMPORT_MEMBERS.md](./docs/technical/IMPORT_MEMBERS.md) | CSV import |
| [EXPORT_ACCOUNTING.md](./docs/technical/EXPORT_ACCOUNTING.md) | Excel export |
| [WEBHOOKS_PAYMENT.md](./docs/technical/WEBHOOKS_PAYMENT.md) | iyzico |
| [SEED_DATA.md](./docs/technical/SEED_DATA.md) | Seed |
| [DEPLOYMENT.md](./docs/technical/DEPLOYMENT.md) | Deploy |
| [MONITORING.md](./docs/technical/MONITORING.md) | Log/metric |

---

## docs/operations/

| Dosya | Açıklama |
|-------|----------|
| [ADMIN_RUNBOOK.md](./docs/operations/ADMIN_RUNBOOK.md) | Süper admin |
| [RECEPTION_GUIDE.md](./docs/operations/RECEPTION_GUIDE.md) | Resepsiyon |
| [FIELD_OPS_GUIDE.md](./docs/operations/FIELD_OPS_GUIDE.md) | Saha |
| [ACCOUNTING_GUIDE.md](./docs/operations/ACCOUNTING_GUIDE.md) | Muhasebe |
| [SEASON_TRANSITION.md](./docs/operations/SEASON_TRANSITION.md) | Balon/mevsim |
| [TOURNAMENT_BLOCKS.md](./docs/operations/TOURNAMENT_BLOCKS.md) | Turnuva |
| [FIX_COURT_PROCESS.md](./docs/operations/FIX_COURT_PROCESS.md) | Fix kort |
| [ACADEMY_ADMIN_GUIDE.md](./docs/operations/ACADEMY_ADMIN_GUIDE.md) | Akademi admin |

---

## docs/design/

| Dosya | Açıklama |
|-------|----------|
| [UI_DESIGN_PRINCIPLES.md](./docs/UI_DESIGN_PRINCIPLES.md) | UX/UI prensipleri |
| [WIREFRAME_SPEC.md](./docs/design/WIREFRAME_SPEC.md) | Ekran wireframe |
| [COMPONENT_SPEC.md](./docs/design/COMPONENT_SPEC.md) | Bileşenler |
| [COPY_DECK.md](./docs/design/COPY_DECK.md) | Metinler |

---

## docs/legal/

| Dosya | Açıklama |
|-------|----------|
| [KVKK_AYDINLATMA.md](./docs/legal/KVKK_AYDINLATMA.md) | Aydınlatma (taslak) |
| [KVKK_ACIK_RIZA.md](./docs/legal/KVKK_ACIK_RIZA.md) | Pazarlama rızası |
| [TERMS_OF_USE.md](./docs/legal/TERMS_OF_USE.md) | Kullanım koşulları |

---

## docs/testing/ & acceptance/

| Dosya | Açıklama |
|-------|----------|
| [TESTING.md](./docs/TESTING.md) | Test stratejisi |
| [TEST_CASES.md](./docs/testing/TEST_CASES.md) | Test case kataloğu |
| [UAT_CHECKLIST.md](./docs/acceptance/UAT_CHECKLIST.md) | Pilot UAT |
| [DEFINITION_OF_DONE.md](./docs/acceptance/DEFINITION_OF_DONE.md) | DoD |

---

## docs/ — çapraz

| Dosya | Açıklama |
|-------|----------|
| [USER_FLOWS.md](./docs/USER_FLOWS.md) | Akışlar |
| [GLOSSARY.md](./docs/GLOSSARY.md) | Sözlük |
| [ROLES_AND_PERMISSIONS.md](./docs/ROLES_AND_PERMISSIONS.md) | RBAC |
| [DATA_DICTIONARY.md](./docs/DATA_DICTIONARY.md) | Veri sözlüğü |
| [NON_FUNCTIONAL_REQUIREMENTS.md](./docs/NON_FUNCTIONAL_REQUIREMENTS.md) | NFR |
| [SECURITY_AND_PRIVACY.md](./docs/SECURITY_AND_PRIVACY.md) | Güvenlik |
| [DECISIONS.md](./docs/DECISIONS.md) | ADR |
| [RISK_REGISTER.md](./docs/RISK_REGISTER.md) | Riskler |

---

## docs/legacy/

| Dosya | Açıklama |
|-------|----------|
| [MIGRATION_FROM_EXCEL.md](./docs/legacy/MIGRATION_FROM_EXCEL.md) | Geçiş planı |

---

## Okuma yolları

**Yönetim:** SPEC → FAQ → RISK → UAT  
**Resepsiyon:** RECEPTION_GUIDE → USER_FLOWS → FAQ  
**Geliştirici:** IMPLEMENTATION → API → AVAILABILITY → PRICING → TASKS → PROMPT  
**Tasarım:** UI_PRINCIPLES → BRANDING → WIREFRAME → COMPONENT → COPY  
**Hukuk:** KVKK → TERMS → SECURITY  

---

*Toplam ~40 belge; kod başlamadan implementasyon için yeterli derinlik hedeflendi.*
