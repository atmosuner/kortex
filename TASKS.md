# TED Tenis Ops — Tasks

**Referans:** [SPECIFICATION.md](./SPECIFICATION.md), [IMPLEMENTATION.md](./IMPLEMENTATION.md), [ACCEPTANCE_CRITERIA.md](./docs/product/ACCEPTANCE_CRITERIA.md)

---

## Faz 0 — Dokümantasyon ✅

- [x] SPECIFICATION, IMPLEMENTATION, TASKS, BRANDING, PROMPT
- [x] UI prensipleri, wireframe, component, copy deck
- [x] Product deep docs (availability, pricing, states, errors, edge cases)
- [x] Technical (API, import, export, webhooks, deploy, seed, monitoring)
- [x] Operations runbooks (8)
- [x] Legal taslak, testing, UAT, migration, risk, FAQ, tarife şablonu
- [ ] TED tarife appendix doldurulması (kulüp)
- [ ] Hukuk onaylı KVKK/koşullar

---

## Faz 1 — Takvim doğru (4–6 hafta)

### Sprint 0 — Kurulum
- [ ] Next.js + TS + Tailwind init
- [ ] Docker Postgres / Supabase
- [ ] Prisma schema v1 + migrate
- [ ] Seed org + 14 courts [SEED_DATA.md](./docs/technical/SEED_DATA.md)
- [ ] Timezone + slot generator tests
- [ ] Auth + roles seed users

### Sprint 1 — Availability
- [ ] season_assignments CRUD
- [ ] calendar_blocks CRUD + recurrence basic
- [ ] AvailabilityService + 10 TC-AV tests
- [ ] GET /api/availability

### Sprint 2 — Booking
- [ ] slot_holds + cron expire
- [ ] BookingService hold/confirm (mock pay)
- [ ] Unique (court_id, starts_at)
- [ ] Weekly 3 + 72h enforcement
- [ ] booking_guests

### Sprint 3 — Member UI
- [ ] Login / logout
- [ ] M2 grid [WIREFRAME_SPEC.md](./docs/design/WIREFRAME_SPEC.md)
- [ ] M3 summary + hold timer
- [ ] M6 list + M7 cancel (fee logic stub ok)

### Sprint 4 — Admin minimum
- [ ] Admin layout RBAC
- [ ] A2 blocks UI
- [ ] A3 manual booking + audit
- [ ] Members read-only list

### Sprint 5 — Hardening
- [ ] Cancel 2h penalty logic
- [ ] Ops O1 stub (manual generate)
- [ ] E2E TC-E2E-001
- [ ] staging deploy [DEPLOYMENT.md](./docs/technical/DEPLOYMENT.md)

**Faz 1 Done:** [DEFINITION_OF_DONE.md](./docs/acceptance/DEFINITION_OF_DONE.md)

---

## Faz 2 — Para (3–4 hafta)

- [ ] Tariff CRUD + PricingService
- [ ] price_snapshot on confirm
- [ ] Admin A5 tariff + simulate
- [ ] iyzico init + webhook [WEBHOOKS_PAYMENT.md](./docs/technical/WEBHOOKS_PAYMENT.md)
- [ ] M4 payment redirect flow
- [ ] Reception payment UI
- [ ] Cancellation fee collection policy
- [ ] TC-PR, TC-PY tests
- [ ] TED tarife import from appendix

---

## Faz 3 — CRM + fix (3–4 hafta)

- [ ] CSV import wizard [IMPORT_MEMBERS.md](./docs/technical/IMPORT_MEMBERS.md)
- [ ] Invite email N6
- [ ] Fix request M8 + admin workflow [FIX_COURT_PROCESS.md](./docs/operations/FIX_COURT_PROCESS.md)
- [ ] Fixed contract → availability lock
- [ ] Excel export [EXPORT_ACCOUNTING.md](./docs/technical/EXPORT_ACCOUNTING.md)
- [ ] accounting role UI A8

---

## Faz 4 — Ops + polish (2–3 hafta)

- [ ] Evening cleaning cron + field O1
- [ ] academy_admin / winter_admin scoped UI
- [ ] Notifications N1–N7 email
- [ ] Dashboard widgets [REPORTING.md](./docs/product/REPORTING.md)
- [ ] UAT full [UAT_CHECKLIST.md](./docs/acceptance/UAT_CHECKLIST.md)
- [ ] Prod go-live [MIGRATION_FROM_EXCEL.md](./docs/legacy/MIGRATION_FROM_EXCEL.md)

---

## Faz 5 — Backlog (opsiyonel)

- [ ] PWA push
- [ ] SMS OTP
- [ ] No-show tracking
- [ ] Booking transfer between members
- [ ] ICS calendar export
- [ ] Dark mode
- [ ] Native app wrapper

---

## Bağımlılık grafi (özet)

```text
Faz0 doc → Faz1 core → Faz2 payment → Faz3 CRM/fix → Faz4 ops
                ↘ staging pilot ↗
```

---

*İlk kod: Sprint 0. Dokümantasyon tamam — onay sonrası PROMPT.md.*
