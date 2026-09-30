# S-3 — Dataset cleaning sample: ETHGlobal project registry (10 of 30 rows)

SAMPLE — capability demo by FreelanceWorker, 2026-09-27.
Source: GitHub Search API, `topic:ethglobal created:>2026-03-01`, fetched 2026-09-27 (65 matches, first 30 taken, 10 shown). Public metadata only. Full pack = all rows, all fields, CSV + notes.

## Before — what arrives raw

Typical defects in this feed (each present in the shown rows):

- **Missing license** on 3 of 14 sampled repos (`null` in API) — a legal blocker if the list feeds a BD or research pipeline.
- **Missing homepage** on 2 of 14; one "homepage" just points back to the repo README; one has a trailing slash.
- **Event name written five ways**: `ETHGlobal Tokyo 2026` in prose, `ethglobal-tokyo`, `ethonline2026`, `ethglobal-2026`, `ethglobal-openagents-2026` in topics, or absent.
- **Descriptions mix product, sponsors and pitch**: one row buries what the thing *does* under four sponsor names; another starts with a lowercase brand and an em-dash slogan.
- **Chain/platform** never appears as a field — it must be inferred from topics + description, and sometimes it genuinely isn't there.
- **Repo names lie**: `a42x/ETHGlobalTokyo2026` contains "MynaAgent"; `Access0x1/Access0x1` is a duplicate-name org.

## After — cleaned 10 rows

| Project | What it does (one line) | Category | Chain / key infra | License | Live link | Event | Last push |
|---|---|---|---|---|---|---|---|
| Waterline | Verifies rented GPUs deliver the chip and speed you pay for; verdicts on ENS | Infra verification | Ethereum Sepolia, Curvegrid | ⚠ none declared | waterline-eth.vercel.app | Tokyo 2026 | 2026-09-27 |
| Kagi Wallet | Threshold wallet giving AI agents their own spending key, never yours | Wallet security | MPC (chain n/s) | ⚠ none declared | kagiwallet.com | n/s | 2026-09-27 |
| MynaAgent | In-wallet AI agent claims JP public benefits with a ZK age proof, paid in JPYC | Identity / agents | Polygon, Noir, Groth16 | Apache-2.0 | ethglobal showcase page | Tokyo 2026 | 2026-09-26 |
| EQLTY Desk | Seven AI agents trade tokenized stocks inside user-granted limits | Agent trading | Robinhood Chain, Uniswap V4 | MIT | ⚠ none | Online 2026 | 2026-09-26 |
| DAS Busters | Proves single status to a dating app via ZK, no data disclosed | Identity / ZK | ZK stack, World ID (chain n/s) | GPL-3.0 | das-busters.vercel.app | Tokyo 2026 | 2026-09-26 |
| AntiScalper Protocol | Human-verified purchasing of limited physical drops when bots can buy too | Commerce | Sui, x402 | MIT | ⚠ none | Tokyo 2026 | 2026-09-26 |
| Tenjō | Ticket-lottery entry system with pity weighting; one human one entry | Consumer dApp | Sui, Move, passkeys | MIT | tenjo-azure.vercel.app | n/s | 2026-09-26 |
| Hanvil | Local Hedera node in one Rust binary; boots in ms, keeps rejected txs | Dev tooling | Hedera/Hiero | MIT | (= repo README) | Online 2026 | 2026-09-26 |
| StoikovHook | Uniswap v4 hook charging arbitrageurs market-making-style fees | DeFi | Ethereum, Foundry | MIT | ethglobal showcase page | n/s | 2026-09-26 |
| OpenBook | Data marketplace for AI agents — fresh data or refund | Data / payments | Arc, USDC, MCP | MIT | openbook.litai.ca | Online 2026 | 2026-09-20 |

## Method notes (the actual deliverable)

1. **Source line preserved**: query string, fetch timestamp, total/matched counts recorded above the table so any number is reproducible.
2. **Description split, not rewritten**: every raw description decomposes into function / event tag / sponsor noise. Only the function survives into "What it does"; nothing invented — if the raw text can't support a one-liner, the cell says `n/s`.
3. **Controlled vocabulary for events**: `ethglobal-tokyo`, `ETHGlobal Tokyo 2026`, `ethglobal-2026` → one canonical value; ambiguous or absent → `n/s`, never guessed.
4. **Chain inferred with provenance**: taken from topics ∩ description; conflicts resolved toward the description; genuinely absent → `n/s`.
5. **License gaps are flags, not blanks**: `⚠ none declared` stays visible in the main table — hiding them would destroy the point of the column.
6. **Homepage normalized**: scheme and trailing slash stripped, then classified `demo | showcase | repo`; a repo-link masquerading as a homepage is labeled as such instead of deleted.
7. **Category from a fixed 12-value list** (agents, DeFi, identity/ZK, infra, dev tooling, consumer, commerce, data, wallet security, gaming, RWA, other) assigned from function text — free-text tags are where datasets go to die.
8. **Nothing silently dropped**: raw fields stay in an adjacent sheet; the clean table is a view, so every cell can be audited back to source.

## What the full $50–100 pack adds

All 30–65 rows · CSV + cleaned-sheet format · dedupe across forks/orgs · contact-handle column · weekly-refresh option.
