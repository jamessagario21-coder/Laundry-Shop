# Abundant Laundry Shop — Laundry POS (Cloud version with remote monitoring)

A free, installable laundry-shop POS backed by a real cloud database
(Supabase / Postgres). Because the data lives online, **you can open the
same app from anywhere** — on your phone at home, a laptop, another
tablet — and see orders as they happen.

## What you get
- Staff/owner **login** (email + password) — only signed-in people can see or change orders.
- **Monitor tab**: today's orders and sales, how many orders are in each stage, unpaid balance, and a **live activity feed** (new orders, status changes, payments, deletions — with who did it and when).
- The feed is saved in the database, so when you open the app later you can **scroll back through what happened while you were away**.
- A **Live** badge in the header (green = connected, "Reconnecting…" = offline).
- Pop-up toast + beep when something new happens on another device; optional browser notifications.

## Setup (once)
1. Create a free project at supabase.com.
2. **SQL Editor → New query**: paste all of `supabase-setup.sql` → Run.
   (Already ran the older script? Run this one too — it's safe to repeat and upgrades it.)
3. **Create accounts** (Authentication → Users → Add user → create with email + password, and tick auto-confirm).
   Make one for yourself (owner) and one per staff member.
4. **Turn off public sign-ups** (Authentication settings → disable "Allow new users to sign up"),
   so strangers can't create their own account.
5. **Project Settings → API**: copy the Project URL and the `anon` public key into
   `SUPABASE_URL` and `SUPABASE_ANON_KEY` near the top of the script in `index.html`.
6. Upload `index.html`, `manifest.json`, `service-worker.js`, `icons/` to your GitHub repo and
   enable GitHub Pages (Settings → Pages → main branch, root).
7. Open the GitHub Pages link on every device → sign in → "Add to Home Screen".

## Monitoring from far away
Open the app on your phone, sign in, tap **Monitor**. Keep it open (or in the background) and it updates by itself.
Tap **Enable alerts on this device** to get notifications.

## Honest limits
- **Alerts only work while the app/browser is running** (foreground or background). They are not true push notifications that wake a closed app. Some tablets/iPads don't support them at all. If you need alerts when the app is fully closed, a next step is sending a Telegram/email message from Supabase — ask and I'll add it.
- **Needs internet.** The app shows the last data it received plus a warning if the connection drops; changes won't save until it's back.
- **Everyone who can sign in can edit and delete orders.** There are no separate owner/staff permissions yet.
- **Supabase free projects can pause after about a week of no activity** (check their current policy). Daily shop use keeps it awake; if it ever pauses you can resume it from the dashboard.
- The `anon` key in `index.html` is meant to be public — it's the login requirement (steps 2–4) that protects your data. Never paste the `service_role` key anywhere in this app.
