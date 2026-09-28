# orcfax-preview-consume-sketch

**Community learning / scaffolding docs** for an **unpaid Orcfax Preview
consume** path: how to read public Fact Statement (FS) UTxOs via the
FactStatementPointer (FSP), and where a Mesh unlock would attach a reference
input — **docs + public-read framing only**.

**Who this is for:** builders who already have Mesh + Aiken hello on Preview
(sibling package) and the packaging-glue map; maintainers packaging a clear
one-vendor unpaid-oracle sketch for community peer review.

> **Not official Orcfax, Mesh, or Aiken docs.**  
> **Not** a live freshness-gated oracle E2E. **Not** CIP-30. **Not** mainnet.  
> **Not** production-audited. **Not** “on-demand Mesh portal = Aiken dApp kit.”  
> Reviewed for community publish readiness before any public release.  
> No seeds / keys / Blockfrost project ids.

> ### Non-executable until re-probe (read this first)
> Sampled Preview Fact Statement UTxOs were **months-stale** at scout time
> (**Shaky** freshness — newest sampled `block_time` ~**2026-04-16 UTC**).
> Treat this package as **docs + public-read framing only**. Do **not** expect
> a DIY Mesh unlock that attaches an FS reference input to succeed on a short
> validity window **today**. Before any “live attach” claim: re-probe freshness
> with a dated STATUS row, or use the upstream Orcfax **mock** path. A live
> attach was **NOT RUN** here.

## Verified scope (2026-09-27 PT)

| | |
|---|---|
| **Solid (docs, re-fetched 2026-09-27 PT)** | Orcfax consume steps (FSP → FS token → statement datum); Preview Active **FSP** / **FS** / **C** hashes; feed-use “public once published”; on-demand = Subbit pay-per-use + Mesh CIP-30 **portal** |
| **Solid (public chain probe, 2026-09-27 PT)** | Preview FSP UTxO present; FSP datum → FS hash matches Active FS; **278** FS-token UTxOs unspent; sample CER `feed_id`s decode (`CER/ENCS-ADA/3`, `CER/SURF-ADA/3`, `CER/MIN-ADA/3`) — **no Orcfax API key** |
| **Solid (sibling practice, 2026-09-25 PT)** | Mesh + Aiken hello lock/unlock on Preview — see `cardano-preview-mesh-aiken-hello` (https://github.com/booper-labs/cardano-preview-mesh-aiken-hello) |
| **Shaky** | Sampled FS UTxO freshness — newest sampled `block_time` ~**2026-04-16 UTC**; `orcfax-aiken` stdlib **1.9.0** vs practice stdlib **v3** drop-in compatibility |
| **Not verified / NOT RUN** | Live short-validity-range Mesh unlock with Orcfax reference input; Aiken feed_id + freshness validator in this tree; CIP-30; mainnet; TVL / users |
| **Not claimed** | production-ready, battle-tested, audited, official, “ships a live oracle kit” |

Exact pins: [`VERSIONS.md`](VERSIONS.md). Evidence matrix: [`STATUS.md`](STATUS.md).  
Upstream scout research notes stay **private** (not part of this public ship set).

## One-sentence unpaid path

**Unpaid consume = on-chain FS UTxOs discovered via FSP.** Once published, that
datum is publicly readable (feed-use). You do **not** need an Orcfax API key for
that path. You **do** need a Cardano chain provider (Koios public / Blockfrost
free tier / node) — separate from Orcfax.

## Quick start (reading order)

1. Scope + honesty: this README
2. Everyday explanation: [`PLAIN-LANGUAGE.md`](PLAIN-LANGUAGE.md)
3. Honest DIY Mesh reference-input path: [`RECIPE.md`](RECIPE.md)
4. Gotchas + link stamps: [`GOTCHA.md`](GOTCHA.md)
5. Pins + evidence: [`VERSIONS.md`](VERSIONS.md) · [`STATUS.md`](STATUS.md)
6. Peer review note: [`audits/peer-review-pass.md`](audits/peer-review-pass.md)

## Package contents

| Path | Role |
|------|------|
| `README.md` | This front door |
| `PLAIN-LANGUAGE.md` | Non-expert explanation of unpaid consume vs on-demand |
| `RECIPE.md` | DIY Mesh reference-input scaffolding (not a live E2E) |
| `GOTCHA.md` | Freshness / stdlib / portal / hello-path gotchas |
| `VERSIONS.md` | Documented Preview FSP/FS + practice pins |
| `STATUS.md` | What was probed vs NOT RUN; URL re-fetch matrix |
| `SECURITY.md` | How to report problems |
| `audits/peer-review-pass.md` | Peer review pass (correctness / presentation) |
| `LICENSE` | MIT |

## Sibling baseline (do not skip)

| Package | Role |
|---------|------|
| `cardano-preview-mesh-aiken-hello` ([live](https://github.com/booper-labs/cardano-preview-mesh-aiken-hello)) | **Verified** Mesh + Aiken hello lock/unlock on Preview |
| `cardano-packaging-glue-starter` | Packaging map + comments-only `stub/oracle-read.sketch.ts` |

Upstream scout notes that informed this sketch stay private.

## Honesty about limits

This is a **docs-only / no CI / unpaid public-read sketch**. It is **not** a recipe you
can run end-to-end on Preview today.

Sampled Preview FS UTxOs looked **months-stale** at scout time (**Shaky**). Do
**not** treat public-read existence as proof that a short validity-range spend
will succeed. DIY Mesh attach of an FS reference input is **scaffolding only** —
**NOT RUN**, and **not expected to succeed** until someone re-probes freshness
(dated STATUS) or uses the upstream `orcfax-examples` **mock** path.

On-demand (Subbit + Mesh CIP-30 portal) is a **different product surface** —
paid, not an Aiken dApp starter.

## License

**MIT** — see [`LICENSE`](LICENSE). Copyright (c) 2026 Brady Sheldon.

## How to cite

- Package folder: `orcfax-preview-consume-sketch`
- Doc + scout verification date: **2026-09-27** (America/Los_Angeles)
- Sibling hello practice date: **2026-09-25** PT
- Network: **Cardano Preview** only for on-chain probe claims
- Do not cite as “live oracle E2E,” “currently spendable oracle attach,”
  “production Orcfax integration,” or “official Mesh/Aiken/Orcfax kit”
- Do not cite Shaky freshness samples as proof a short-validity spend works today
