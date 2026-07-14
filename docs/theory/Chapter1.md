# Pillar 1 (Continued): Chapter 2 Summary Notes — The Many-Body Schrödinger Equation

This file compiles comprehensive technical notes covering Chapter 2 of *Materials Modelling using Density Functional Theory: Properties & Predictions* by Feliciano Giustino. It serves as a pedagogical bridge connecting the elementary single-particle quantum mechanics of an isolated particle moving inside a static potential well to the complex multi-particle frameworks necessary to simulate real interacting solid-state matter (electronic structure theory).

---

## 2.1 The Electrostatic Foundation: Coulomb Interactions

At the fundamental atomic scale, any physical material can be conceptualized by a single unifying relationship:

$$\text{Materials} = \text{Electrons} + \text{Nuclei}$$

The ultimate geometric stability, cohesion, and physical properties of solids are governed entirely by a fine electrostatic balance between competing attractive and repulsive interactions:

* **Electron-Electron Repulsion ($E_{ee}$):** The repulsive energy between two distinct electrons separated by a spatial distance $d_{ee}$:
  $$E_{ee} = \frac{e^2}{4\pi\epsilon_0 d_{ee}}$$
  where $e$ represents the absolute charge of an electron and $\epsilon_0$ is the vacuum permittivity constant.

* **Nucleus-Nucleus Repulsion ($E_{nn}$):** The repulsive energy between two nuclei carrying atomic numbers $Z_1, Z_2$ (or an identical atomic species $Z$ for simplicity) separated by a distance $d_{nn}$:
  $$E_{nn} = \frac{Z_1 Z_2 e^2}{4\pi\epsilon_0 d_{nn}}$$

* **Electron-Nucleus Attraction ($E_{en}$):** The attractive energy binding an electron to a nucleus at a distance $d_{en}$, carrying a negative sign to reflect the bound electrostatic stability:
  $$E_{en} = -\frac{Ze^2}{4\pi\epsilon_0 d_{en}}$$

---

## 2.2 Transition from Single-Particle to Many-Body Mechanics

### 2.2.1 The Single-Particle Baseline
In standard stationary configurations, the time-independent single-particle Schrödinger equation takes the conceptual form:

$$\left( \text{Kinetic Energy} + \text{Potential Energy} \right) \psi = E\psi$$

Written explicitly for an electron of mass $m_e$ moving inside a static external potential landscape $V(\vec{r})$:

$$\left[ -\frac{\hbar^2}{2m_e}\nabla^2 + V(\vec{r}) \right] \psi(\vec{r}) = E\psi(\vec{r})$$

Where the quantum-mechanical momentum operator is defined as $\hat{p} = -i\hbar\nabla$, and the probability of locating the electron at a precise coordinate vector $\vec{r} = x\hat{u}_x + y\hat{u}_y + z\hat{u}_z$ is given by the squared modulus of the wavefunction $|\psi(\vec{r})|^2$.

### 2.2.2 The Many-Body Multi-Dimensional Shift
When a second electron is introduced into this isolated single-particle environment, the naive temptation is to simply accommodate the new electron within the exact same lowest-energy ground-state orbital $\psi_0(\vec{r})$, assigning it an opposite spin in compliance with the Pauli exclusion principle (doubling the local density to $2|\psi_0|^2$).

However, this simplification ignores the **Coulomb repulsion ($E_{ee}$)** between the two electrons. This mutual repulsion acts back on the system, altering both the original shape of the spatial wavefunctions and modifying the localized effective potential energy landscape.

To handle this multi-particle coupling accurately, a system containing $N$ interacting electrons and $M$ interacting nuclei cannot be treated via isolated single-particle wavefunctions. Instead, we must define a single collective, multi-dimensional **Many-Body Wavefunction ($\Psi$)** that depends simultaneously on every single coordinate:

$$\Psi = \Psi(\vec{r}_1, \vec{r}_2, \dots, \vec{r}_N; \vec{R}_1, \vec{R}_2, \dots, \vec{R}_M)$$

* **Electronic Coordinates:** $\vec{r}_i$ indicates the spatial position of the $i$-th electron.
* **Nuclear Coordinates:** $\vec{R}_I$ indicates the spatial position of the $I$-th nucleus.

