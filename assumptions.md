# Monte Carlo Assumptions — Private Prisons / Occupancy Guarantee Trap

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
| Private payoff Π | $8.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 12.08 | Confirmed by N=100,000 draws |
| ΔW median (result) | $96.7B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_over_incarceration` | lognormal | $21.0B | $38.1B | $62.9B | Lobbying for longer sentences, mandatory minimums. Private prison occupancy guar |
| `C2_human_capital_destruction` | lognormal | $13.1B | $23.8B | $39.3B | Recidivism, intergenerational transmission of incarceration. Lost earnings, fami |
| `C3_monopoly_captive_extraction` | normal | $15.2B | $19.0B | $22.8B | Price gouging on phone calls, commissary, medical co-pays in captive market. Sou |
| `C4_institutional_defense_failure` | lognormal | $5.2B | $9.5B | $15.7B | Inadequate healthcare, understaffing, violence. DOJ consent decrees. Sources: DO |
| `C5_governance_political_feedback` | lognormal | $2.6B | $4.8B | $7.9B | Campaign contributions, ALEC model legislation, revolving door. Sources: Justice |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 6.5 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 6.5) = 0.0300%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 11.9 | 20% DC adj = 9.52 | 40% DC adj = 7.14

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $97B = 0.1% of world GDP ($106T) ✓
- **β_W range**: 12.08 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
