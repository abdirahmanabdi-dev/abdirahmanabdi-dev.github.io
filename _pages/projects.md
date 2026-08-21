---

permalink: /projects/

title: "Projects"

author_profile: true

---

A collection of academic research and personal projects I've worked on, ranging from computational chemistry and materials science to physics simulations and scientific computing. Some are serious research projects, some are experiments I started because I was curious, and some are probably a mixture of both.

## Academic projects

**Computational modelling of hydrogen-bonded atmospheric complexes**

**University of Leicester — supervised by [Prof. Shengfu Yang](https://le.ac.uk/people/shengfu-yang) — Oct 2025 to Dec 2025**

I investigated how hydrogen bonding affects small molecular complexes that can form in the atmosphere. Using Gaussian, I modelled several hydrogen-bonded complexes with both DFT and MP2, optimising their geometries and calculating their binding energies for different molecular orientations.

One of the things I found particularly interesting was how much care is needed when calculating these relatively small interactions. I used counterpoise correction to account for basis set superposition error (BSSE), which brought the calculated binding energies much closer to established experimental values.

<img class="project-image" src="/images/frm-dimer.JPG" alt="DFT-optimised formaldehyde dimer geometry">

**Carbon quantum dot synthesis and bioconjugation**

**University of Leicester — supervised by [Dr. Philip Ash](https://le.ac.uk/people/philip-ash) — Jan 2026 to Mar 2026**

I worked on the synthesis and characterisation of carbon quantum dots (CQDs), a type of nanomaterial with interesting optical properties and potential applications in areas such as biosensing and bioimaging.

I synthesised nitrogen-doped CQDs from organic precursors using microwave-assisted synthesis, then used FTIR and UV-Vis spectroscopy to investigate their surface chemistry and electronic transitions. I then coupled the CQDs with myoglobin to see whether they could be used for bioconjugation, using photoluminescence measurements to look for changes in their optical behaviour.

<img class="project-image" src="/images/cqd-website-pic.jpg" alt="Carbon quantum dot synthesis and characterisation">

**EPSRC Undergraduate Research Internship – Nanoparticle-enabled ionic skin**

**University of Leicester — supervised by [Prof. Shengfu Yang](https://le.ac.uk/people/shengfu-yang) — Jul 2026 to Sep 2026 (ongoing)**

I was awarded an 8-week EPSRC-funded summer research internship investigating nanoparticle-enabled ionic skin materials for potential sensing applications. The wider project is looking at how advanced materials can be used to improve the performance of flexible electronic systems.

My role involves laboratory-based research, materials characterisation and experimental development alongside the wider research team. I'm particularly interested in getting experience with how an open-ended research problem develops in practice, from designing experiments through to interpreting the results.

*As this research is ongoing and unpublished, further technical details will be added once they are suitable for public release.*

## Coding projects

**Hückel molecular orbital solver**

*Personal project — [GitHub](https://github.com/abdirahmanabdi-dev/huckel-theory)*

I wanted to have a go at implementing Hückel Molecular Orbital (HMO) theory myself rather than just using the equations on paper. The basic idea is that we can simplify the quantum mechanics of conjugated molecules by focusing on their π-electrons and turning the problem into a matrix diagonalisation.

I built a Python solver that takes the connectivity of a molecule and uses it to construct the Hückel matrix, applying the usual HMO assumptions along the way. I then use JAX's hardware-accelerated `eigh` routine to solve the matrix and get the π-orbital energies and coefficients.

One of the more interesting parts of the project was digging into why this works mathematically. The Hückel matrix is real and symmetric, which means it is also Hermitian. This guarantees that the orbital energies are real and that the resulting orbital coefficient vectors are orthogonal. I found this a particularly nice connection between the chemistry and the linear algebra underneath it.

The solver currently works with both linear chains and cyclic systems, so it can be used to explore different conjugated molecules and see how changing the molecular structure affects the resulting π-orbitals.

**Basic particle simulation**

*Personal project — [GitHub](https://github.com/abdirahmanabdi-dev/basic-particle-simulation)*

Hello, World! I recently discovered a Python library called Taichi, which piqued my interest, so I spent a day experimenting with it and built a very basic 3D particle simulation.

The core philosophy of the project was that the `engine.py` file — or, henceforth, the **Engine** — would be the ultimate source of truth. The rendering code knows nothing about why a particle is at a particular position; it simply renders the positions provided by the Engine. This separation means I can change the initial conditions or add more particles without having to modify the rendering code.

<img class="project-image" src="/images/basic-particle-sim-gif.gif" alt="Basic particle simulation running in Taichi">

The Engine currently models particles as point charges and calculates their interactions using Coulomb's law. I initially used Euler integration to update the velocity and position of each particle, which exposed some of the problems associated with numerical integration and finite time steps. In particular, particles could gain enough velocity to pass through one another. This was a useful lesson in the difference between implementing a physical equation and actually producing a physically accurate simulation.

I also built a basic ray-sphere renderer in Taichi to visualise the particles in 3D. The renderer generates rays from a camera, solves the ray-sphere intersection as a quadratic equation, calculates the surface normal and applies basic diffuse lighting. Importantly, none of this affects the physics — the renderer simply receives the particle positions from the Engine.

The next step is to replace Euler integration with Verlet integration and compare the behaviour of the simulation. From there, I'd like to explore more of the underlying physics, particularly condensed matter and particle physics, and see how far I can take the simulation while keeping the architecture general rather than simply adding fixes whenever something goes wrong.
