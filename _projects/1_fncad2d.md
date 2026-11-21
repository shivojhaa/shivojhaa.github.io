---
layout: page
title: FNCAD2D
description: A 2D device simulator for GaN HEMTs that adds hot-electron transport (Fermi kinetics transport) to a drift-diffusion solver, checked against exact limits, a measured HEMT and a published benchmark.
importance: 1
category: research
---

FnCAD2D is a two-dimensional semiconductor device simulator, written in Python, for modelling GaN high-electron-mobility transistors (HEMTs) from DC through RF. It grows out of FnCAD, a 1D drift-diffusion solver, and adds hot-electron transport based on the Fermi kinetics transport (FKT) framework of Miller et al.

## Why

GaN HEMTs operate with electric fields of hundreds of kV/cm near the drain-side gate edge. There the electrons heat up to thousands of kelvin, so their velocity and where they deposit energy depend on their own temperature, not only on the local field. Standard drift-diffusion cannot describe this. FKT treats the electrons at every mesh node as a Fermi gas with its own Fermi level and temperature, and solves for particle and energy conservation together with Poisson's equation.

## What the simulator does

- **Mesh:** Delaunay triangulation with Voronoi control volumes (box method) on arbitrary 2D cross-sections, including T-gates.
- **Transport:** drift-diffusion with Scharfetter–Gummel fluxes, or FKT: densities and fluxes from incomplete Fermi–Dirac integrals, a generalized Scharfetter–Gummel flux, heat flow from the thermodynamics of Fermi gases, and energy relaxation to the lattice.
- **Device physics:** heterojunctions and Schottky gates with thermionic emission (including energy flux), polarization charges, bulk and surface traps, quantum confinement of the 2DEG, and lattice self-heating.
- **RF:** small-signal analysis giving S-parameters, $f_T$ and $f_{max}$, with pad parasitics embedded.

## Validation

Before any comparison with a real device, the solver was checked against exact limits:

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

The simulator was applied, without fitting, to a published AlGaN/GaN HEMT (0.25 µm gate, Vitanov et al., IEEE TED 2012). At $V_{GS} = -1.5$ V and $V_{DS} = 7$ V, including self-heating and contact resistance, it gives a drain current of 0.31 A/mm (measured 0.27 A/mm) and $f_T = 47$ GHz (measured 31 GHz).

The $f_T$ gap is informative rather than a failure. Since $f_T \approx g_m / 2\pi(C_{gs} + C_{gd})$, I compared each part: the simulated transconductance is about 12% _below_ the measurement, so the transport is not too fast. The gate capacitance must instead be about 60% too small. The likely causes are gate geometry the paper does not specify (T-gate head, passivation thickness), three-dimensional layout capacitance that a 2D cross-section cannot include, and mesh resolution at the gate corners.

## Benchmark against published FKT

To test the FKT implementation independently of fabrication unknowns, I reproduced the GaN HEMT simulation of Tunga et al. (2022), which compares FKT with a commercial hydrodynamic solver on a fully specified device, using their geometry and parameters and no fitting. The electron temperature in the channel peaks at 4694 K under the middle of the gate, against about 4700 K for their FKT and about 15,500 K for their commercial solver. With each curve divided by its own on-state current, my drain-current curves agree with theirs to within a few percent in the on-state. Near threshold at high drain bias my currents are higher than theirs (for example 0.36 against 0.29 of the on-state current at $V_{GS} = -2$ V, $V_{DS} = 10$ V), and a finer mesh does not change that. The paper's values are read off its figures, so they are good to a few percent at best.

## Lessons

- **Convergence is physics too.** Nearly empty electron gases in the buffer were never truly converged because the convergence test (rightly) ignored them; a later, longer solve exposed them and diverged. Letting such gases fill to a negligible density in one Newton step fixed it without changing any result.
- **Exactness matters at equilibrium.** The paper's arithmetic-mean temperature in the flux produces spurious current next to the degenerate 2DEG; a logarithmic mean makes the equilibrium current vanish exactly.
