# 🧠 Google Review Bot

Automate your **Google Business Profile review management**.  
This bot automatically **replies to positive reviews** using **Gemini** and **emails you when negative reviews appear**.

---

## 🚀 Features

| ⭐ Rating | Action |
|-----------|--------|
| 1–3 Stars | Sends an **email alert** so you can review it manually. |
| 4–5 Stars | Uses **Gemini AI** to generate a polite, brand-friendly response and posts it automatically. |

Additional features:
- Prevents duplicate alerts or replies using persistent state.
- Runs on schedule (local cron, Cloud Function, or Cloud Run).
- Fully configurable via environment variables.

---

## 🧩 Architecture

