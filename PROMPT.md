# TED Tenis Ops — Autonomous Implementation Prompt

**Amaç:** Kod aşamasına geçildiğinde coding agent’e tek seferde verilecek özet talimat.  
**Ön koşul:** Tüm belgeler okunmuş olmalı.

---

## Context

TED Spor Kulübü (İstanbul Tarabya) tenis kort rezervasyonu: 13 kiralanabilir kort (Balon 1–9, Kapalı 1–3, Merkez) + 1 fitness (kiralanamaz). Üyeler 72 saat içinde, haftada max 3 aktif rezervasyon; misafir sınırsız ama sadece üye book eder. Fix kort sözleşmeli. Akademi/kış/turnuva blokları. Online + resepsiyon tahsilat. Türkçe UI.

**Repo:** `/Users/bahadiruner/Apps/kortex` (henüz uygulama kodu yok)

---

## Required reading (in order)

1. [SPECIFICATION.md](./SPECIFICATION.md) — iş kuralları  
2. [IMPLEMENTATION.md](./IMPLEMENTATION.md) — stack, schema, servisler  
3. [TASKS.md](./TASKS.md) — Faz 1 sırası  
4. [BRANDING.md](./BRANDING.md) + [docs/UI_DESIGN_PRINCIPLES.md](./docs/UI_DESIGN_PRINCIPLES.md)  
5. [docs/ROLES_AND_PERMISSIONS.md](./docs/ROLES_AND_PERMISSIONS.md)  
6. [docs/USER_FLOWS.md](./docs/USER_FLOWS.md)

---

## Your task

Implement **Faz 1** only:

- Next.js + TypeScript + Tailwind + Prisma + PostgreSQL  
- Seed courts per SPECIFICATION §3  
- Domain: `AvailabilityService`, `BookingService` (mock payment → confirmed)  
- Rules: 72h advance, weekly 3 active, 15min hold, no double booking  
- Member UI: login, date+group, grid, hold→confirm, my bookings  
- Admin: blocks CRUD, manual booking + audit  
- Tests: Vitest for availability + booking concurrency edge cases  

Do **not** implement iyzico, tariff engine, CSV import, fix contracts, evening cleaning cron until Faz 2+ (see TASKS.md backlog).

---

## Constraints

- UI copy Turkish; design tokens from BRANDING.md  
- `Europe/Istanbul` for slot grid  
- All tenant data scoped by `organization_id`  
- Follow UI accessibility notes in UI_DESIGN_PRINCIPLES.md  
- Minimize scope; no unrelated features  

---

## Definition of done (Faz 1)

- [ ] SPECIFICATION §5 rules enforced in API  
- [ ] Admin manual booking writes audit_log  
- [ ] Member cannot book fitness court  
- [ ] README updated with dev setup commands  

---

## After Faz 1

Proceed TASKS.md Faz 2 items only when user explicitly requests.
