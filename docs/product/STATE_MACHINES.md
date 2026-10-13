# Durum Makineleri (State Machines)

**Versiyon:** 1.0

---

## 1. Booking

```mermaid
stateDiagram-v2
  [*] --> pending_payment: confirm initiated (online)
  [*] --> confirmed: reception cash / admin manual paid
  pending_payment --> confirmed: payment success
  pending_payment --> cancelled: payment fail / timeout / user abort
  confirmed --> cancelled: member/admin cancel
  confirmed --> completed: ends_at passed (cron)
  cancelled --> [*]
  completed --> [*]
```

### Geçiş kuralları

| From | To | Tetikleyici | Koşul |
|------|-----|-------------|-------|
| — | pending_payment | Üye ödemeye geç | hold valid |
| — | confirmed | Resepsiyon kayıt | reason if manual |
| pending_payment | confirmed | Webhook OK | amount = snapshot |
| pending_payment | cancelled | 15 dk timeout job | |
| confirmed | cancelled | İptal API | ceza hesap |
| confirmed | completed | Cron hourly | now > ends_at |

**pending_payment** slot’u bloklar (BOOKED sayılır availability’de).

---

## 2. Slot hold

```mermaid
stateDiagram-v2
  [*] --> active: POST hold
  active --> expired: now > expires_at
  active --> consumed: confirm success
  active --> released: user cancel checkout
  expired --> [*]
  consumed --> [*]
  released --> [*]
```

TTL: 15 dakika (org setting `hold_minutes`).

---

## 3. Payment

```mermaid
stateDiagram-v2
  [*] --> pending
  pending --> completed: provider success
  pending --> failed: provider fail
  completed --> refunded: partial/full refund
  failed --> [*]
  refunded --> [*]
```

Manuel kanal: doğrudan `completed` + `recorded_by_user_id`.

---

## 4. Fixed court contract

```mermaid
stateDiagram-v2
  [*] --> requested: üye talep
  requested --> contract_signed: admin imza tarihi
  contract_signed --> active: muhasebe paid + admin activate
  requested --> cancelled: red
  contract_signed --> cancelled: ödeme gelmedi
  active --> ended: active_to geçti
  active --> cancelled: erken fesih
  ended --> [*]
  cancelled --> [*]
```

**active** → availability FIX lock.

---

## 5. Member status

```mermaid
stateDiagram-v2
  [*] --> active
  active --> suspended: admin
  active --> passive: admin / import
  suspended --> active: admin
  passive --> active: admin + yenileme
```

---

## 6. Evening cleaning item

```mermaid
stateDiagram-v2
  [*] --> pending: cron generate
  pending --> completed: field staff toggle
  completed --> [*]
```

---

## 7. Calendar block

Statik — zaman aralığı; “durum” yok. **Soft delete** `deleted_at` (audit).

---

## 8. İptal ceza alt durumu (booking meta)

| cancellation_fee_status | Açıklama |
|-------------------------|----------|
| none | Erken iptal |
| assessed | Ceza hesaplandı |
| collected | Tahsil edildi |
| waived | Admin muaf |

---

*Hata kodları: [ERROR_CATALOG.md](./ERROR_CATALOG.md).*
