---
title: "A Free-Surface 2D Fluid Solver from Voronoï Diagrams to Optimal Transport"
date: 2025-06-18
tags: []
author: "Alexandre Bismuth"
description: "CSE306 Computer Graphics project: a free-surface 2D fluid solver built on Power diagrams, semi-discrete optimal transport with L-BFGS, and the de Gallouet-Mérigot incompressible Euler scheme."
summary: "CSE306 Computer Graphics project at École Polytechnique. A free-surface 2D fluid solver built from the ground up — Voronoï and Power diagrams, semi-discrete optimal transport optimised with L-BFGS, and the de Gallouet-Mérigot incompressible Euler scheme."
cover:
    image: "cover.png"
    alt: "Free-surface 2D fluid simulation of blue particles"
---

---

*Computer Graphics (CSE306), Bachelor of Science, École Polytechnique.*

<div class="buttons" style="display:flex;flex-wrap:wrap;justify-content:space-between;gap:10px;margin:14px 0 10px 0;">
  <a class="button" style="flex:1;text-align:center;margin:0;padding:5px 10px;background:rgba(0,0,0,0.1);" href="report.pdf"><span class="button-inner">Report</span></a>
  <a class="button" style="flex:1;text-align:center;margin:0;padding:5px 10px;background:rgba(0,0,0,0.1);" href="https://github.com/alexandre-bismuth/CSE306-FluidSolver"><span class="button-inner">Code</span></a>
</div>

---

##### Overview

This project implements a free-surface 2D fluid solver using incompressible Euler's equations. It implements all of the mandatory sections of the assignment — Voronoï Diagrams, Power Diagram, Optimization with LBFGS, the de Gallouet-Mérigot incompressible Euler scheme, and a spring force from each fluid particle to their Laguerre's cell centroid. The code is written in C++11 and split into headers and sources for organisational purposes, with a Makefile to simplify compilation. To ensure clarity and correctness, the code is also optimized as much as possible: `const` statements were added wherever possible to avoid and identify bugs easily, floating-point operations were prioritized for the highest precision, and the most efficient types were used for each variable to optimize memory.

---

##### Clipping and Voronoï diagrams

The first part of the project revolves around implementing the Voronoï Parallel Linear Enumeration algorithm. For that, I implement the Sutherland-Hodgman polygon clipping algorithm, a `Polygon` class, and a `VoronoiDiagram` class. The implementation renders a diagram of *N* = 3000 cells in **0.072s**.

---

##### Power diagram and weights optimization with L-BFGS

In this second part, the Voronoï diagram is converted to a Power diagram that generalizes it by assigning a weight to each point, implementing semi-discrete optimal transport with L-BFGS. Beyond uniform weights, the solver can be tested with arbitrary weight distributions — below, a Gaussian distribution (standard deviation *σ* = 0.18) and an exponential distribution from the bottom-left corner (*λ* = 4), each tailored for best visual results.

<div style="display:flex;flex-wrap:wrap;gap:16px;justify-content:center;margin:6px 0;">
  <figure style="flex:1 1 220px;max-width:280px;margin:0;text-align:center;">
    <img src="power-uniform.svg" alt="Power diagram with uniform weights" style="width:100%;border:1px solid rgba(0,0,0,0.08);border-radius:8px;">
    <figcaption style="font-size:0.82em;opacity:0.75;margin-top:4px;">Uniform weights (N = 2000)</figcaption>
  </figure>
  <figure style="flex:1 1 220px;max-width:280px;margin:0;text-align:center;">
    <img src="power-gaussian.svg" alt="Power diagram with Gaussian weights" style="width:100%;border:1px solid rgba(0,0,0,0.08);border-radius:8px;">
    <figcaption style="font-size:0.82em;opacity:0.75;margin-top:4px;">Gaussian weights (σ = 0.18)</figcaption>
  </figure>
  <figure style="flex:1 1 220px;max-width:280px;margin:0;text-align:center;">
    <img src="power-exponential.svg" alt="Power diagram with exponential weights" style="width:100%;border:1px solid rgba(0,0,0,0.08);border-radius:8px;">
    <figcaption style="font-size:0.82em;opacity:0.75;margin-top:4px;">Exponential weights (λ = 4)</figcaption>
  </figure>
</div>

---

##### Fluid dynamics

After implementing these diagrams which we can parametrize with any kind of weights, we can move on to modeling fluid dynamics. Each fluid particle is coupled to its Laguerre cell through a spring force to the cell centroid, and the system is advanced with the de Gallouet-Mérigot incompressible Euler scheme. The simulation below runs **500 fluid particles** with *ε* = 0.004, *dt* = 0.002 and a mass of 200 per particle, over 250+ frames.

<figure style="margin:10px auto;max-width:480px;text-align:center;">
  <img src="fluid-simulation.gif" alt="Working free-surface fluid simulation" style="width:100%;border-radius:10px;">
  <figcaption style="font-size:0.82em;opacity:0.75;margin-top:6px;">Working fluid simulation over 250+ frames</figcaption>
</figure>

---

##### Key results

+ Voronoï diagram via parallel linear enumeration: **0.072s** for *N* = 3000 cells.
+ Power diagram with semi-discrete optimal transport optimised through **L-BFGS**, supporting arbitrary weight distributions (uniform, Gaussian, exponential).
+ Free-surface fluid simulation coupling each particle to its Laguerre cell centroid via the **de Gallouet-Mérigot incompressible Euler scheme**.
