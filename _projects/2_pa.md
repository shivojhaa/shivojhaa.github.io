---
layout: page
title: MY FIRST (FAILED) PA
description: Design, fabrication and characterization of an RF power amplifier for the 0.8 to 1.2 GHz band using a SKY65050 GaAs pHEMT. It was our first amplifier and it failed to meet specifications, with a leftward shift of 300-400 MHz.
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

This ECE 404 project, done with Avery Wiklund (now at CU Boulder, working with Dr. Taylor Barton), was the design, fabrication and characterization of an RF power amplifier using the SKY65050 transistor, a GaAs pHEMT. We designed it on a Rogers RO4350B substrate with soldered components for the 0.8 to 1.2 GHz band. The objective was an S21 of 17 dB with a tolerable limit of ±1 dB, and an S11 and S22 of less than -8 dB, in a 50 Ω system.

## Design

We designed it in Keysight ADS using circuit-based and EM simulations. It has a stability circuit, input and output matching networks that combine lumped and distributed elements, and a DC bias network (V_GS of -0.4 V and V_DS of 3.0 V) with RF/DC blocks. The layout was also done in ADS. The boards were fabricated at MSU and we soldered the components ourselves.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/pa_layout.png" title="PCB layout" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    PCB layout.
</div>

## Results

Our first attempt did not work. It was our first time soldering surface-mount parts, so we were learning on the job, and some solder shorted connections near port 2. We never soldered the pHEMT properly, so we could not bias it and saw practically no S21. We also made the layout smaller than we wanted, which made the soldering harder.

On the second attempt we saw some S21, or gain, but at the wrong band: about 14 dB near 0.5 GHz instead of 17 dB across 0.8 to 1.2 GHz. S11 and S22 shifted left with it. We saw a leftward shift of 300-400 MHz and the amplifier failed to meet the specifications.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/pa_sparams.png" title="Measured S-parameters" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Measured S-parameters, 0.1 to 1.8 GHz.
</div>

## What went wrong

The EM simulation matched the real-world performance and the circuit simulation did not. That was the difference between a working and a dysfunctional amplifier, so in the future we will pay more attention to EM simulations. We also left out the electrical length of the transmission lines between our pads, which caused compounding reflections, so the match got worse as the frequency went up. One capacitor on the S22 side had no spacing, so we used tweezers to force a gap, which could have added to the shift.

From this we learned how much proper soldering matters, to verify the layout carefully, and not to make the board smaller than we can solder.
