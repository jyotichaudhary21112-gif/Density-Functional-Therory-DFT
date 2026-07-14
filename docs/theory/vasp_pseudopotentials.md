# VASP Reference: Transition Metal Suffix Classes & Selection Guide

When selecting pseudopotentials (`POTCAR`) for elements in VASP—especially transition metals like Chromium (`Cr`)—the files are classified by distinct suffixes. These suffixes indicate how deep semi-core electronic states are treated relative to the core or the valence shell. 

Choosing the correct variant is critical for balancing computational speed with physical accuracy.

---

## 1. Suffix Classification Table

| Suffix Class | Explicit Valence Configuration | Intended Simulation Context |
| :--- | :--- | :--- |
| **`Cr`** (Standard) | $3d^5 4s^1$ | **Standard bulk calculations.** Best used near equilibrium volume. It skips deeper semi-core states to minimize computational costs. |
| **`Cr_pv`** (Semi-Core $p$) | $3p^6 3d^5 4s^1$ | **Highly Recommended for surface slabs, work functions, high strain, and mechanical tests.** It explicitly treats the $3p$ valence shell, which is necessary when bonds are distorted or fields are applied. |
| **`Cr_sv`** (Semi-Core $s,p$) | $3s^2 3p^6 3d^5 4s^1$ | **Extreme environments.** Intended for ultra-high-pressure configurations, highly compressed bulk states, or complex multi-species oxides where deep core states polarize. |
| **`Cr_sv_GW`** (GW Optimized) | $3s^2 3p^6 3d^5 4s^1$ + Unoccupied states | **Many-body perturbation theory.** Specially optimized with high-energy unoccupied state descriptors for excited-state GW band structures. |

---

## 2. Selection Strategy Guidelines

1. **For Slab & Surface Calculations (e.g., Work Functions):** Always default to the **`_pv`** version if available for your transition metal. When you create a surface, the sudden drop in electronic density requires the valence profile to have flexibility, which standard potentials lack.
2. **For High-Pressure Phase Diagrams:** Use **`_pv`** or **`_sv`**. Under high pressures (like Earth's core conditions), atoms are pushed close enough that their inner core electronic shells begin to overlap and interact.
3. **Consistency Check:** Ensure that if you change to a `_pv` potential for a convergence test, you use the exact same POTCAR variant across all related runs (bulk references, slabs, and defect systems) to prevent energetic mismatch.
