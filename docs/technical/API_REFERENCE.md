# API Reference

**Versiyon:** 1.0 (taslak OpenAPI)  
**Base URL:** `https://tenis.tedclub.org.tr` (prod placeholder)  
**Auth:** Session cookie `ted_session` veya `Authorization: Bearer` (Faz 2 mobile)

Tüm zamanlar ISO 8601 offset ile; slot mantığı Europe/Istanbul.

---

## 1. Genel

### 1.1 Envelope (başarı)

```json
{
  "ok": true,
  "data": { }
}
```

### 1.2 Pagination

```json
{
  "ok": true,
  "data": { "items": [], "next_cursor": "opaque" }
}
```

Query: `limit` (max 100), `cursor`

---

## 2. Auth

### POST /api/auth/login

Body:

```json
{ "email": "uye@ornek.com", "password": "..." }
```

Response: session set-cookie, `{ "user": { "id", "role", "member_id" } }`

### POST /api/auth/logout

### POST /api/auth/forgot-password

### POST /api/auth/reset-password

---

## 3. Member — Availability

### GET /api/availability

Query:

| Param | Zorunlu | Açıklama |
|-------|---------|----------|
| date | ✓ | YYYY-MM-DD |
| group | ✓ | BALON \| KAPALI \| MERKEZ |

Response:

```json
{
  "ok": true,
  "data": {
    "date": "2026-10-14",
    "group": "BALON",
    "courts": [
      {
        "court_id": "uuid",
        "display_name": "Balon 3",
        "slots": [
          {
            "starts_at": "2026-10-14T14:00:00+03:00",
            "ends_at": "2026-10-14T15:00:00+03:00",
            "status": "AVAILABLE",
            "bookable": true
          }
        ]
      }
    ]
  }
}
```

---

## 4. Member — Booking

### POST /api/bookings/hold

Body:

```json
{
  "court_id": "uuid",
  "starts_at": "2026-10-14T14:00:00+03:00"
}
```

Response:

```json
{
  "ok": true,
  "data": {
    "hold_id": "uuid",
    "expires_at": "2026-10-14T12:15:00+03:00"
  }
}
```

Errors: WEEKLY_LIMIT, SLOT_NOT_AVAILABLE, …

### POST /api/bookings/confirm

Body:

```json
{
  "hold_id": "uuid",
  "guests": [{ "full_name": "Ali Veli", "phone": "+905..." }],
  "payment_method": "online"
}
```

Response (Faz 1 mock):

```json
{
  "ok": true,
  "data": { "booking_id": "uuid", "status": "confirmed" }
}
```

Faz 2 online:

```json
{
  "ok": true,
  "data": {
    "booking_id": "uuid",
    "status": "pending_payment",
    "payment": { "redirect_url": "https://..." }
  }
}
```

### GET /api/bookings/mine

Query: `status`, `from`, `to`

### GET /api/bookings/:id

### POST /api/bookings/:id/cancel

Body (ceza onayı):

```json
{ "acknowledge_fee": true }
```

---

## 5. Member — Fix request

### POST /api/fixed-court/requests

```json
{
  "court_id": "uuid",
  "weekday": 2,
  "start_time": "18:00",
  "notes": "..."
}
```

### GET /api/fixed-court/requests/mine

---

## 6. Pricing (Faz 2)

### GET /api/pricing/preview

Query: `court_id`, `starts_at`

---

## 7. Admin — Blocks

### GET /api/admin/blocks

### POST /api/admin/blocks

```json
{
  "block_type": "academy",
  "title": "Akademi U12",
  "court_id": "uuid",
  "starts_at": "...",
  "ends_at": "...",
  "recurrence": { "freq": "weekly", "until": "2027-06-01" }
}
```

### PATCH /api/admin/blocks/:id

### DELETE /api/admin/blocks/:id

---

## 8. Admin — Bookings manual

### POST /api/admin/bookings/manual

```json
{
  "member_id": "uuid",
  "court_id": "uuid",
  "starts_at": "...",
  "reason": "Acil kulüp talebi - ...",
  "payment_channel": "reception",
  "amount_cents": 50000
}
```

---

## 9. Admin — Courts & season

### GET /api/admin/courts

### PATCH /api/admin/courts/:id

### GET /api/admin/season-assignments

### POST /api/admin/season-assignments

---

## 10. Admin — Tariffs (Faz 2)

CRUD `/api/admin/tariff-sets`, `/api/admin/tariff-rules`  
POST `/api/admin/pricing/simulate`

---

## 11. Admin — Members

### GET /api/admin/members?search=

### PATCH /api/admin/members/:id

### POST /api/admin/members/import

Multipart CSV — bkz. [IMPORT_MEMBERS.md](./IMPORT_MEMBERS.md)

---

## 12. Admin — Fixed contracts (Faz 3)

POST `/api/admin/fixed-contracts`  
PATCH `/api/admin/fixed-contracts/:id` (status, payment)

---

## 13. Admin — Reports

### GET /api/admin/export/excel

Query: `from`, `to`, `channel?`

---

## 14. Admin — Audit

### GET /api/admin/audit-logs?entity_type=&from=

---

## 15. Ops

### GET /api/ops/cleaning/today

### PATCH /api/ops/cleaning/items/:id

```json
{ "completed": true }
```

---

## 16. Webhooks

POST `/api/webhooks/iyzico` — [WEBHOOKS_PAYMENT.md](./WEBHOOKS_PAYMENT.md)

---

## 17. Cron (internal)

POST `/api/cron/expire-holds` — Header `X-Cron-Secret`  
POST `/api/cron/complete-bookings`  
POST `/api/cron/evening-cleaning`  
POST `/api/cron/cancel-stale-pending-payments`

---

## 18. Rate limits

| Route | Limit |
|-------|-------|
| login | 10 / 15 min / IP |
| hold | 30 / hour / member |
| availability | 120 / min / IP |

---

*RBAC: [../ROLES_AND_PERMISSIONS.md](../ROLES_AND_PERMISSIONS.md).*
