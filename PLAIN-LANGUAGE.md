# Plain language — unpaid Orcfax Preview consume sketch

**Scope:** community learning explanation for Cardano **Preview**.  
**Not claimed:** production-ready, battle-tested, official, live oracle E2E, or
CIP-30. We verified public-read existence of Preview statements (scout) and
Mesh + Aiken hello (sibling). Live freshness-gated spend was **not run**.

**Non-executable expectation:** sampled statements were **months-stale**
(**Shaky**). Do **not** expect a DIY Mesh unlock that attaches an oracle
reference input to succeed on a short time window today. Re-probe freshness
first, or use Orcfax’s mock examples — this package is reading notes, not a
working spend drill.

For anyone who does not live in Cardano tooling all day.

## What problem this package talks about

You already know how to lock and unlock a tiny Aiken script with Mesh on
Preview (sibling hello). Now you want an **oracle fact** — for example an
exchange rate — to sit in the same transaction story as that unlock.

Orcfax is one Cardano-native oracle. This package only covers the **unpaid,
public-read** way to *look at* facts already sitting on Preview — not the
paid “ask for a fresh price now” portal.

## Two Orcfax doors (do not mix them up)

### Door A — Unpaid consume (this package)

1. Orcfax already published a **statement** into an on-chain box (a **UTxO**).
2. A special pointer box (**FSP**) tells you which script currently owns the
   authentic statement boxes (**FS**).
3. Anyone with a normal Cardano chain reader (Koios, Blockfrost free tier, a
   node) can find those boxes and decode the note:
   `feed_id`, `created_at`, and a body (for exchange rates: a fraction).
4. Your future dApp transaction **reads** that box as a **reference input**
   (look, don’t spend) while unlocking your own locked funds.

**You do not need an Orcfax API key for Door A.**  
You may still need a chain-provider key (Blockfrost etc.) — that is separate.

### Door B — On-demand portal (not unpaid, not this kit)

The `orcfax/on-demand` app lets a browser wallet open a **Subbit** L2 payment
channel, then pay per request (README prices e.g. `/api/prices` **0.01 ADA**,
`/api/publish` **5 ADA**). Mesh CIP-30 is used to connect the wallet **on that
oracle portal**.

That is **pay-per-use**, has a password-gated login surface, and is **not** an
Aiken dApp starter kit. Do not cite Door B as “the free Mesh+Aiken oracle kit.”

## What a statement looks like (plain)

Think of a sticky note taped to a coin purse:

- **feed_id** — which feed, e.g. `CER/MIN-ADA/3` (type / name / version)
- **created_at** — when Orcfax considered that fact true
- **body** — for current exchange rate (CER) feeds, a numerator / denominator

Your future validator decides whether that note is the **right feed** and
**fresh enough** for *your* business rules. Orcfax’s consume docs show the
shape; they do not replace your freshness window.

## What we actually saw on Preview (2026-09-27 PT scout)

| Observation | Confidence |
|-------------|------------|
| Official docs list Preview FSP / FS hashes | **Solid** |
| FSP UTxO exists; its datum points at the Active FS hash | **Solid** |
| Hundreds of FS-token UTxOs exist and decode as CER feeds | **Solid** |
| Newest sampled FS UTxO was from ~**April 2026** | **Solid** as sample; freshness for a *short* spend window today is **Shaky** |
| Mesh unlock that attaches an FS reference input | **NOT RUN** |

So: “can I learn the unpaid read path without paying Orcfax?” → **Yes.**  
“can I claim a live short-validity oracle spend on Preview today?” → **Not from
this package.**

## How this sits next to siblings

1. **hello** — proves Mesh can lock/unlock Aiken on Preview.  
2. **packaging-glue** — names oracle / Aiken / Mesh roles and the kit gap.  
3. **this sketch** — zooms into **one unpaid vendor path** (Orcfax public FS)
   without pretending the glue is finished.

## Confidence legend

- **Solid** — We saw it, ran it, or docs we re-fetched support it.
- **Shaky** — Reasonable inference or stale-sample risk; do not treat as green.
- **Unknown** — Not evidenced; do not invent numbers (TVL, users, uptime).

## One sentence for stakeholders

Unpaid Orcfax Preview consume is real as **public on-chain statement read via
FSP/FS** (no Orcfax API key); live short-validity Mesh spend and on-demand
Subbit portal are different stories — this package only documents the first.
