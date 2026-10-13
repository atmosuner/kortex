# Edge Cases — Ürün ve Operasyon

**Versiyon:** 1.0

Operasyon ekibinin “ya şöyle olursa?” sorularına hazır cevaplar.

---

## Rezervasyon

1. **Üye ödeme ekranında uygulama kapattı** — pending_payment 15 dk sonra cron cancel; slot açılır. Üye “Rezervasyonlarım”da pending görür veya iptal.

2. **Kart çekildi webhook gecikti** — booking pending; üye destek. Admin payment reconcile manuel confirm (audit).

3. **Aynı üye iki cihazda aynı slot** — ikinci hold red veya aynı hold token.

4. **Saat 21:00 son slot, maç 22:00 biter** — grid doğru; temizlik akşam batch, rez sonrası değil.

5. **Misafir 20 kişi** — izin var; UI performans textarea/list.

6. **Üye adını yanlış yazdı misafir** — edit Faz 2; MVP admin düzeltme.

7. **Turnuva bloku yarın, üye bugün 3. rezervasyonu yarın için** — limit haftaya göre; turnuvada slot blocked.

8. **Fix kort + üye o saatte başka kort** — izin var (farklı court).

9. **Admin blok koydu, mevcut rez var** — import uyarı; admin mevcut rez taşımalı (manuel prosedür).

10. **DST günü** — [SEASON_TRANSITION.md](../operations/SEASON_TRANSITION.md).

---

## Tahsilat

11. **Kısmi iade** — payment refunded partial; booking cancelled veya fee deducted.

12. **Nakit resepsiyon, sonra üye online da dener** — slot BOOKED.

13. **Ceza borcu, yeni rez** — policy: borç varken book engelle (önerilen Faz 2b) veya izin ver.

14. **KDV faturası** — uygulama dışı muhasebe; export’ta tutar yeterli.

---

## Fix kort

15. **Sözleşme bitiş haftası yarım** — active_to date inclusive; son gün lock.

16. **Kort bakım, fix Salı** — bakım bloku öncelik; kulüp fix taşır (offline anlaşma).

17. **Ödeme gecikti, sözleşme imzalandı** — status contract_signed, not active; slot açık.

---

## Mevsim / balon

18. **Balon 1–3 fark fiyat, 4–9 fark** — tariff_rule court_id.

19. **Geçiş haftası yarım hafta farklı mod** — season_assignment günlük granularity date range.

20. **Merkez yaz modu, balon kış** — bağımsız assignment.

---

## Personel

21. **Resepsiyon yanlış üyeye rez** — admin transfer booking (Faz 2) veya cancel+recreate audit.

22. **Saha telefonu şarj yok** — kağıt yedek liste cron email Faz 4.

23. **super_admin ayrıldı** — en az 2 super_admin policy.

---

## Teknik

24. **DB restore dün** — ödeme provider reconciliation.

25. **Import duplicate üye no** — skip veya merge admin seçimi.

---

*Availability detay: [AVAILABILITY_RULES.md](./AVAILABILITY_RULES.md).*
