---
layout: page
title: "PATCH ANTENNA: 3 GHZ"
description: An inset-fed patch antenna for 3 GHz on a Rogers 4350B substrate with a 50-ohm feed, designed in Ansys HFSS, fabricated, and characterized with a VNA and in an anechoic chamber.
img: assets/img/projects/patch_board.png
importance: 6
category: coursework
---

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/patch_board.png" title="The fabricated patch antenna" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The fabricated patch antenna.
</div>

In this ECE 405 project, done with Grant Bell, we were tasked with designing a patch antenna to operate around 3 GHz. It is on a Rogers 4350B substrate with a single port, using a 3.5 mm coaxial connector so that it works with the VNA, and the impedance is matched to 50 Ω. We designed and simulated it in Ansys HFSS, had the PCB fabricated at MSU, soldered on the connector and then measured it in an anechoic chamber with a VNA.

## Design

From the patch antenna formulas we got W = 33.13 mm and L = 26.06 mm, using the effective dielectric constant of 3.55 that Rogers gives. The input impedance of the patch is about 251 Ω, so we used an inset feed to match it to the 50 Ω line, which is 3.46 mm wide from ADS LineCalc. The inset formulas gave a starting spacing of 5.19 mm, but in HFSS that shifted the resonance. We swept the ratio of spacing to feed width from 1.0 to 2.0 in steps of 0.1, and 1.3 worked best. That gives S = 4.5 mm and D = 6.83 mm, and a simulated resonance of 2.991 GHz.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/patch_model.png" title="HFSS model with dimensions" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    HFSS model with dimensions in mm.
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/patch_s11.png" title="S11 against frequency" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    S11 against frequency.
</div>

## Measurement

We measured S11 from 1 to 5 GHz on a Keysight FieldFox VNA. For the radiation patterns we mounted the antenna in the anechoic chamber with a Vivaldi antenna as the receiver and rotated it in 5 degree steps, measuring the E and H planes at 3 GHz. Our measured co-pole patterns match the HFSS simulation. The cross-pole patterns do not match. This could be a high polarization loss factor, because the antenna was held in place with tape and may not have been aligned well, or it could be bad measurements or an improper setup. With the two-antenna method we got a gain of 4.6 dB.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/patch_chamber.png" title="Anechoic chamber setup" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Anechoic chamber setup.
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/patch_pattern.png" title="Radiation patterns at 3 GHz" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Radiation patterns at 3 GHz: E and H co-pol compared with the simulated H-plane and E-plane co-pol.
</div>
