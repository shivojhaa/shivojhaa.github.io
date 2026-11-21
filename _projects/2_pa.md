---
layout: page
title: MY FIRST (FAILED) PA
description: A 0.8 to 1.2 GHz power amplifier on a GaAs pHEMT, designed in ADS, built and measured. It missed its specifications, with the whole response landing 300 to 400 MHz too low.
img: assets/img/projects/pa_board.png
importance: 3
category: coursework
---

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/pa_board.png" title="The fabricated board" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The fabricated board.
</div>

An ECE 404 project, done with a lab partner: design, build and measure an RF power amplifier around the Skyworks SKY65050 GaAs pHEMT on a Rogers RO4350B board, for the 0.8 to 1.2 GHz band in a 50 Ω system. The targets were S21 = 17 dB ± 1 dB, and S11 and S22 below −8 dB across the band.

## Design

We designed it in Keysight ADS: a stability circuit, input and output matching networks that combine lumped and distributed elements, and a DC bias network (V_GS = −0.4 V, V_DS = 3.0 V) with RF/DC blocks. We checked it with circuit and electromagnetic simulations, laid it out in ADS, had the board fabricated at MSU, and soldered the surface-mount parts ourselves.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/pa_layout.png" title="PCB layout" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    PCB layout.
</div>

## Results

The first board did not work. Solder shorted connections near port 2, the transistor was never soldered properly so it could not be biased, and the layout was too small to work on by hand. On the second board the amplifier had gain, but in the wrong place: about 14 dB, centred near 0.5 GHz, instead of 17 dB across 0.8 to 1.2 GHz, and the input and output match moved down with it. It did not meet the specification.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/pa_sparams.png" title="Measured S-parameters" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Measured S-parameters, 0.1 to 1.8 GHz.
</div>

## What went wrong

The electromagnetic simulation of the layout showed the same 300 to 400 MHz shift from the schematic result, and it tracked the measurement closely; the circuit-only simulation did not. We had put transmission lines between the component pads without accounting for their electrical length, which added reflections and pulled the match down in frequency. One capacitor pad also had no gap, so we cut one by hand, which probably added to the shift.

The lesson: the electromagnetic simulation, not the circuit simulation, decides whether an RF layout works, so start from it. Also, do not make the board smaller than you can solder by hand.
