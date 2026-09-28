# GOTCHA — Orcfax Preview unpaid consume sketch

**Type:** community packaging notes / learning scaffold  
**Scope verified (docs + scout probe, 2026-09-27 PT):** Orcfax consume,
deployments, feed-use, on-demand README, orcfax-aiken `aiken.toml`,
orcfax-examples README; Koios Preview FSP/FS public-read  
**Scope verified (sibling practice, 2026-09-25 PT):** Aiken **v1.1.23**,
`@meshsdk/core@1.9.1`, Node **20**, Blockfrost **Preview**, hello lock/unlock  
**Not claimed:** live oracle E2E, CIP-30 in this spike, mainnet, production audit

## Contents

1. [Unpaid consume vs on-demand (Solid)](#1-unpaid-consume-vs-on-demand-solid)
2. [Freshness trap (Shaky for short spends)](#2-freshness-trap-shaky-for-short-spends)
3. [stdlib pin skew (Shaky)](#3-stdlib-pin-skew-shaky)
4. [Hello-path gotchas that still apply](#4-hello-path-gotchas-that-still-apply)
5. [Vendor / link stamps](#5-vendor--link-stamps)
6. [Honest limits + residual Unknowns](#6-honest-limits--residual-unknowns)

## 1. Unpaid consume vs on-demand (Solid)

| Surface | Gate | What it is |
|---------|------|------------|
| **Unpaid consume** | No Orcfax API key | Read on-chain FS UTxOs via FSP; public once published (feed-use) |
| **On-demand portal** (`orcfax/on-demand`) | Subbit L2 pay-per-use; password-gated login route | Mesh SDK CIP-30 wallet **on the oracle portal** — **not** an Aiken dApp starter |
| **Blockfrost / Koios / node** | Separate from Orcfax | Needed to *see* chain state; free Preview tiers OK for learning |

**Oversell (forbidden):** citing on-demand Mesh CIP-30 as “the Mesh+Aiken
oracle kit,” or claiming unpaid consume requires an Orcfax API key.

README prices stamped from on-demand README (2026-09-27 PT): `/api/prices`
**0.01 ADA/req**, `/api/publish` **5 ADA/req**.

## 2. Freshness trap (Shaky for short spends)

Consume docs suggest integrators may:

1. Keep the transaction validity range short (example: ~1h)
2. Require `created_at` inside that range

Scout sample (Koios Preview, 2026-09-27 PT): newest FS UTxO `block_time` in
sample ≈ **2026-04-16 UTC** (~5 months before scout). Existence of FS UTxOs is
**Solid**; suitability for a short-validity drill **today** is **Shaky**.

**Mitigation before claiming live attach:**

- Re-probe Preview publish cadence and pick a statement inside your window, **or**
- Use `orcfax-examples` **mock** publish for local drills, then label the STATUS
  row honestly

**Live short-validity Mesh unlock with Orcfax ref input: NOT RUN** in this tree.

## 3. stdlib pin skew (Shaky)

| Pin | Value | Source |
|-----|-------|--------|
| Practice hello stdlib | **v3** | sibling `cardano-preview-mesh-aiken-hello` |
| Practice Aiken CLI | **v1.1.23** | same |
| `orcfax/orcfax-aiken` dependency | stdlib **1.9.0** | `aiken.toml` main, WebFetch 2026-09-27 PT |

Treat helper drop-in as **compatibility re-check required**. Do not paste
blindly into a v3 practice tree and call it verified.

`orcfax-examples` is **WIP / demo only**; off-chain is **Deno**, not Mesh.

## 4. Hello-path gotchas that still apply

These bit sibling Preview hello unlock and transfer when you attach oracle
reference inputs (details also in packaging-glue `GOTCHA.md`):

1. **Enterprise vs base address** — prefer MeshWallet UTxO fetch  
2. **Inline vs supplemental datum** — `txInInlineDatumPresent` only; no
   `txInDatumValue` when inline already present (`NotAllowedSupplementalDatums`)  
3. **Collateral** — distinct ~5 ADA UTxO for script spends  
4. **Redeemer encoding** must match Aiken types  
5. **Toolchain** — pin stdlib **v3**; TypeScript **5.8.x** for `ts-node`;
   `aikup` can hit GitHub rate limits (practice used release tarball)  
6. **Do not mix Midnight Compact** into this L1 oracle + Aiken + Mesh kit

## 5. Vendor / link stamps

Link checks performed **2026-09-27 PT** via WebFetch unless noted.

| Source | URL | Relevance | Link check |
|--------|-----|-----------|------------|
| Orcfax consume | https://docs.orcfax.io/consume | Integrator steps; Preview FSP in Deployments | **Live** |
| Orcfax deployments | https://docs.orcfax.io/deployments | Active Preview FSP/FS/C | **Live** |
| Orcfax feed-use | https://docs.orcfax.io/feed-use | Public-once-published stance | **Live** |
| Orcfax on-demand README | https://raw.githubusercontent.com/orcfax/on-demand/main/README.md | Subbit pay-per-use; Mesh CIP-30 portal | **Live** |
| orcfax-aiken aiken.toml | https://raw.githubusercontent.com/orcfax/orcfax-aiken/main/aiken.toml | stdlib **1.9.0** pin | **Live** |
| orcfax-examples README | https://raw.githubusercontent.com/orcfax/orcfax-examples/main/README.md | WIP / demo; Aiken + Deno; mock | **Live** |
| Mesh — Aiken overview | https://meshjs.dev/aiken | Hello baseline docs | **Live** (sibling stamp) |
| Packaging-glue stub | `cardano-packaging-glue-starter` / `stub/oracle-read.sketch.ts` | Comments-only Mesh attach point | Sibling package |

## 6. Honest limits + residual Unknowns

| Item | Grade |
|------|-------|
| Mesh unlock + Orcfax ref input on Preview | **NOT RUN** |
| Aiken feed_id + freshness validator in this tree | **NOT RUN** |
| CIP-30 browser wallet | **NOT RUN** (hello used MeshWallet + CLI skey) |
| Charli3 unpaid Preview Push UTxO ready | **Unknown** (not re-verified this pass) |
| Identity / compliance attribute oracles | **Unknown** |
| TVL / MAU / consumer counts | **Unknown** — do not invent |
| Preview FS publish cadence going forward | **Unknown** — re-probe before live claims |
| Undiscovered Catalyst / unofficial one-kits | **Unknown** residual (packaging-glue gap framing) |
