# Peer review pass (community second-reader)

**Date:** 2026-09-27 PT  
**Package:** `orcfax-preview-consume-sketch`  
**Verdict:** **PASS** on correctness + presentation for an unpaid Orcfax Preview
**public-read** learning sketch (docs-only)

## Brief

- Unpaid consume framed as on-chain FS UTxOs via FSP (no Orcfax API key);
  on-demand Subbit + Mesh CIP-30 portal correctly separated (paid; not an Aiken kit).
- Preview FSP/FS existence and sample CER feed_id decode match STATUS evidence.
- Sampled FS freshness labeled **Shaky** (newest sampled `block_time` ~2026-04-16 UTC).
- Live Mesh unlock attaching an FS reference input: **NOT RUN** / package is
  **non-executable** until a dated freshness re-probe (or upstream mock path).
- Docs-only / no CI; learning / scaffolding label intact.

## Links

- Scope and evidence: [`STATUS.md`](../STATUS.md)
- Pins: [`VERSIONS.md`](../VERSIONS.md)
- Front door: [`README.md`](../README.md)
