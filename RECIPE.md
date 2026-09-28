# RECIPE — honest DIY Mesh reference-input path (Orcfax Preview)

**Type:** community scaffolding recipe (learning docs), **not** a copy-paste
live oracle E2E.  
**Verified base:** sibling Mesh + Aiken hello on **Preview**; scout public-read
probe of Preview FSP/FS (2026-09-27 PT).  
**Not claimed:** unpaid live freshness-gated spend, CIP-30, mainnet, or a
finished starter kit.

**Non-executable until re-probe:** sampled FS UTxOs were **months-stale**
(**Shaky**, ~2026-04). Steps labeled “later DIY” Mesh attach / Aiken freshness
/ short-validity spend are **NOT RUN** and are **not expected to succeed today**.
Re-probe freshness into STATUS, or use the upstream mock path, before treating
those steps as a working drill.

## Goal

After reading this, you can point to each step of:

```
choose Preview FSP (docs / VERSIONS)
  → locate FSP UTxO (public indexer / provider)
  → extract Active FS script hash from FSP datum
  → find an FS-token UTxO + decode statement (feed_id, created_at, body)
  → (later DIY) Mesh unlock attaches readOnlyTxInReference(fsTxHash, index)
  → (later DIY) Aiken checks feed_id prefix + freshness window
  → Blockfrost / explorer confirm
```

Steps through “decode statement” are **Solid** as public-read / docs.  
Mesh attach + Aiken freshness validator + short-validity spend are **DIY /
NOT RUN** in this package.

## 0. Preconditions

- Sibling hello understood: `cardano-preview-mesh-aiken-hello` (https://github.com/booper-labs/cardano-preview-mesh-aiken-hello)
- Packaging map understood: `cardano-packaging-glue-starter`
- Cardano **Preview** chain access (Koios public **or** Blockfrost Preview
  project id — **never commit** the project id)
- Node.js **20.x**, `@meshsdk/core` **1.9.1**, Aiken **v1.1.23**, stdlib **v3**
  (practice pins — see `VERSIONS.md`)
- **No** Orcfax API key required for unpaid consume
- **No** Subbit channel / on-demand login required for unpaid consume

## 1. Documented Preview deployments (Solid — docs 2026-09-27 PT)

From https://docs.orcfax.io/consume (Deployments table) and
https://docs.orcfax.io/deployments (v1 Preview **Active**):

| Item | Value |
|------|-------|
| Preview **FSP** (Active) | `0690081bc113f74e04640ea78a87d88abbd2f18831c44c4064524230` |
| Preview **FS** (Active) | `e6c8a314ae942401619460f00c69de3d1b996db588d4042243a4b259` |
| Preview **C** | `3a81e444b7b88e41d421551d056ce1e7701948236251019d6fdce656` |
| FSP script NFT name | `000de140` (CIP-67) |
| FS token name | empty bytearray |

Integrators use **FSP + FS**. Constitution (**C**) is for Orcfax publish
signing checks — **not** something integrators consume (consume docs).

## 2. Unpaid public-read steps (Solid shape; probe evidence in STATUS)

Official consume integrator steps (paraphrased):

1. Verify **FSP** UTxO from reference inputs (or off-chain locate it first).
2. Extract **FS script hash** from FSP inline datum (`FspDat = ByteArray`).
3. Find reference input(s) holding an **FS token** (empty token name).
4. Parse FS inline datum → `Statement { feed_id, created_at, body }`.
5. Prefix-match `feed_id` (include trailing `/` after the feed name).
6. Enforce **your** freshness rules against `created_at` (often: short tx
   validity range + `created_at` inside that range).

**Public-once-published:** https://docs.orcfax.io/feed-use — once a feed
results in a published datum, that data is publicly available to the network
by design. Production ToS still applies for production use — learning Preview
read ≠ production partnership.

### Scout probe snapshot (2026-09-27 PT, Koios Preview — no Orcfax key)

| Check | Result |
|-------|--------|
| FSP asset holder / UTxO | Present |
| FSP datum → FS hash | Matches Active FS `e6c8a314…4b259` |
| FS-token UTxOs | **278** unspent at FS script address |
| Sample `feed_id`s | `CER/ENCS-ADA/3`, `CER/SURF-ADA/3`, `CER/MIN-ADA/3` |
| Newest sampled FS `block_time` | **~2026-04-16 UTC** |

**Implication:** discovery + decode works. A short (~1h) validity-range spend
against that sample is **not** something this package claims will succeed.

## 3. Where Mesh would attach (DIY — NOT RUN)

Reuse the packaging-glue comments-only stub placement:

`cardano-packaging-glue-starter` → `stub/oracle-read.sketch.ts`

Keep the hello unlock pieces:

- `spendingPlutusScriptV3` + blueprint script
- `txInInlineDatumPresent` (do **not** also `txInDatumValue`)
- matching redeemer + `requiredSignerHash` if owner-gated
- collateral UTxO (~5 ADA)
- MeshWallet UTxO fetch (base change address)

Add **later** (not shipped live here):

```ts
// Pseudocode only — do not treat as a verified E2E
// const fsRef = await resolveFsStatementUtxo(/* feed_id prefix, freshness */);
// txBuilder.readOnlyTxInReference(fsRef.txHash, fsRef.index);
```

Off-chain resolve means: query your provider for the FSP UTxO, then for an
FS-token UTxO whose datum matches your feed prefix and freshness window.
Document which provider you used; do **not** invent a vendor “oracle REST API
key” for unpaid consume.

## 4. Aiken freshness shape (described only — NOT RUN)

Consume docs: verify `feed_id` **prefix** (with trailing `/`) and enforce
business freshness on `created_at`. CER body type is a `Rational { num, denom }`.

Upstream helpers:

| Repo | Role | Caveat |
|------|------|--------|
| `orcfax/orcfax-aiken` | Aiken types / helpers | `aiken.toml` pins stdlib **1.9.0**; practice hello uses stdlib **v3** — **Shaky** drop-in; re-check before paste |
| `orcfax/orcfax-examples` | Demo dApps + **mock** publish; Deno off-chain | Marked WIP / demo only; **not Mesh** |

Do **not** claim a Mesh+Aiken+Orcfax unified official starter exists because
these repos exist.

## 5. Suggested DIY order (when expanding beyond this sketch)

1. Re-run sibling hello lock/unlock until boring.
2. Re-probe Preview FS freshness (or use `orcfax-examples` **mock**).
3. Only if a statement is inside your chosen window: write a tiny Aiken check
   (feed_id prefix + freshness) — no product economics.
4. Extend Mesh unlock with `readOnlyTxInReference`.
5. CIP-30 browser signing only after CLI MeshWallet path works.
6. Keep secrets out of git; Preview only until unpaid public freshness is Solid.

## 6. Explicit non-goals for this recipe

- No live feed spend / unlock with oracle ref input submitted from this tree
- No Subbit / on-demand payment channel setup
- No inventing feed ids, tx hashes, TVL, or user counts
- No claiming on-demand Mesh CIP-30 portal = Aiken dApp kit
- No assertion that Midnight Compact closes this L1 oracle packaging gap
