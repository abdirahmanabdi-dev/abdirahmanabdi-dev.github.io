---
permalink: /projects/
title: "Projects"
author_profile: true
---
A record of my academic and personal projects. More will be added as work progresses.
## Academic projects
**Computational modelling of hydrogen-bonded atmospheric complexes**
*University of Leicester — supervised by [Prof. Shengfu Yang](https://le.ac.uk/people/shengfu-yang) — Oct 2025 to Dec 2025*
Hydrogen bonds play a subtle but important role in atmospheric chemistry, influencing how molecules cluster and react in the gas phase. Using Gaussian, I applied DFT and MP2 methods to model a set of hydrogen-bonded molecular complexes, optimising geometries and computing binding energies across multiple orientations. To address basis set superposition error (BSSE), I applied counterpoise correction throughout, bringing computed binding energies into quantitative agreement with established experimental benchmarks.

<img src="/images/comp-chem.png" alt="DFT-optimised hydrogen-bonded complex geometry" style="max-width:100%;">

**Carbon quantum dot synthesis and bioconjugation**
*University of Leicester — supervised by [Dr. Philip Ash](https://le.ac.uk/people/philip-ash) — Jan 2026 to Mar 2026*
Carbon quantum dots are a class of nanomaterial with tunable optical properties and promising applications in biosensing and bioimaging. I synthesised nitrogen-doped CQDs from organic precursors via microwave-assisted synthesis, then characterised their surface chemistry and electronic transitions using FTIR and UV-Vis spectroscopy. To assess bioconjugation potential, I coupled the CQDs with myoglobin and analysed the interaction through photoluminescence measurements, looking for spectroscopic shifts indicative of successful surface binding.

<img src="/images/qcd-project-website.png" alt="Carbon quantum dot synthesis and characterisation" style="max-width:100%;">

## Coding projects
**Hückel molecular orbital solver**
*Personal project — [GitHub](https://github.com/abdirahmanabdi-dev/huckel-theory)*
Hückel Molecular Orbital (HMO) theory isolates the π-electron system of conjugated molecules, reducing the quantum mechanical problem to a matrix diagonalisation. I built a Python solver that constructs the Hückel secular matrix from molecular graph connectivity — encoding the four core HMO approximations (σ–π separation, zero differential overlap, constant Coulomb integral, nearest-neighbour resonance) — and solves it using JAX's hardware-accelerated `eigh` routine. A key aspect of the implementation is the proof that the real, symmetric chemical adjacency matrix satisfies the Hermitian condition exactly, which guarantees purely real orbital energies and orthogonal wavefunction coefficients. The solver handles both linear chains and cyclic ring systems, returning π-orbital energies and expansion coefficients for any conjugated polyene.