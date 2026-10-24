# The Desk — Design & Security Review (Phase 0)

**Branch:** `lab-agent-pond-phase0` · **Date:** 2026-10-24 · **Author:** Agent0
**Status:** prototype for Director review — no merge, no deploy, no DNS.

## 1. What was built

A static prototype of Agent0's first Pond plot, per the Director's Phase 0
ruling (2026-10-24): namespace-first, real neighbors only, Agent0 designs his
own plot consistent with ToadAid community principles.

| File | Purpose |
|---|---|
| `desk.html` | The plot's public face: identity card, charter, labeled evidence, approved public KF artifacts |
| `CHARTER.md` | The plot's law: five charter laws + what The Desk is / is not |
| `EVIDENCE.md` | Curated evidence examples, labeled VERIFIED / SIMULATED / PROPOSAL |
| `REVIEW.md` | This report |

Design choices: dark pond palette with frog-green accents; three-badge label
system (green VERIFIED / amber SIMULATED / grey PROPOSAL) so a reader can never
confuse a graded fact with practice or a plan; zero JavaScript, zero external
assets, zero trackers; every external link goes to a public ToadAid surface.

## 2. Security review — boundary checklist

| Director boundary | Status | How it is honored |
|---|---|---|
| No live private journal or memory exposure | ✅ | Only aggregate counts (n=440+, hit rate, gate states) — no journal text, no memory content, no receipt bodies |
| No credentials, internal endpoints, or sensitive receipts | ✅ | No keys, tokens, URLs to internal services, or wallet material anywhere in the four files |
| No public deployment, DNS changes, token issuance, or merge | ✅ | Work confined to `lab-agent-pond-phase0`; PR is for review only; merge is the Director's |
| No execution authority or human-approval bypass | ✅ | Page is static text; charter states the human authorizes; nothing on the plot can act |
| Show only approved public KF artifacts | ✅ | Links limited to `ToadAid/knowledge-forge-public` (doctrine, blueprint, fixture) — the public release repo, not the ops repo |
| Clearly distinguish verified vs simulated vs proposal | ✅ | Three-badge system applied to every record, plus a legend |

## 3. Threats considered

- **Data leakage:** mitigated — aggregates only; no positions, sizes, or private text.
- **Impersonation / spoofed identity:** mitigated — identity card points to the
  onchain registry and explicitly invites re-verification; the page claims
  nothing live.
- **Label confusion (paper read as real):** mitigated — badges on every record
  plus the legend; simulated records state "no funds move" inline.
- **Supply chain:** mitigated — no JS, no CDN assets, no forms; pure HTML/CSS.
- **Overclaiming:** the identity card says VERIFIED *at verification time* and
  tells the reader to re-verify; the proposal section is labeled PROPOSAL.

## 4. Honest limitations

- The identity card is a snapshot (2026-10-24); a live re-verification endpoint
  is Phase 1 territory (pond-card), not built here.
- Aggregate counts drift as the desk runs; the page dates them instead of
  pretending they are current.
- The page is unlinked from `index.html` navigation on purpose — wiring it in
  is part of the Director's merge decision.

## 5. Build provenance

- Branch cut via the P1B forge lane after the shared MCP lane refused branch
  creation (`403 Resource not accessible by personal access token` — reported
  verbatim, not routed around).
- Identity proof from a read-only ERC-8004 verification against Base.
- Doctrine/fixture links confirmed live in `ToadAid/knowledge-forge-public`
  before inclusion.

**Recommendation to Director:** review the four files; if approved, merge and
wire a link from `index.html` (one line) — deployment then follows the site's
existing GitHub Pages flow, which remains the Director's action.