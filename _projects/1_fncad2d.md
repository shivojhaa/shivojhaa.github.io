---
layout: page
title: FNCAD2D
description: A 2D device simulator for GaN HEMTs that adds hot-electron transport (Fermi kinetics transport) to a drift-diffusion solver. I checked it against exact limits, a measured HEMT and a published benchmark.
importance: 1
category: research
---

FnCAD2D is a two-dimensional semiconductor device simulator written in Python for modeling GaN HEMTs from DC through RF. It started from FnCAD, a 1D drift-diffusion solver. I added hot-electron transport using the Fermi kinetics transport (FKT) framework of Miller et al.

## Why

In a GaN HEMT the electric field near the drain side of the gate is hundreds of kV/cm. The electrons heat up to thousands of kelvin there, so their velocity and where they give up their energy depend on their own temperature and not only on the local field. Drift-diffusion cannot describe this. In FKT every mesh node has its own electron gas with its own Fermi level and temperature, and the energy equation is solved together with particle conservation and Poisson's equation.

## What the simulator does

- **Mesh:** Delaunay triangulation with Voronoi control volumes (box method) on any 2D cross-section, including T-gates.
- **Transport:** drift-diffusion with Scharfetter–Gummel fluxes, or FKT, which uses incomplete Fermi–Dirac integrals, a generalized Scharfetter–Gummel flux, heat flow from the thermodynamics of Fermi gases, and energy relaxation to the lattice.
- **Device physics:** heterojunctions and Schottky gates with thermionic emission, polarization charges, bulk and surface traps, quantum confinement of the 2DEG, and lattice self-heating.
- **RF:** small-signal analysis that gives S-parameters, $f_T$ and $f_{max}$, with the pad parasitics included.

## Validation

Before comparing with any real device I checked the solver against exact limits:

| Test                                              | Result                  |
| ------------------------------------------------- | ----------------------- |
| Fermi–Dirac integrals vs exact values             | $6\times10^{-13}$       |
| Jacobian vs finite differences                    | $10^{-7}$–$10^{-9}$     |
| Current at zero bias (equilibrium)                | $5\times10^{-11}$ A/cm² |
| Fast energy relaxation reproduces drift-diffusion | $10^{-5}$–$10^{-3}$     |
| Total lattice heat equals $I \cdot V$             | $10^{-11}$              |
| Uniform GaN vs the analytic hot-electron model    | $10^{-4}$               |
| Small-signal conductance at 1 kHz vs DC $dI/dV$   | $5\times10^{-10}$       |

## Comparison with a measured device

I applied it, without fitting, to a published AlGaN/GaN HEMT (0.25 µm gate, Vitanov et al., IEEE TED 2012). At $V_{GS} = -1.5$ V and $V_{DS} = 7$ V, with self-heating and contact resistance, it gives a drain current of 0.31 A/mm (measured 0.27 A/mm) and $f_T = 47$ GHz (measured 31 GHz).

To see why $f_T$ comes out too high, I looked at $f_T \approx g_m / 2\pi(C_{gs} + C_{gd})$. The simulated $g_m$ is about 12% below the measured one, so the transport is not too fast. That leaves the gate capacitance, which is about 60% too small. The likely causes are gate geometry the paper does not give (the T-gate head and the passivation thickness), 3D layout capacitance that a 2D cross-section cannot include, and the mesh at the gate corners.

## Benchmark against published FKT

To test the FKT part without fabrication unknowns, I reproduced the GaN HEMT simulation of Tunga et al. (2022), which compares FKT with a commercial hydrodynamic solver on a fully specified device. I used their geometry and parameters and did not fit anything. The electron temperature in the channel peaks at 4694 K under the middle of the gate. Their FKT gives about 4700 K and their commercial solver about 15,500 K.

With each curve divided by its own on-state current, my drain current curves agree with theirs to within a few percent in the on-state. Near threshold at high drain bias my currents are higher than theirs (0.36 against 0.29 of the on-state current at $V_{GS} = -2$ V and $V_{DS} = 10$ V), and a finer mesh does not change that. I read their values off their figures, so they are only good to a few percent.

## Lessons

- **Convergence:** nearly empty electron gases in the buffer were never really converged, because the convergence test ignores them. A longer solve exposed them and it diverged. Letting those gases fill up to a negligible density in one Newton step fixed it and did not change any result.
- **Equilibrium:** the arithmetic-mean temperature in the flux from the paper gives a spurious current next to the degenerate 2DEG. A logarithmic mean makes the equilibrium current exactly zero.
