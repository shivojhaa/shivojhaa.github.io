---
layout: page
title: UTILIZING GENETIC ALGORITHMS TO DESIGN SEMICONDUCTOR DEVICES
description: My Bachelor's capstone, advised by Dr. Nicholas C. Miller. A genetic algorithm (NSGA-II) with a 1D TCAD solver in the loop that designs graded AlGaN Schottky contacts. It found a design with a much narrower tunneling width than the baseline in about 10 minutes on a laptop.
importance: 8
img: assets/img/projects/capstone_search.png
category: capstone
---

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/capstone_search.png" title="Search space of the optimization problem" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Search space of this optimization problem on hyperspace R2. The main optimization sample space is on R2, which is well suited for this optimization.
</div>

This is my Bachelor's capstone (ECE 489), advised by Dr. Nicholas C. Miller. Designing a semiconductor device usually means manual parameter sweeps and tuning from experience. As the number of coupled parameters grows (doping, compositional grading, the length of the grade, polarization-induced band bending), that gets inefficient and can lead to suboptimal designs. For this project I used a genetic algorithm with a TCAD simulation in the loop to explore the design space automatically.

## Method

I wrote the optimizer in Python with pymoo, the library built by Dr. Kalyanmoy Deb at Michigan State, using NSGA-II with a custom problem definition. Each candidate is a genome with the doping concentration, the compositional grading endpoints, the grading length and the number of grading regions, for single- and multi-segment devices. Each genome is decoded into a device, written to an input file and simulated with a 1D numerical solver (SpartyCAD), which gives the tunneling length, barrier area, conduction-band profile and E-field. The objective is to minimize the tunneling length and the barrier area.

To save time, results are cached by hash so identical devices are never simulated twice, and the runs are parallel. The crossover and mutation probabilities adapt using hypervolume feedback, and a run stops early once the Pareto front stops improving. I seeded part of the initial population with the Schottky diode from Chen et al. (UW-Madison) and filled the rest with random devices.

## Results

The GA diode beats the seeded baseline in tunneling width. The effective tunneling width came down from roughly 5 nm (at a doping of 6e19) in the early generations to about 2.6-2.8 nm in the final design, depending on the polarization properties of AlxGa1-xN. This comes from refined compositional grading and higher doping near the contact, which raises the contact E-field without changing the metallization. The algorithm produced the smooth band bending on its own, I did not force it into shape.

The reverse-bias TFE/FE currents of the GA diode are larger than the seeded one, which is expected with a narrower tunneling width, so reverse-bias leakage in AlxGa1-xN Schottky diodes still needs a study of its own. The Pareto plot of the search space, about 10,000 (10⁴) candidate devices, shows a clear, roughly linear trade-off between Schottky barrier width and doping.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/capstone_pareto.png" title="Pareto plot of the search space" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Full Pareto front of the search space of about 10,000 devices. The gap in solutions comes from the lack of vertical search (see the search space figure above). We can still see a linear relationship developing between SBH (width) and doping (x-axis).
</div>

In forward bias the GA diode has a higher current density at the ohmic contact and a more linear Schottky side, which points to better carrier injection. Single-segment grading gave the best Pareto fronts. The whole search took about 10 minutes on a 6-core laptop CPU with 32 GB of RAM.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/capstone_iv_seed.png" title="Seeded device, J against V at the anode" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Seeded device: voltage at the ohmic contact (into the semiconductor) and the Schottky barrier (metal-semiconductor contact).
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/capstone_iv_ga.png" title="GA device, J against V at the anode" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    GA device: the same plots, with better performing IV curves. The Schottky barrier gives a more linear characteristic, V_anode against J_anode being more linear.
</div>

## Limits and next steps

The search explores well horizontally but struggles to reach the vertical solutions, because of the seeding and the adaptive hypervolume, so the Pareto front has gaps. These are 1D simulations only, so I will only know how good the designs are once they are fabricated and tested.

Next I want to improve the search to fill in the Pareto front, add 2D solvers so a diode can be co-designed for electro-thermal performance (AlGaN-channel HEMTs, where self-heating matters), and fabricate the stack and test it as a diode, then as the epitaxial stack of a HEMT.
