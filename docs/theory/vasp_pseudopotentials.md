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

# Pillar 1: Theoretical Foundations (Continuation)

## 1.3 Examples of Materials Modeling from First Principles (Continued)

### 1.3.1 Phase Diagrams from First Principles: Iron in the Earth's Core (Continued)
Calculating phase boundaries under extreme environments requires evaluating the thermodynamic stability of competing crystal structures. A classic example is determining the behavior of iron ($\text{Fe}$) at the center of the Earth under pressures approaching $350\ \text{GPa}$. 

* **The Thermodynamic Condition:** The determination of melting curves relies on the observation that when a solid and liquid phase coexist in thermodynamic equilibrium at a given temperature $T_m$ and pressure $p$, their corresponding Gibbs free energies are equal:
  
  $$G_s(p, T_m) = G_l(p, T_m)$$

* **Phase Stability:** At pressures above $10 \text{--} 15\ \text{GPa}$, iron crystallizes into a hexagonal close-packed (hcp) structure denoted as the **$\epsilon\text{-Fe}$ phase**. First-principles DFT calculations are used to compute the Gibbs energies for both the solid and liquid phases across a range of pressures and temperatures to find where these two energy surfaces intersect, successfully narrowing down experimental uncertainties.

---

## 2. Density Functional Theory: A Closer Look

### 2.1 The Many-Body Schrödinger Equation
To model any material, we begin with a microscopic description consisting of a collection of atomic nuclei and electrons interacting via Coulomb forces. The non-relativistic time-independent Schrödinger equation is written as:

$$\hat{H} \Psi = E \Psi$$

Where $\hat{H}$ is the many-body Hamiltonian operator, $\Psi$ is the many-body wavefunction, and $E$ is the total energy of the system. The full Hamiltonian for a system of $N$ electrons and $M$ nuclei is given by:

$$\hat{H} = -\frac{\hbar^2}{2m_e} \sum_i \nabla_i^2 - \sum_{i,I} \frac{Z_I e^2}{4\pi\epsilon_0 |\vec{r}_i - \vec{R}_I|} + \frac{1}{2} \sum_{i \neq j} \frac{e^2}{4\pi\epsilon_0 |\vec{r}_i - \vec{r}_j|} - \sum_I \frac{\hbar^2}{2M_I} \nabla_I^2 + \frac{1}{2} \sum_{I \neq J} \frac{Z_I Z_J e^2}{4\pi\epsilon_0 |\vec{R}_I - \vec{R}_J|}$$

Where:
* $m_e$ and $e$ represent the mass and charge of an electron.
* $M_I$ and $Z_I$ represent the mass and atomic number of the $I$-th nucleus.
* $\vec{r}_i$ and $\vec{R}_I$ are the spatial coordinates of the $i$-th electron and $I$-th nucleus, respectively.

### 2.2 The Born-Oppenheimer Approximation
Because nuclei are vastly heavier than electrons (e.g., a single proton is roughly 1,836 times heavier than an electron), the electrons respond almost instantaneously to any nuclear motion. Consequently, we can separate their degrees of freedom:

1. **Electronic Sub-Problem:** Electrons are assumed to move in a static external potential $V_{\text{ext}}(\vec{r})$ generated by frozen nuclear positions. The nuclear kinetic energy term drops out, and the nuclear-nuclear repulsion acts as a constant energy shift.
2. **Simplified Electronic Hamiltonian:**
   
   $$\hat{H}_{\text{elec}} = -\frac{\hbar^2}{2m_e} \sum_i \nabla_i^2 + \sum_i V_{\text{ext}}(\vec{r}_i) + \frac{1}{2} \sum_{i \neq j} \frac{e^2}{4\pi\epsilon_0 |\vec{r}_i - \vec{r}_j|}$$

Even with this approximation, the electron-electron interaction term couples the motion of all electrons together, making it an impossible task to solve the wavefunction directly for realistic materials containing $10^{23}$ particles.

---

## 3. The Hohenberg-Kohn Theorems & Kohn-Sham Formulation

### 3.1 The Reduction to Electron Density
Density Functional Theory alters this paradigm by using the **electron probability density $n(\vec{r})$** as the fundamental variable instead of the many-body wavefunction $\Psi$. The electron density is defined as the integral over the spin and spatial coordinates of all but one electron:

$$n(\vec{r}) = N \int \dots \int |\Psi(\vec{r}, \vec{r}_2, \dots, \vec{r}_N)|^2 d\vec{r}_2 \dots d\vec{r}_N$$

### 3.2 The Core Theorems
* **Hohenberg-Kohn Theorem I (1964):** Asserts that the ground-state electron density $n(\vec{r})$ uniquely determines the external potential $V_{\text{ext}}(\vec{r})$ up to an arbitrary additive constant. Therefore, the total ground-state energy can be expressed as a unique functional of the density: $E[n]$.
* **Hohenberg-Kohn Theorem II:** Establishes a variational principle. The energy functional $E[n]$ reaches its global minimum if and only if the input density is the true ground-state density of the system.

$$E[n] = T[n] + E_{\text{H}}[n] + E_{\text{ext}}[n] + E_{\text{xc}}[n]$$

Where $T[n]$ is the kinetic energy of non-interacting electrons, $E_{\text{H}}[n]$ is the classical Hartree electrostatic energy, $E_{\text{ext}}[n]$ is the interaction energy with the external potential, and $E_{\text{xc}}[n]$ captures all non-trivial many-body Exchange-Correlation effects.

---

## 4. The Kohn-Sham Self-Consistent Equations

To solve this practically, Kohn and Sham introduced fictitious single-particle wavefunctions (orbitals $\psi_i$) whose collective density matches the real system:

$$n(\vec{r}) = \sum_i |\psi_i(\vec{r})|^2$$

This yields the single-particle **Kohn-Sham Equations**:

$$\left[ -\frac{\hbar^2}{2m_e}\nabla^2 + V_{\text{eff}}(\vec{r}) \right] \psi_i(\vec{r}) = \epsilon_i \psi_i(\vec{r})$$

Where the effective potential $V_{\text{eff}}(\vec{r})$ is defined as:

$$V_{\text{eff}}(\vec{r}) = V_{\text{ext}}(\vec{r}) + e^2 \int \frac{n(\vec{r}')}{4\pi\epsilon_0 |\vec{r} - \vec{r}'|} d\vec{r}' + V_{\text{xc}}(\vec{r})$$

Because $V_{\text{eff}}$ depends directly on the electron density $n(\vec{r})$, which itself is constructed from the output orbitals $\psi_i$, these equations must be solved iteratively via a **Self-Consistent Field (SCF) loop**.