### 2.2.3 The Comprehensive Many-Body Hamiltonian
The absolute non-relativistic time-independent many-body Schrödinger equation governing this combined system is expressed as:

$$\hat{H} \Psi = E \Psi$$

Where the full complete Hamiltonian operator $\hat{H}$ expands into five individual components representing kinetic energy and Coulomb interactions:

$$\hat{H} = -\sum_{i=1}^{N}\frac{\hbar^2}{2m_e}\nabla_i^2 - \sum_{I=1}^{M}\frac{\hbar^2}{2M_I}\nabla_I^2 - \sum_{i=1}^{N}\sum_{I=1}^{M}\frac{Z_I e^2}{4\pi\epsilon_0 |\vec{r}_i - \vec{R}_I|} + \frac{1}{2}\sum_{i \neq j}^{N}\frac{e^2}{4\pi\epsilon_0 |\vec{r}_i - \vec{r}_j|} + \frac{1}{2}\sum_{I \neq J}^{M}\frac{Z_I Z_J e^2}{4\pi\epsilon_0 |\vec{R}_I - \vec{R}_J|}$$

#### Hamiltonian Terms Decoded:
* **$\hat{T}_e = -\sum_{i=1}^{N}\frac{\hbar^2}{2m_e}\nabla_i^2$**: Kinetic energy operator summed over all $N$ individual electrons.
* **$\hat{T}_n = -\sum_{I=1}^{M}\frac{\hbar^2}{2M_I}\nabla_I^2$**: Kinetic energy operator summed over all $M$ individual nuclei (where $M_I$ is the mass of the $I$-th nucleus).
* **$\hat{V}_{en} = -\sum_{i=1}^{N}\sum_{I=1}^{M}\frac{Z_I e^2}{4\pi\epsilon_0 |\vec{r}_i - \vec{R}_I|}$**: The attractive electron-nuclear potential energy between every electron-nucleus pair.
* **$\hat{V}_{ee} = \frac{1}{2}\sum_{i \neq j}^{N}\frac{e^2}{4\pi\epsilon_0 |\vec{r}_i - \vec{r}_j|}$**: The repulsive electron-electron interactions (the factor of $1/2$ prevents double-counting pairs).
* **$\hat{V}_{nn} = \frac{1}{2}\sum_{I \neq J}^{M}\frac{Z_I Z_J e^2}{4\pi\epsilon_0 |\vec{R}_I - \vec{R}_J|}$**: The repulsive inter-nuclear potential energy between distinct nuclei pairs.

---

### 2.3 The Dimensionality Catastrophe

The major challenge in directly evaluating the many-body equation is the **dimensionality scaling**. For a relatively small system containing a few dozen atoms:

* Each single electron requires 3 spatial degrees of freedom ($x, y, z$).
* A system with $N$ electrons results in a differential equation operating across a $3N$-dimensional mathematical space.

## 2.4 The Clamped Nuclei (Born-Oppenheimer) Approximation

To begin simplifying the many-body problem, we exploit the enormous mass difference between electrons and atomic nuclei. Because a single proton is approximately 1,836 times heavier than an electron, the nuclei move at a snail's pace compared to the nearly instantaneous response of the surrounding electron cloud. 

We can therefore decouple their motion by "freezing" or clamping the coordinates of the nuclei at fixed spatial coordinates $\vec{R}_I$:
1. The nuclear kinetic energy operator vanishes: $\hat{T}_n = 0$.
2. The nucleus-nucleus repulsion term $E_{nn}$ becomes a constant electrostatic shift.

In Hartree atomic units ($e = 1, m_e = 1, \hbar = 1, 4\pi\epsilon_0 = 1$), this simplifies the total many-body Hamiltonian to the **electronic Hamiltonian** $\hat{H}$:

$$\hat{H} = -\sum_{i=1}^{N} \frac{\nabla_i^2}{2} - \sum_{i=1}^{N}\sum_{I=1}^{M}\frac{Z_I}{|\vec{r}_i - \vec{R}_I|} + \frac{1}{2}\sum_{i \neq j}^{N}\frac{1}{|\vec{r}_i - \vec{r}_j|}$$

