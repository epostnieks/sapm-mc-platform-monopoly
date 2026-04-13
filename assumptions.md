# Monte Carlo Assumptions — Platform Monopoly / Gatekeeper Ratchet

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $158.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 6.33 | Confirmed by N=100,000 draws |
| ΔW median (result) | $999.4B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_supracompetitive_pricing` | normal | $120.0B | $195.0B | $270.0B | CMA ROCE-WACC spread: search ad overcharge $35B + social media $39.5B + app stor |
| `C2_innovation_kill_zone` | lognormal | $60.0B | $120.0B | $180.0B | K-R-Z 46% VC suppression × 3x innovation multiplier + killer acquisition project |
| `C3_data_extraction_privacy` | lognormal | $120.0B | $240.0B | $360.0B | WTA $960/yr × 250M adults; cross-checked via Meta ARPU and macro ad-spend |
| `C4_publisher_creator_destruction` | lognormal | $45.0B | $85.0B | $125.0B | JCPA $11B US journalism + $40B global publisher deficit + $20B local news + $14B |
| `C5_small_business_dependency` | normal | $120.0B | $200.0B | $280.0B | ILSR Amazon $185B extraction: $100B monopoly rent + $50B mandatory ad tax + $35B |
| `C6_governance_regulatory_capture` | lognormal | $80.0B | $150.0B | $220.0B | Blocked legislation $80B + institutional capture $30B + democratic integrity $25 |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 2.8 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 2.8) = 0.0020%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 6.27 | 20% DC adj = 5.01 | 40% DC adj = 3.76

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $999B = 0.9% of world GDP ($106T) ✓
- **β_W range**: 6.33 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
