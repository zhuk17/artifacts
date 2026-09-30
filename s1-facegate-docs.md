# S-1 — Docs rewrite sample: FaceGate quickstart

Sample docs work by FreelanceWorker, 2026-09-27. Source: [omsant02/FaceGate](https://github.com/omsant02/FaceGate) @ `80a1ed8` (ETHGlobal ETHOnline 2026). Original README quoted briefly with attribution; everything below Part 2 is newly written.

Target page: the developer quickstart for `@facegate/sdk`.

## Part 1 — What is actually wrong (each item verifiable)

1. **No license.** The repo contains no LICENSE file and GitHub reports `license: null`. An SDK whose npm package has no license cannot be legally integrated by any subscription platform — the exact customers it targets. This is a revenue bug, not a docs nit.
2. **Internal artifact linked as documentation.** The README sends readers to `FEEDBACK.md` ("a full analysis of why this friction is intentional") — a hackathon judging document, not user docs.
3. **The core flow is documented backwards.** The login snippet calls `gate.enroll()` on every login; the docs then apologize in a footnote ("We know this looks like enrollment every login — it isn't"). When the API name and the explanation fight each other, the reader stops trusting both.
4. **The failure path — the product's whole value — is undocumented.** What happens when faces don't match? What error does `confirm()` throw, what should the app show, can the user retry, how many times? Nothing. The happy path works; the path that *is the product* is missing.
5. **The wasm footgun is buried.** "Critical: bundler configuration" sits near the bottom of a 10 KB README. A Next.js integrator hits it at minute two, not hour two.
6. **SDK reference has no contract.** A table of method names with prose descriptions — no signatures, no types, no return shapes, no error cases. A developer cannot write code against it without opening the source.

## Part 2 — Proposed quickstart (new text)

### Prerequisites

- Node 18+, a bundler that handles WASM (see [WASM setup](#wasm-setup) — do this first, it breaks builds silently)
- A FaceGate API key from the [dashboard](https://face-gate-ecru.vercel.app)
- Users need the World app with a World ID

### Install

```bash
npm install @facegate/sdk
```

### The model in one paragraph

Each account gets one enrolled nullifier — a cryptographic fingerprint of one face, created on the user's device, never a photo. At signup you store that pairing. At every login you check the presented face against the stored nullifier. Match → same person. Mismatch → different person, block. Cross-app unlinkability: the same face produces different nullifiers per app.

### Signup: enroll once

```ts
import { FaceGate } from "@facegate/sdk";

const gate = new FaceGate({ apiKey: process.env.FACEGATE_API_KEY! });

// During signup only:
const { success, nullifier } = await gate.enroll({ userId });
if (!success) throw new Error("enrollment failed — see error table below");
// Store `nullifier` against `userId` in your database. This is your only record.
```

### Login: gate every session

```ts
const result = await gate.confirm({ userId, expectedNullifier: stored });

switch (result.status) {
  case "match":     grantSession(result.userId); break;
  case "mismatch":  denySession("This account is enrolled to a different face."); break;
  case "not_found": redirect("complete-enrollment"); break; // user reinstalled World app
  default:          failClosed(); // never fail open on unknown status
}
```

### Failure modes

| Status | Meaning | User sees | Retry? |
|---|---|---|---|
| `match` | Same face as enrollment | normal login | — |
| `mismatch` | Different face presented | generic "verification failed"; log internally | yes, own face only |
| `not_found` | No nullifier stored | "finish setting up verification" | yes, re-enroll |
| network/API error | FaceGate server unreachable | "try again" — **treat as failure, do not grant access** | yes, backoff |

Design rule: every non-`match` outcome denies access. A verification library that fails open is a verification library that is off.

### WASM setup (do before first build)

`@worldcoin/idkit-core` ships WASM. Without config, Vite/Next builds silently produce a broken hash module. For Next.js add to `next.config.js`:

```js
module.exports = { webpack: (config) => { config.experiments = { ...config.experiments, asyncWebAssembly: true }; return config; } };
```

Symptom if skipped: runtime error mentioning `wasm` or `WebAssembly.instantiate`.

### Re-enrollment policy (decide this before launch)

A user can re-enroll by design (new phone, lost World account). Your anti-sharing goal needs a rule: e.g. max 1 re-enrollment per 90 days, or re-enrollment requires a second factor. FaceGate stores nullifiers; the policy is yours.

## Part 3 — What the full $80 pack adds

API reference with real signatures and error unions · server-side endpoint docs · threat model (what the API key can and cannot do, key rotation) · LICENSE triage and file (this alone unblocks integrators) · troubleshooting index.
