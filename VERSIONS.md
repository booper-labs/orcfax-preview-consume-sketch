# VERSIONS — pins and documented Preview ids

**Scope:** what we **documented / probed** for the unpaid Orcfax Preview
consume sketch.  
**Do not treat** as a live integration pin set until a STATUS row shows a
Mesh+Orcfax re-run.

## Documented protocol (Solid — docs re-fetched 2026-09-27 PT)

| Component | Value | Notes |
|-----------|-------|-------|
| Network (target) | **Cardano Preview** | Sketch only |
| Orcfax Preview FSP (Active) | `0690081bc113f74e04640ea78a87d88abbd2f18831c44c4064524230` | consume Deployments + `/deployments` |
| Orcfax Preview FS (Active) | `e6c8a314ae942401619460f00c69de3d1b996db588d4042243a4b259` | `/deployments`; scout FSP datum match |
| Orcfax Preview C | `3a81e444b7b88e41d421551d056ce1e7701948236251019d6fdce656` | not used by integrators |
| FSP token name | `000de140` | CIP-67 script NFT |
| FS token name | empty bytearray | authenticity check |

## Practice baseline (sibling hello — not re-run in this tree)

| Component | Version | Notes |
|-----------|---------|-------|
| Aiken CLI | **v1.1.23** | `cardano-preview-mesh-aiken-hello` (https://github.com/booper-labs/cardano-preview-mesh-aiken-hello) |
| Aiken stdlib | **v3** | `orcfax-aiken` upstream cites **1.9.0** — re-check |
| Plutus | **V3** | hello_world spend |
| `@meshsdk/core` | **1.9.1** | Mesh attach still DIY here |
| Node.js | **20.x** (practice **v20.19.2**) | |
| TypeScript | **5.8.x** | for `ts-node` |
| Provider (hello) | Blockfrost Preview | project id never committed |
| Wallet signing (hello) | MeshWallet + CLI payment skey | CIP-30 **not** exercised |

## Upstream references (existence — not vendored here)

| Repo / doc | Role | Caveat |
|------------|------|--------|
| `orcfax/orcfax-aiken` | Aiken types/helpers | stdlib **1.9.0** vs practice **v3** |
| `orcfax/orcfax-examples` | Demo dApps + **mock** publish; Deno off-chain | WIP / demo only; not Mesh |
| `orcfax/on-demand` | Portal + Subbit pay-per-use | **Not unpaid**; CIP-30 portal ≠ Aiken kit |
| docs.orcfax.io/consume | Integrator steps | Re-fetched 2026-09-27 PT |
| docs.orcfax.io/deployments | Active Preview hashes | Re-fetched 2026-09-27 PT |
| docs.orcfax.io/feed-use | Public-once-published | Re-fetched 2026-09-27 PT |

## Sibling practice transaction artifacts (Preview — cite hello package)

| Step | Tx hash (full) | Block |
|------|----------------|-------|
| Lock | `ebdc1565c39b6d295736317634bcb019a65860ce787669058010b005f6dd569c` | 4697224 |
| Unlock | `b7e23631f73db4a5a7913001dbbfd7cb57ad48d63ef043c4bd9d71f7f524d975` | 4697227 |

These prove Mesh↔Aiken hello only — **not** an oracle reference-input spend.

## Live oracle call

**none** — out of scope for this sketch package v0.

## Doc verification date

External Orcfax URLs re-fetched **2026-09-27** (America/Los_Angeles).  
Sibling hello practice runs dated **2026-09-25** PT.
