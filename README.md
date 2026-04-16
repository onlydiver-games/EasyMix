# EasyMix
Mixing scale up calculation tool
https://onlydiver-games.github.io/EasyMix/


# Mixing Scale-Up Toolkit

A browser-based tool for chemical engineers scaling up agitated tank operations from lab to pilot or production scale. Enter the geometry and conditions of two tanks and get dimensionless mixing parameters, scale-up criterion recommendations, feasibility analysis, and heat transfer estimates — all in one place, with inline explanations of the underlying correlations and their validity conditions.


---

## What it does

Given two tanks at different scales, the tool answers the core scale-up question: *what agitator speed should I set at large scale to preserve the mixing behavior that matters for my process?*

It calculates Reynolds number, P/V, tip speed, blend time, Kolmogorov scale, Zwietering N_js, k_La, and a dozen other parameters at both scales simultaneously, shows you how each one changes, and tells you which scale-up criteria are valid given your geometry and flow regime. Every parameter has an inline tooltip with its definition, the correlation used, validity conditions, and a literature citation.

---

## Getting started

Select a **process context** before entering any geometry — this is the most important first step. The context controls which inputs are shown, which parameters are highlighted, and which scale-up criterion is pre-selected:

- **General / blending** — bulk homogeneity, blend time, circulation
- **Gas-liquid** — sparged aeration, k_La, flooding limits, OTR vs demand
- **Solid-liquid** — particle suspension, Zwietering N_js, C/T sensitivity
- **3-phase** — simultaneous suspension + aeration constraints with feasibility window
- **Shear-sensitive** — tip speed as the binding constraint, Kolmogorov scale vs cell/crystal size
- **Heat transfer limited** — jacket and coil area vs heat generation at scale

Then fill in the small-scale tank (your reference), the large-scale tank (your target), and fluid properties. The **recommended agitator speed** for the large scale appears prominently at the top of the output panel and updates live.

---

## Workflow

1. **Set context** → activates relevant inputs and pre-selects the appropriate scale-up criterion
2. **Enter small-scale geometry** — T, H, D, C, impeller type, baffles, internal obstructions
3. **Enter large-scale geometry** — same fields; geometric similarity score is calculated automatically
4. **Enter fluid properties** — Newtonian, power-law, or Bingham plastic; slurry viscosity correction applied automatically in solid-liquid contexts
5. **Check the Parameters tab** — all mixing parameters side by side with ratio pills; blue-highlighted cards are most relevant to your context
6. **Read the Scale-Up tab** — recommended N for all six criteria simultaneously; locked criteria are explicitly marked when geometry or regime makes them inapplicable
7. **Check the Feasibility tab** (gas/solid contexts) — the valid N window where all constraints are satisfied at once; for 3-phase systems this shows where suspension, flooding, and OTR constraints overlap
8. **Review Trade-offs** — sweeps N across the full operating range so you can see how P/V, blend time, tip speed, k_La, and N_flood move together
9. **Check Heat Transfer** (if relevant) — jacket + coil + electrical heater balance at each scale, with area-per-volume comparison
10. **Use Sensitivity** — drag viscosity/density sliders to see how regime and parameters respond to fluid property variation

---

## Key concepts the tool handles

**Geometric similarity score** rates how closely the two tanks match on D/T, H/T, C/T, and baffle w/T. Below 60/100, scale-up criteria that require geometric similarity are locked with an explanation of why. The tool still calculates what it can, but is explicit about what is no longer reliable.

**Damköhler number** (enabled when "mixing involves a reaction" is checked) computes Da = blend time / reaction half-life at both scales. Da << 1 means mixing is not limiting and criterion choice matters little. Da >> 1 means local mixing quality controls yield and selectivity — equal blend time becomes the appropriate criterion regardless of energy cost.

**3-phase feasibility window** maps three simultaneous constraints against N: solids must be suspended (N ≥ N_js), gas must not flood the impeller (N ≤ N_flood), and oxygen transfer must meet demand (k_La × C* ≥ OTR). These constraints pull in opposite directions and the valid window can be narrow or nonexistent. When no window exists, the tool explains what geometry changes would create one.

**Heat transfer** accounts for jacket coverage %, cooling coils, heating coils, heat transfer plates, and electrical resistance heaters separately, each with its own ΔT. The fundamental scale-up challenge — that heat generation scales as T³ while jacket area scales as T² — is quantified numerically at both scales.

---

## Limitations

The correlations in this tool are lumped-parameter models calibrated for standard geometries in turbulent, baffled, single-phase (or pseudo-single-phase) operation. Validity conditions are shown on every parameter tooltip. Situations where accuracy degrades include: transitional or laminar flow, non-standard D/T or C/T ratios, highly non-Newtonian or viscoelastic fluids, high solids loading (> ~20 wt%), non-coalescent media for k_La, and geometric dissimilarity between scales. The tool flags most of these with warnings, but does not eliminate the need for pilot-scale validation before committing to production equipment.
