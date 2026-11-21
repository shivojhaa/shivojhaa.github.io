---
layout: page
title: SUBSTRATE INTEGRATED WAVEGUIDE AND POWER DIVIDER
description: A 2-port substrate integrated waveguide and a 3-port power divider on a Rogers substrate, designed in Ansys HFSS and fabricated. The waveguide matched the simulation and the power divider is only functional in simulation.
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

Project 1 of ECE 405, done with Grant Bell, explores the design of substrate integrated waveguides, or SIWs. An SIW is a type of waveguide that is integrated into a PCB substrate, and the wave is guided by walls of vias drilled into the substrate. It has lower losses than microstrip in the S-band. We designed a 2-port waveguide and a 3-port power divider in Ansys HFSS on a Rogers substrate, and both were fabricated by Mr. Brian Wright at MSU Technologies.

## Waveguide

We were given the via diameter (1 mm), the pitch between vias (2 mm) and the spacing between the via walls (3.87 cm). The distance between the via walls sets how the waveguide behaves, not its length, so we chose a length of 50 mm. The 50 Ω microstrip is 3.65 mm wide from ADS LineCalc and 10 mm long. We tuned the triangular taper in HFSS and it ended up 7.3 mm wide and 38 mm long, about a 10.87 degree angle with the SIW. After fabrication we pressed copper rivets into the vias and soldered 3.5 mm SMA connectors to the ports.

We measured it on a Keysight FieldFox VNA. The waveguide has broadband transmission from about 2.2 to 6.1 GHz with near-zero loss, and S11 peaks at -40 dB around 3 GHz, our center frequency. The measurement matched our HFSS simulation within ±0.1 GHz and ±0.5 dB. For the TE10 mode the cutoff frequency is about 2.06 GHz.

## Power divider

The power divider reuses our SIW design, with an iris, an additional wall of vias, between ports 2 and 3. Late in the design we had to change the via pitch from 2 mm to 4 mm, because the large number of vias made the board non-manufacturable with the equipment at MSU. In simulation this decreased the bandwidth by about 0.4 GHz.

The FieldFox only has two ports and we did not terminate the third port with a 50 Ω load, so we see resonance in our S-parameters and no isolation between ports 2 and 3. Because of this we can only call the power divider functional in a simulated environment.
