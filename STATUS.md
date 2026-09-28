# STATUS — verification log (orcfax-preview-consume-sketch)

**As-of:** 2026-09-27 ~06:52 PT (package assemble + Orcfax URL re-fetch); RAISE soft scrub evening 2026-09-27 PT  
**Public-read probe:** 2026-09-27 ~06:51 PT  
**Sibling hello practice:** 2026-09-25 PT  
**Label:** community learning / scaffolding docs — **Preview** / **docs + unpaid public-read**  
**Not claimed:** battle-tested, production-ready, audited, mainnet, official,
live oracle E2E, CIP-30

## Matrix

| Check | Result | Notes |
|-------|--------|-------|
| Orcfax consume docs (Preview FSP listed) | **PASS** (docs) | WebFetch 2026-09-27 PT |
| Orcfax deployments Active Preview FSP/FS/C | **PASS** (docs) | https://docs.orcfax.io/deployments |
| Feed-use “public once published” | **PASS** (docs) | https://docs.orcfax.io/feed-use |
| Unpaid consume needs Orcfax API key? | **NO** (Solid) | On-chain FS via FSP; no Orcfax key |
| On-demand unpaid? | **FAIL as unpaid** | Subbit pay-per-use; Mesh CIP-30 **portal** only |
| Preview FSP UTxO exists (public Koios) | **PASS** (probe) | FSP datum → FS `e6c8a314…4b259` |
| Preview FS-token UTxOs exist (public Koios) | **PASS** (probe) | 278 unspent sampled |
| Sample CER feed_id decode | **PASS** (probe) | e.g. `CER/MIN-ADA/3` |
| Fresh statement inside short validity window **today** | **NOT PROVEN** | Newest sampled FS block_time ~2026-04-16 UTC — **Shaky** |
| Mesh unlock + Orcfax ref input on Preview | **NOT RUN** | Explicit non-goal for sketch v0 |
| Aiken feed_id + freshness validator (this tree) | **NOT RUN** | Docs/pointer only |
| orcfax-aiken stdlib vs practice v3 | **Shaky** | Upstream `1.9.0`; practice `v3` |
| Sibling Mesh + Aiken hello baseline | **PASS** (sibling) | `cardano-preview-mesh-aiken-hello` |
| CIP-30 | **NOT RUN** | |
| Mainnet / TVL / users | **NOT CLAIMED** | Unknown |

## External URL re-fetch (2026-09-27 PT)

| URL | Result |
|-----|--------|
| https://docs.orcfax.io/consume | **Live** (Preview FSP `0690081b…4230` listed) |
| https://docs.orcfax.io/deployments | **Live** (Active Preview FSP/FS/C match VERSIONS) |
| https://docs.orcfax.io/feed-use | **Live** (public-once-published) |
| https://raw.githubusercontent.com/orcfax/on-demand/main/README.md | **Live** (Subbit; Mesh CIP-30; 0.01 / 5 ADA prices) |
| https://raw.githubusercontent.com/orcfax/orcfax-aiken/main/aiken.toml | **Live** (stdlib **1.9.0**) |
| https://raw.githubusercontent.com/orcfax/orcfax-examples/main/README.md | **Live** (WIP / demo; Aiken + Deno; mock) |
| https://github.com/orcfax/on-demand | **Live** (repo front door) |
| https://github.com/orcfax/orcfax-examples | **Live** (repo front door) |

## Artifacts in this folder

| Path | Role |
|------|------|
| `README.md` | Front door / scope |
| `PLAIN-LANGUAGE.md` | Non-expert explanation |
| `RECIPE.md` | DIY Mesh reference-input scaffolding |
| `GOTCHA.md` | Gotchas + link stamps |
| `VERSIONS.md` | Documented FSP/FS + practice pins |
| `STATUS.md` | This evidence log |
| `SECURITY.md` | How to report problems |
| `audits/peer-review-pass.md` | Peer review pass (correctness / presentation) |
| `LICENSE` | MIT |

## Secrets

None. No wallet seeds, mnemonics, private keys, Orcfax credentials, Subbit
credentials, or Blockfrost project ids in this folder.

## Publishing stance

Community learning package under **MIT**. Docs-only / no CI / unpaid public-read
sketch. No upstream issues are filed from this package unless the maintainer asks.

**Sibling note:** `cardano-preview-mesh-aiken-hello` (live at
https://github.com/booper-labs/cardano-preview-mesh-aiken-hello) and
`cardano-packaging-glue-starter` are separate sibling packages (named in prose
only). Upstream scout notes stay private.
