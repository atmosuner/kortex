# Monitoring, Logging, Alerting

**Versiyon:** 1.0

---

## 1. Loglama

- Structured JSON logs  
- Fields: `timestamp`, `level`, `request_id`, `user_id`, `action`, `duration_ms`  
- PII mask: email partial, no password, no card  

---

## 2. Metrikler

| Metrik | Alert |
|--------|-------|
| API 5xx rate | &gt; 1% 5 min |
| booking confirm latency p95 | &gt; 3s |
| payment webhook fail | any |
| hold expire job miss | job not run 15 min |
| pending_payment stale | &gt; 10 count |

---

## 3. Araçlar

- Sentry (errors)  
- Vercel analytics veya self-hosted Grafana (opsiyonel)  

---

## 4. Health

`GET /api/health` → `{ "db": "ok", "version": "..." }`

Load balancer probe.

---

## 5. Audit vs application log

Audit: DB append-only. App log: ephemeral 30 gün.

---

## 6. On-call

Kulüp içi — super_admin iletişim listesi (operasyon doc).

Pilot ilk ay günlük log review.

---

*Security incidents: [../SECURITY_AND_PRIVACY.md](../SECURITY_AND_PRIVACY.md).*
