# Bileşen Spesifikasyonu (Design System)

**Versiyon:** 1.0  
**Token kaynağı:** [BRANDING.md](../../BRANDING.md)

---

## 1. Button

| Variant | BG | Text | Min height |
|---------|-----|------|------------|
| primary | --color-primary | white | 44px |
| secondary | transparent | primary border | 44px |
| destructive | --color-error | white | 44px |
| ghost | transparent | text | 44px |

States: hover, focus-visible ring 2px, disabled opacity 0.5, loading spinner inline.

---

## 2. Segment control (kort grubu)

3 segment: Balon | Kapalı | Merkez.  
Active: primary bg; inactive: surface border.

---

## 3. Date stepper

◀ ▶ chevron 44px touch.  
Center: formatted date.  
Disabled next if &gt; max advance.

---

## 4. CourtGridCell

Props: `status`, `selected`, `label?`, `onSelect`

| status | Background | Cursor |
|--------|------------|--------|
| available | surface | pointer |
| booked | neutral | default |
| blocked | warning tint | default |
| not_bookable | — | hidden |

Selected: 2px primary border.

Keyboard: Enter to select.

---

## 5. HoldTimer

Countdown mm:ss; &lt; 2 min warning color; expire callback.

---

## 6. PriceBreakdown

Rows: label left, amount right tabular-nums; total bold border-top.

---

## 7. GuestListEditor

Dynamic rows; min 0 guests; add button secondary full width mobile.

---

## 8. StatusBadge

booking: confirmed green, pending amber, cancelled gray.

---

## 9. Admin DataTable

Sortable headers, row click → detail, pagination cursor.

Compact density: row 36px.

---

## 10. ReasonTextarea

Manual booking / override.  
`minLength=10`, live counter, error state red border.

---

## 11. CleaningCheckRow

Checkbox 32px + court name text-lg; entire row tap target.

---

## 12. Toast / Banner

Toast: 5s auto dismiss.  
Banner: persistent error (payment fail).

---

## 13. Empty state

Illustration optional; title + body + primary CTA.

Örnek: “Bu tarihte müsait saat yok” + tarih değiştir.

---

## 14. Form field

Label, input, hint, error text linked aria-describedby.

---

## 15. Modal

Overlay 50% black; panel max-width 480px mobile full bleed bottom sheet optional.

---

*Copy: [COPY_DECK.md](./COPY_DECK.md).*
