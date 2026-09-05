# First Devin Task — HELPER Proof-First Hardening

You are working on HELPER, a nonprofit direct-human-help platform. Your job is **not** to redesign the mission or invent new authority. Your job is to inspect the canonical codebase, preserve the immutable laws below, and produce a bounded merge-ready hardening candidate with evidence.

## Immutable laws

1. HELPER platform fee on aid intended for recipients is exactly 0%.
2. The operator must not possess custody or aid-moving keys.
3. Settlement must be donor-to-recipient-authorized / provider-authorized direct settlement.
4. Recipient-signed destinations and route terms remain immutable after authorization.
5. Need Confidence, Fraud Risk, and Recipient Authority remain separate concepts, outputs, and reason-code families.
6. NCG remains SHADOW with `controls_aid=false`.
7. Funding, broadcast, finality, delivery, evidence, proof, dispute, reorg, human decision, appeal, and resolution remain separate states. Do not infer one from another.
8. Mainnet and real aid remain disabled.
9. Model output is not fact. A passing test is evidence only for the scope it actually tested.
10. Do not silently rewrite history or hide unresolved blockers.

## Task

### Checkpoint 1 — Repository map
- Inventory the repo, runtime surfaces, payment/route code, trust code, state machines, evidence/proof code, tests, CI, and demo-only surfaces.
- Identify every place that can mutate destination, fee, authority, settlement state, or public success state.
- Return a concise authority map before editing code.

### Checkpoint 2 — Invariant tests
Add or strengthen tests that prove, at minimum:
- HELPER fee is zero on recipient aid paths.
- No operator withdrawal / reroute / destination-rewrite path exists.
- Recipient-authorized destination and route terms cannot be changed after authorization.
- NCG cannot release, block, reroute, or otherwise control aid.
- Trust outputs remain separated.
- UI/API state cannot jump from funding/broadcast directly to delivery/resolution.

### Checkpoint 3 — Adversarial cases
Attempt to break the laws with:
- state skipping,
- false-success API responses,
- stale or mismatched evidence,
- route mutation,
- duplicate/replayed events,
- reorg/reversal after apparent success,
- dispute/appeal race conditions,
- missing recipient authority,
- malformed reason codes.

### Checkpoint 4 — Browser / E2E evidence
Run the relevant app locally. Exercise one complete simulation-only path in the browser:

`discover need → inspect trust → verify recipient authority → inspect immutable route → advance evidence states → open dispute/appeal path`

Capture screenshots or video evidence for the tested path. Do not label a step as successful unless the underlying state actually supports it.

### Checkpoint 5 — Report and PR
Return:
- files changed,
- tests added/updated,
- commands run,
- test results,
- screenshots/video evidence,
- unresolved blockers,
- any place the code or UI still violates an immutable law.

Do **not** merge or recommend production deployment if any invariant gate is unresolved.
