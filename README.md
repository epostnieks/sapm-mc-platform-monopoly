# SAPM Monte Carlo — Platform Monopoly / Gatekeeper Ratchet

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Platform Monopoly (Gatekeeper Ratchet).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **6.33** |
| β_W mean | 6.37 |
| β_W std | 1.01 |
| **90% CI** | **[4.8, 8.1]** |
| 99% CI | [4.2, 9.0] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$999.4B/yr** |
| Π (revenue) | $158.0B/yr |

**β_W = 6.33** means the platform monopoly industry destroys **$6.33 in system
welfare for every $1.00 in revenue** — across 6 channels and 100,000 Monte Carlo draws.

**Classification**: Class 2 — Intractability

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-platform-monopoly.git
cd sapm-mc-platform-monopoly
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 6.33` and `ΔW median : $999.4B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_supracompetitive_pricing | $194.7B | [$119.5B, $269.7B] | Normal |
| C2_innovation_kill_zone | $119.9B | [$79.9B, $180.5B] | Lognormal |
| C3_data_extraction_privacy | $239.9B | [$160.0B, $359.8B] | Lognormal |
| C4_publisher_creator_destruction | $85.1B | [$57.7B, $124.9B] | Lognormal |
| C5_small_business_dependency | $199.7B | [$120.3B, $279.4B] | Normal |
| C6_governance_regulatory_capture | $149.9B | [$102.4B, $220.0B] | Lognormal |
| **Total ΔW** | **$999.4B** | **[$758.5B, $1,282.9B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 2.8 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0020%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Platform Monopoly (Gatekeeper Ratchet)*.
> GitHub: epostnieks/sapm-mc-platform-monopoly.
> https://github.com/epostnieks/sapm-mc-platform-monopoly
