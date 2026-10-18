# Extriver Verified Contacts

Public business contact research for the [Extriver-Onboarding source dataset](https://github.com/HyeonbinJung/Extriver-Onboarding/blob/main/data/extriver_influencer_leads.csv).

## Data files
- [**Verified contacts**](data/verified_contacts.csv): creator leads where a business email, published business phone, or official contact form/link is available. Carries provenance, verification date, and original outreach status.
- [**Research queue**](data/contact_research_queue.csv): creators with no public email, business phone, or official contact link in the source. Includes processing state and attempts so each batch advances.
- [**Research log**](data/contact_research_log.csv): audit of completed searches, including failures and exact sources.

## Current coverage (2026-10-18)
- Source dataset: **660 creator leads**.
- Public business emails recorded: **112** (110 carried forward from the source, 2 newly checked).
- Additional creator with a published business phone/contact page but no confirmed email: **1**.
- Still in research queue: **547**.
- Source CSV was updated for Professor Noslen, Nathalia Arcuri, and Carolina Okubo.

## Hourly deep-search batch specification
Process **up to 50 queued creators per run** in oldest-unresearched order. Search:
1. Instagram bio, public contact button text, link-in-bio destinations and linked official sites.
2. YouTube channel About/description, public video and podcast descriptions, and linked site Contact/Business pages.
3. TikTok bio, official websites, management/agency pages, and indexed web search for named collaboration contacts.
4. Follow source hyperlinks and confirm the contact clearly belongs to the creator/official management and is **publicly posted for business use**.

**Never invent or infer** email patterns. Do not extract personal/private phone numbers, gated email reveals, scraped data brokers, or unrelated employers' contact addresses. Respect site access rules; blocked About panels are not verified contacts. Put a source URL next to each new contact. Prefer original official creator pages over directories or snippets. Record ambiguous leads as `needs_review` rather than filling them.

For every verified result, update both `Extriver-Onboarding/data/extriver_influencer_leads.csv` (original source of truth) and this repository's `data/verified_contacts.csv`, remove/mark the queue entry resolved, and log the evidence and date. For unsuccessful cases, record the search attempt to avoid repeating the same 50 creators every run. Do not send emails or DMs. Do not overwrite existing verified contacts unless stronger contradictory evidence is documented.

> The source repository also has an XLSX mirror, which is **not** automatically synchronized by this batch. CSV is the authoritative dataset.

## Verification labels
- `official_website`: contact publicly displayed on the creator's official website.
- `official_channel_description_mirror`: public YouTube description reproduced by a third-party channel metadata site.
- Blank verification date + `imported_from_onboarding`: carried over from the previous source without independent re-check during this run.

Scheduled research is carried out by a ChatGPT hourly task; it is not a GitHub Actions workflow, and updates depend on the connected research/GitHub tools being available during a run.
