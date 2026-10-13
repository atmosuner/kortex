# Deployment ve Ortamlar

**Versiyon:** 1.0

---

## 1. Ortamlar

| Ortam | URL (örnek) | Amaç |
|-------|-------------|------|
| local | localhost:3000 | geliştirme |
| staging | staging-tenis.tedclub.org.tr | pilot |
| production | tenis.tedclub.org.tr | canlı |

---

## 2. Altyapı seçenekleri

**Önerilen MVP:** Vercel (Next.js) + Supabase (Postgres) veya Neon Postgres.

Alternatif: Kulüp VPS (Docker Compose: app + postgres + caddy).

---

## 3. Ortam değişkenleri

| Değişken | Zorunlu | Açıklama |
|----------|---------|----------|
| DATABASE_URL | ✓ | Postgres |
| AUTH_SECRET | ✓ | session |
| CRON_SECRET | ✓ | cron routes |
| IYZICO_API_KEY | Faz 2 | |
| IYZICO_SECRET | Faz 2 | |
| IYZICO_BASE_URL | Faz 2 | sandbox/prod |
| APP_URL | ✓ | callback URL |
| EMAIL_* | Faz 4 | SMTP |

---

## 4. Docker Compose (local)

```yaml
# referans — kod aşamasında repo kökünde
services:
  db:
    image: postgres:16
    environment:
      POSTGRES_DB: kortex
      POSTGRES_USER: kortex
      POSTGRES_PASSWORD: kortex
    ports:
      - "5432:5432"
```

---

## 5. Migration

- `prisma migrate deploy` prod  
- Rollback: forward-fix migration (no down)  

---

## 6. Cron

Vercel cron `vercel.json`:

```json
{
  "crons": [
    { "path": "/api/cron/expire-holds", "schedule": "*/5 * * * *" },
    { "path": "/api/cron/evening-cleaning", "schedule": "5 19 * * *" }
  ]
}
```

`19:05 UTC` = 22:05 Istanbul (DST dikkat — cron Istanbul ayarı tercih).

---

## 7. SSL / DNS

- TED IT DNS A/CNAME  
- TLS Let’s Encrypt  

---

## 8. Release prosedürü

1. staging deploy  
2. smoke test checklist  
3. prod deploy maintenance window (düşük trafik)  
4. monitor 24h  

---

## 9. Rollback

Vercel instant rollback previous deployment. DB migration geri alınmaz — repair forward.

---

## 10. Yedekleme

- Supabase/Neon otomatik daily  
- Manual pg_dump before major migration  

RPO/RPO: [../NON_FUNCTIONAL_REQUIREMENTS.md](../NON_FUNCTIONAL_REQUIREMENTS.md)

---

*Monitoring: [MONITORING.md](./MONITORING.md).*
