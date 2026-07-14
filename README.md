# ⚛️ DFT & Materials Theory: Knowledge Base

Welcome! This repository serves as my personal technical reference and research hub for **Computational Materials Modelling**. My goal is to bridge the gap between quantum-mechanical theory (DFT) and macroscopic material properties.

---

## 📚 Technical Syllabus
This repository is organized based on the core pillars of Density Functional Theory and its application in materials science:

### 1. Fundamentals of DFT
* **Theory:** Origins, popularity, and the Many-Body Schrödinger Equation.
* **Approximations:** Clamped nuclei, Independent electrons, Mean-field, and Hartree–Fock.
* **Kohn-Sham Framework:** Total energy calculations, Local Density Approximation (LDA), and self-consistency.

### 2. Structural & Mechanical Properties
* **Equilibrium Structures:** Calculating forces, minimizing energy, and comparing DFT results with X-ray crystallography and STM data.
* **Elasticity:** Stress-strain formalisms, elastic constants, and extreme-condition behavior.

### 3. Vibrations & Thermodynamics
* **Lattice Dynamics:** Vibrational eigenmodes, phonon dispersion, and Density of States (DOS).
* **Spectroscopy:** Connections to Raman and neutron scattering.
* **Phase Stability:** Using Phonon DOS to construct $P-T$ phase diagrams.

### 4. Electronic & Optical Properties
* **Band Theory:** Metals, insulators, semiconductors, and the "Band Gap Problem."
* **Optics:** Dielectric functions and optical spectra calculations.
* **Magnetism:** Spin-DFT, exchange energy, and magnetic materials modeling.

---

## 🛠 Simulation Workflow: Best Practices


* **Consistency:** Always match pseudopotentials (e.g., `_sv` vs `_pv`) across all elements.
* **Convergence:** Always test `ENCUT` and `KPOINTS` convergence before production runs.
* **Stability:** Use `ISIF=2` for ionic relaxation before switching to `ISIF=3` for cell relaxation to prevent numerical instability.

---

## 💡 Research Motivation
Why model materials from first principles?
1. **Predictive Capability:** Designing materials (like refractory alloys) on a computer before costly lab synthesis.
2. **Emergent Properties:** Understanding how atomic-scale quantum interactions manifest as bulk elasticity, magnetism, and thermal stability.
3. **Bridge-Building:** Linking atomic vibrations (Phonons) to macroscopic thermodynamics ($P-T$ phase diagrams).

---

## 🚀 Active Objectives
- [ ] **Benchmark:** Compare `_sv` vs `_pv` potentials for BCC Cr, Mo, and W.
- [ ] **Automation:** Develop Python scripts to automate structural convergence tests.
- [ ] **Analysis:** Visualize phonon DOS and generate phase diagrams for new alloys.

---

*“Everything is theoretically impossible, until it is done.”*
*This repository is maintained for educational purposes. Feel free to explore the derivations and implementation scripts.*
