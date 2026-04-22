# JEP v1 fixtures

These fixtures add JEP (Judgment Event Protocol) receipts to the AgentID + APS + AgentGraph interop corpus.

The receipts are raw JEP artifacts. They are not reshaped for CTEF/composed-v1. In the composed example, the JEP receipt is carried verbatim in `slots.jep.payload`.

## Files

- `judgment-event.json` — root `J` event for the interop test agent.
- `verification-event.json` — `V` event whose `ref` points to the root judgment event.
- `hashes.json` — deterministic hashes used by the composed-v1 slot.
- `jwks.json` — test-only Ed25519 public key for the inner JEP JWS receipts.

## Fixture contract

- JEP core fields are preserved: `jep`, `verb`, `who`, `when`, `what`, `nonce`, `aud`, `ref`, `sig`.
- `aud` is `did:web:agentgraph.co#gateway-reverify` for the worked example.
- `ref` forms the prior-event chain.
- Canonicalization is JCS / RFC 8785.
- Inner JEP receipts are signed with EdDSA / Ed25519.
- The composed-v1 wrapper checks the JEP slot as `category: decision_event`, but skips it from the naive all-must-pass composite.

The private key seed is the test-only deterministic seed already documented by the interop repo. Do not use these keys outside fixtures.
