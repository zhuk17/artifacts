# Offer: fixed-scope web3 artifacts (line A)

One line: we ship written artifacts — docs, copy, cleaned data — at a fixed price, as files or a pull request, within 48 hours, paid in USDT. No calls, no hourly billing. Ongoing work only as productized subscriptions (fixed menu, prepaid monthly, cancel anytime in one message).

Buyer: small web3 projects with a treasury and no writer — best trigger: recently funded (grant announced or raise in the last ~90 days: budget exists, output pressure is real); indie devs with a grant to show output for; agencies overflow. They post these tasks publicly; we take them at the posted scope.

Why they pick a nobody: cheaper than an agency, faster than hiring, crypto-native payment, and every claim here is a link they can open.

## Catalog

| ID | What | Deliverable | Price | Made by |
|---|---|---|---|---|
| O-1 | Docs starter pack | 5 pages: intro, quickstart, install/config, API reference skeleton, FAQ — markdown, ready to merge | $80 | local model |
| O-2 | Landing copy rewrite | New copy for one landing page, same structure, plus 3 headline variants | $120 | local model |
| O-3 | Dataset clean/compile | Deduped, normalized CSV/JSON up to ~2k rows + a method note so it can be re-run | $50–100 | local tools + model |
| O-4 | Tutorial/blog set | 2 posts, 800–1200 words, code blocks tested where runnable | $90 | local model |
| O-5 | Landing illustration pack | 5–8 images, consistent style, web-optimized | $45 | Qwen-Image |

O-5 is optional filler — weak on the crypto-buyer filter, only taken alongside O-1/O-2.

## Services menu (added 2026-09-27 per human instruction: files alone cannot reach the goal)

| ID | What | Deliverable | Price | Cadence |
|---|---|---|---|---|
| S-1 | Docs site build | Full docs site (MkDocs/Docusaurus) 10–20 pages from their repo/README + CI/deploy config, delivered as mergeable repo/PR | $350–600 | one-off |
| S-2 | Docs retainer | Up to 4 update requests OR 2 new pages per month + changelog upkeep, all via PR | $250/mo prepaid | monthly |
| S-3 | Content retainer | 4 posts/mo (800–1200 w, tested code where runnable) or 2 posts + newsletter, markdown PRs to their blog repo | $300/mo prepaid | monthly |
| S-4 | Docs migration | Move existing docs to a new framework, content preserved, links fixed. ≤20 pages $200, ≤50 pages $350 | fixed tiers | one-off |
| S-5 | Data feed | Curated niche dataset refreshed monthly (built on our watcher rails), CSV/JSON + change log. Format note: publish a free summary, sell the full data (benchmark-report model) | $50–150/mo prepaid | monthly |
| S-6 | Ops subscription | Small crypto team back office run async: community report digests, analytics summaries, grant/invoice paperwork drafts, all delivered via PR/TG | $400–800/mo prepaid | monthly |

Service rules (scope-creep armor): menu-only — anything off-menu is a new quote; prepaid; 2 revision rounds included, more = new invoice; async channels only (GitHub PR + TG bot), no calls/screen-shares/voice; response within 24h; cancel anytime by one message. O-items stay as tripwire offers: every file buyer gets pitched the matching S-item after delivery.

## Included / not included

Included: one revision round inside the original scope; source files; a short changelog.

Not included: meetings (if a job needs one, we pass), open-ended maintenance, scope growth without a new fixed price, anything promising profit (signals, "growth", trading content — banned category, see IDEAS.md segment rules).

## Deal shape

1. Task found in a public channel → reply with template T1 (see `PITCH.md`), price fixed, scope quoted back in their own words.
2. Agreement in-thread or in DM. Scope frozen in writing before work starts (rule 28).
3. Work done locally. Buyer sees a watermarked preview or an open PR — proof before payment, per D-013.
4. Payment: Plisio invoice link, USDT (TRC20). Under $100: pay-on-delivery against the preview. Over $100: half before, half after.
5. Final files delivered through the Telegram bot. Entry logged in `SALES.md`.

## Open before first pitch

- Supply check: **done 2026-09-30** — see `research/supply-check-2026-09-30.md`. Lead offer is S-1 docs site build; O-items are entry purchases (D-016). Landing-copy band verified from search snippets the same day (market floor around $299), so O-2 moved to $120 (D-017). Content-retainer band stays anchored on buyer-side tooling spend ($250/mo docs tool) rather than a survey.
- Two channels named and accounts warmed (INBOX item). Waiting on the human.
- Proof samples produced (`proof/README.md`). Can start now, does not wait on anything.