This acts on the electronic wavefunction $\Psi(\vec{r}_1, \vec{r}_2, \dots, \vec{r}_N)$, yielding the electronic Schrödinger equation:

$$\hat{H}\Psi(\vec{r}_1, \vec{r}_2, \dots, \vec{r}_N) = E\Psi(\vec{r}_1, \vec{r}_2, \dots, \vec{r}_N)$$

---

## 2.5 The Independent Electrons Approximation

Even with fixed nuclei, the electron-electron interaction term $\hat{V}_{ee} = \frac{1}{2}\sum_{i\neq j} \frac{1}{|\vec{r}_i - \vec{r}_j|}$ couples the positions of all electrons, rendering the equation mathematically inseparable. 

The simplest starting approximation is to assume that the electrons **do not interact with one another** (setting $\hat{V}_{ee} = 0$). Under this assumption, the Hamiltonian simplifies to a sum of independent single-particle Hamiltonians:

$$\hat{H} \approx \sum_{i=1}^{N} \hat{H}_0(\vec{r}_i), \quad \text{where} \quad \hat{H}_0(\vec{r}_i) = -\frac{\nabla_i^2}{2} + V_n(\vec{r}_i)$$

Here, $V_n(\vec{r}_i) = -\sum_{I} \frac{Z_I}{|\vec{r}_i - \vec{R}_I|}$ is the attractive potential of the fixed nuclei.

### Wavefunction Ansatz
Because the operator is fully separable, the collective many-body wavefunction can be written simply as a Hartree product of individual, single-particle orbitals $\phi_i(\vec{r}_i)$:

$$\Psi(\vec{r}_1, \vec{r}_2, \dots, \vec{r}_N) = \phi_1(\vec{r}_1)\phi_2(\vec{r}_2)\dots\phi_N(\vec{r}_N)$$

Applying this product to the independent Schrödinger equation yields the total energy as a simple sum of individual orbital eigenvalues:

$$E = \sum_{i=1}^{N} \epsilon_i$$

---

## 2.6 Incorporating the Pauli Exclusion Principle

The simple Hartree product fails a fundamental physical criterion: electrons are fermions, meaning their collective wavefunction must be **antisymmetric** under the exchange of any two electronic coordinates:

$$\Psi(\vec{r}_1, \dots, \vec{r}_i, \dots, \vec{r}_j, \dots, \vec{r}_N) = -\Psi(\vec{r}_1, \dots, \vec{r}_j, \dots, \vec{r}_i, \dots, \vec{r}_N)$$

To mathematically enforce this antisymmetric property, we write the many-body wavefunction as a **Slater Determinant**:

$$\Psi(\vec{r}_1, \vec{r}_2, \dots, \vec{r}_N) = \frac{1}{\sqrt{N!}} \begin{vmatrix} 
\phi_1(\vec{r}_1) & \phi_2(\vec{r}_1) & \dots & \phi_N(\vec{r}_1) \\ 
\phi_1(\vec{r}_2) & \phi_2(\vec{r}_2) & \dots & \phi_N(\vec{r}_2) \\ 
\vdots & \vdots & \ddots & \vdots \\ 
\phi_1(\vec{r}_N) & \phi_2(\vec{r}_N) & \dots & \phi_N(\vec{r}_N) 
\end{vmatrix}$$

If two electrons occupy the exact same state (i.e., $\phi_i = \phi_j$), two columns become identical, making the determinant zero. This naturally satisfies the Pauli exclusion principle.

---

## 2.7 The Mean-Field (Hartree) Approximation

To reintroduce electron-electron repulsion without returning to the $3N$-dimensional complexity, we employ a **mean-field approximation**. Instead of tracking the explicit point-to-point repulsion between individual electrons, we assume each electron moves in an average classical electrostatic potential created by the *entirety of the other electrons*.

This modifies our single-particle Schrödinger equations to:

$$\left[ -\frac{\nabla^2}{2} + V_n(\vec{r}) + V_H(\vec{r}) \right] \phi_i(\vec{r}) = \epsilon_i \phi_i(\vec{r})$$

Where $V_H(\vec{r})$ is the **Hartree potential** representing the classical electrostatic potential generated by the total electron density $n(\vec{r})$:

