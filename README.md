# Idealista Bot

**AI-powered listing matching for [imoFlow](https://github.com/TGS07/imoflow), the real-estate CRM built at [FORMA](https://formaagency.pt).**

> 🔒 This repository is a public overview. The source code is private.

## What it does

Real-estate agents get dozens of Idealista alerts every day and have to check each new listing against every buyer they're working with. This bot does that automatically:

1. **Reads** Idealista alert emails from a central Gmail inbox. It works only with the alert emails, with no scraping.
2. **Extracts** each listing (price, type, area, location, features) with an LLM.
3. **Matches** every listing against the search criteria of all active buyers in imoFlow, across all agencies.
4. **Drafts** a personalised message to the buyer.
5. **Notifies** the agent responsible for that buyer on Telegram, with **Send / Edit / Ignore** buttons.
6. **Sends** the email in the agency's name when the agent taps *Send*, and logs it in the lead's history in imoFlow.

## Architecture

```
Gmail (alerts) ──▶ parser (LLM) ──▶ matching (LLM for areas)
                                          │
                                          ▼
Telegram ◀── card + buttons ◀── drafter (LLM) ── Supabase (imoFlow)
   │
   └─ Send ─▶ email on behalf of the agency (Gmail) + logged in imoFlow
```

## Highlights

- **Multi-agency:** one bot instance serves every agency on imoFlow. Each match is routed to the agent assigned to that lead.
- **Self-service onboarding:** agents connect their own Telegram from imoFlow's settings with one click.
- **Swappable LLM provider:** Groq for development and Claude for production, chosen with a single setting.
- **Safe by default:** a dry-run mode prints what would be sent without sending anything.

## Tech stack

<img src="https://skillicons.dev/icons?i=python,supabase,postgres&perline=10" alt="Python, Supabase, Postgres" />

Python · python-telegram-bot · Supabase (Postgres) · Gmail API · Claude / Groq · Railway

---

Interested in imoFlow for your agency? Get in touch at [formaagency.pt](https://formaagency.pt).
