# Colby Reminders Clock

Independent every-5-minute trigger for the Paid In Full pre-call reminder + value-track
automation (`learn.paidinfull.vip/api/send-reminders`).

**Why this exists:** Vercel's native cron for the `colby-paidinfull` project stopped firing
(platform-level scheduler failure, diagnosed 2026-06-07) even with correct config. Rather than
depend on it, this repo's GitHub Action calls the same secret-protected endpoint on a schedule.

- The endpoint is idempotent: it dedups via GHL `*-sent` tags and only acts inside tight time
  windows, so repeat calls never double-send.
- The full URL (including `?secret=`) is stored in the repo secret `REMINDERS_PING_URL`.
- To pause: disable the workflow in the Actions tab. To change cadence: edit the cron in
  `.github/workflows/ping-reminders.yml`.

See the master doc in the vault: `Clients/colby-lyman/automation-system-DOCS.md`.