$$V_H(\vec{r}) = \int \frac{n(\vec{r}')}{|\vec{r} - \vec{r}'|} d\vec{r}' \quad \text{with} \quad n(\vec{r}') = \sum_{j=1}^N |\phi_j(\vec{r}')|^2$$

### The Self-Consistent Field (SCF) Cycle
Because the potential $V_H$ depends directly on the wavefunctions we are trying to solve for, these equations must be solved iteratively:
1. Guess an initial set of wavefunctions $\{\phi_i\}$.
2. Compute the electron density $n(\vec{r})$ and the resulting Hartree potential $V_H(\vec{r})$.
3. Solve the Schrödinger equation to yield a new set of wavefunctions.
4. Repeat until the input and output wavefunctions are identical (self-consistency).

---

## 2.8 The Hartree-Fock Approximation

While the Hartree approximation includes classical repulsion, it lacks quantum-mechanical exchange effects arising from the antisymmetric Slater determinant. By formally applying the variational principle to a single Slater determinant wavefunction, we arrive at the **Hartree-Fock (HF) equations**:

$$\left[ -\frac{\nabla^2}{2} + V_n(\vec{r}) + V_H(\vec{r}) \right] \phi_i(\vec{r}) + \int V_X(\vec{r}, \vec{r}') \phi_i(\vec{r}') d\vec{r}' = \epsilon_i \phi_i(\vec{r})$$

Here, the new term $V_X(\vec{r}, \vec{r}')$ is the **Fock Exchange Potential**:

$$V_X(\vec{r}, \vec{r}') = -\sum_{j=1}^{N} \frac{\phi_j^*(\vec{r}')\phi_j(\vec{r})}{|\vec{r} - \vec{r}'|}$$

### The Catch: Non-Locality
* **The Good:** It transitions our description from classical point charges to interacting quantum fermions.
* **The Bad:** The exchange potential is **non-local**. It cannot be written as a simple multiplicative potential $V_X(\vec{r})$; instead, evaluating it requires a complex integration over the secondary spatial variable $\vec{r}'$. This makes Hartree-Fock calculations computationally expensive for large systems.

---

## 2.9 The Kohn-Sham Formulation

Density Functional Theory (DFT) solves the limitations of both methods. Hohenberg and Kohn proved that the ground-state properties of a many-body system are uniquely determined by the **electron density $n(\vec{r})$** rather than the highly complex $3N$-dimensional wavefunction $\Psi$.

Kohn and Sham mapped this complex interacting system onto an auxiliary, *non-interacting* reference system that yields the exact same ground-state density. This results in the elegant **Kohn-Sham Equations**:

$$\left[ -\frac{\nabla^2}{2} + V_{\text{tot}}(\vec{r}) \right] \phi_i(\vec{r}) = \epsilon_i \phi_i(\vec{r})$$

Where the total effective potential $V_{\text{tot}}(\vec{r})$ is purely **local** and partitioned into three distinct physical contributions:

$$V_{\text{tot}}(\vec{r}) = V_n(\vec{r}) + V_H(\vec{r}) + V_{xc}(\vec{r})$$

1. **$V_n(\vec{r})$:** The local electrostatic attraction of the fixed nuclei.
2. **$V_H(\vec{r})$:** The classical Hartree repulsion potential of the electron cloud.
3. **$V_{xc}(\vec{r})$:** The **Exchange-Correlation Potential**. 

### The Exchange-Correlation Potential ($V_{xc}$)
The exchange-correlation potential is formally defined as the functional derivative of the exchange-correlation energy with respect to the electron density:

$$V_{xc}(\vec{r}) = \frac{\delta E_{xc}[n]}{\delta n(\vec{r})}$$

This single term contains *all* the remaining complex quantum interactions:
* Quantum **exchange** (which Hartree-Fock calculated using its non-local potential).
* Dynamic **correlation** (the way electrons actively avoid one another beyond average-field or exchange models).
* The kinetic energy correction between the non-interacting auxiliary system and the real interacting system.

By condensing these many-body complications into a single local potential $V_{xc}(\vec{r})$, the Kohn-Sham formulation allows us to accurately solve solid-state electronic structures with extreme computational efficiency.
