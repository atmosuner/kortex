# Test Case Catalog

**Versiyon:** 1.0  
**Format:** TC-ID — Priority — Steps — Expected

---

## Availability

**TC-AV-001** P0  
Given no booking, When evaluate available slot, Then status AVAILABLE bookable true.

**TC-AV-002** P0  
Given confirmed booking same court+start, Then BOOKED.

**TC-AV-003** P0  
Given academy block overlap, Then BLOCKED publicLabel akademi.

**TC-AV-004** P0  
Given slot start now+73h, Then OUTSIDE_ADVANCE_WINDOW.

**TC-AV-005** P0  
Given member 3 active this ISO week Mon-Sun, Then WEEKLY_LIMIT on 4th.

**TC-AV-006** P0  
Given FITNESS court, Then NOT_BOOKABLE.

**TC-AV-007** P1  
Given active fix contract Tue 18:00, When Tue 18:00 same court, Then FIXED_CONTRACT.

**TC-AV-008** P0  
Given hold expired, When confirm, Then HOLD_EXPIRED.

**TC-AV-009** P0  
Parallel confirm same slot, Then exactly one success.

**TC-AV-010** P1  
Given passive member, When POST hold, Then MEMBER_INACTIVE.

---

## Booking / cancel

**TC-BK-001** P0  
Happy path hold → confirm mock → status confirmed.

**TC-BK-002** P0  
Cancel T-3h → no fee, status cancelled.

**TC-BK-003** P0  
Cancel T-1h with ack → fee assessed.

**TC-BK-004** P1  
Add 5 guests → stored 5 rows.

**TC-BK-005** P0  
Manual booking without reason → 400.

---

## Pricing (Faz 2)

**TC-PR-001** P0  
Rule match court+season+time → snapshot total.

**TC-PR-002** P0  
Light after 18:00 slot 18:00 → surcharge in breakdown.

**TC-PR-003** P1  
No matching rule → TARIFF_NOT_FOUND.

**TC-PR-004** P0  
Tariff change after booking → old snapshot unchanged.

---

## Payment (Faz 2)

**TC-PY-001** P0  
Webhook success → payment completed booking confirmed.

**TC-PY-002** P0  
Amount mismatch → booking stays pending alert.

**TC-PY-003** P0  
Duplicate webhook → idempotent single payment.

**TC-PY-004** P1  
Reception channel → no webhook immediate confirmed.

---

## Import (Faz 3)

**TC-IM-001** P1  
100 rows 2 bad → 98 upsert error file 2 lines.

**TC-IM-002** P1  
Duplicate membership_no skip mode → skip count 1.

---

## Fix (Faz 3)

**TC-FX-001** P1  
active contract → member cannot book that slot.

**TC-FX-002** P2  
contract_signed unpaid → slot still available.

---

## Ops (Faz 4)

**TC-OP-001** P1  
3 bookings today → cleaning list 3 courts.

**TC-OP-002** P2  
Mark complete → completed_at set.

---

## E2E (Playwright)

**TC-E2E-001** P0  
Login member → select tomorrow slot → confirm → see in list.

**TC-E2E-002** P1  
Admin login → create block → member sees blocked.

---

## Accessibility

**TC-A11Y-001** P1  
Grid cells have accessible name including status.

**TC-A11Y-002** P2  
Focus order logical on checkout.

---

*Strategy: [../TESTING.md](../TESTING.md).*
