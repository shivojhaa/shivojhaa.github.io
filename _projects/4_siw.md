---
layout: page
title: SUBSTRATE INTEGRATED WAVEGUIDE AND POWER DIVIDER
description: A 3 GHz substrate integrated waveguide and a three-port SIW power divider on a Rogers board, designed in HFSS. The waveguide matched its simulation; the divider could only be verified in simulation.
img: assets/img/projects/siw_model.png
importance: 5
category: coursework
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/siw_model.png" title="HFSS model of the waveguide" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    HFSS model of the waveguide.
</div>

An ECE 405 project, done with Grant Bell. A substrate integrated waveguide (SIW) guides the TE10 mode between two walls of vias in a PCB, with lower loss than microstrip in S-band. We designed a two-port waveguide and a three-port power divider in Ansys HFSS on a Rogers substrate, with triangular tapers from microstrip to 50 Ω SMA connectors, and had both fabricated at MSU.

## Waveguide

The design used 1 mm vias at a 2 mm pitch with the via walls 3.87 cm apart; that spacing, not the length, sets the cutoff of about 2.06 GHz, so we chose a 50 mm length. The 50 Ω feed line is 3.65 mm wide, and the taper, tuned in HFSS, is 7.3 mm wide and 38 mm long, about 11° from the guide. After fabrication we pressed copper rivets into the vias and soldered the SMA connectors. Measured on a FieldFox VNA, the waveguide transmits from about 2.2 to 6.1 GHz with close to zero loss and S11 around −40 dB at 3 GHz, within ±0.1 GHz and ±0.5 dB of the HFSS result.

## Power divider

The divider reuses the waveguide and splits the input between ports 2 and 3 with an iris, a partial wall of vias. The via pitch had to be relaxed from 2 mm to 4 mm because the board could not otherwise be made with the equipment at MSU; in simulation that reduces the bandwidth by about 0.4 GHz. We measured it on a two-port VNA without terminating the third port, so reflections dominate the response and the isolation cannot be judged. Without a matched load on the unused port the measurement is not valid, so we can only call the divider working in simulation.
