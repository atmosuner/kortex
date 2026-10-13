# Hata ve Mesaj Kataloğu

**Versiyon:** 1.0  
**Format:** `CODE` — HTTP — Kullanıcı mesajı (TR) — Staff mesajı — Retry?

---

## 1. Auth

| CODE | HTTP | Kullanıcı | Staff | Retry |
|------|------|-----------|-------|-------|
| AUTH_INVALID | 401 | E-posta veya şifre hatalı. | — | Evet |
| AUTH_SESSION_EXPIRED | 401 | Oturumunuz sona erdi. Tekrar giriş yapın. | — | Evet |
| MEMBER_INACTIVE | 403 | Üyeliğiniz rezervasyon için uygun değil. Resepsiyonla iletişime geçin. | Member passive/suspended | Hayır |
| FORBIDDEN | 403 | Bu işlem için yetkiniz yok. | RBAC | Hayır |

---

## 2. Availability / booking

| CODE | HTTP | Kullanıcı | Retry |
|------|------|-----------|-------|
| SLOT_TAKEN | 409 | Bu saat az önce rezerve edildi. Lütfen başka saat seçin. | Evet |
| SLOT_NOT_AVAILABLE | 409 | Bu saat müsait değil. | Evet |
| BLOCKED | 409 | Bu saat kulüp programına ayrılmıştır. | Hayır |
| NOT_BOOKABLE | 400 | Bu kort rezervasyona kapalıdır. | Hayır |
| OUTSIDE_ADVANCE_WINDOW | 400 | En fazla 3 gün sonrasına rezervasyon yapabilirsiniz. | Hayır |
| WEEKLY_LIMIT | 400 | Bu hafta en fazla 3 aktif rezervasyonunuz olabilir. | Hayır |
| HOLD_EXPIRED | 410 | Rezervasyon süreniz doldu. Lütfen tekrar seçin. | Evet |
| HOLD_NOT_FOUND | 404 | — | Evet |
| BOOKING_NOT_FOUND | 404 | Rezervasyon bulunamadı. | Hayır |
| CANCEL_TOO_LATE | 400 | İptal cezası uygulanacaktır. Onaylıyor musunuz? | — (2-step) |
| INVALID_GUEST | 400 | Misafir adı boş olamaz. | Evet |

---

## 3. Pricing / payment

| CODE | HTTP | Kullanıcı | Retry |
|------|------|-----------|-------|
| TARIFF_NOT_FOUND | 500 | Fiyat hesaplanamadı. Resepsiyonla iletişime geçin. | Hayır |
| PAYMENT_FAILED | 402 | Ödeme tamamlanamadı. Kart bilgilerinizi kontrol edin. | Evet |
| PAYMENT_AMOUNT_MISMATCH | 500 | — (internal) | Hayır |
| REFUND_FAILED | 500 | İade işlemi tamamlanamadı. Muhasebe ile iletişime geçin. | Hayır |

---

## 4. Admin

| CODE | HTTP | Staff | Retry |
|------|------|-------|-------|
| OVERRIDE_REASON_REQUIRED | 400 | Gerekçe en az 10 karakter olmalıdır. | Evet |
| BLOCK_OVERLAP_WARNING | 409 | Mevcut rezervasyon var. Devam? | Evet |
| IMPORT_ROW_ERROR | 422 | Satır {n}: {detail} | Düzelt |

---

## 5. Sistem

| CODE | HTTP | Kullanıcı | Retry |
|------|------|-----------|-------|
| RATE_LIMIT | 429 | Çok fazla deneme. Lütfen bekleyin. | Evet |
| INTERNAL | 500 | Beklenmeyen bir hata oluştu. | Evet |

---

## 6. API response envelope

```json
{
  "ok": false,
  "error": {
    "code": "WEEKLY_LIMIT",
    "message": "Bu hafta en fazla 3 aktif rezervasyonunuz olabilir.",
    "details": { "active_count": 3, "week_start": "2026-10-12" }
  }
}
```

---

## 7. Log seviyesi

| CODE | Log |
|------|-----|
| 4xx business | info |
| PAYMENT_* | warn |
| INTERNAL | error + stack |

---

*Copy deck: [../design/COPY_DECK.md](../design/COPY_DECK.md).*
