---
layout: page
title: "PATCH ANTENNA: 3 GHZ"
description: An inset-fed microstrip patch antenna for 3 GHz, designed in HFSS, fabricated on a Rogers board and characterised in an anechoic chamber.
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

An ECE 405 project, done with a lab partner. We designed a rectangular inset-fed patch antenna for 3 GHz on a 50 × 50 mm Rogers RO4350B board, with a 50 Ω microstrip feed and an SMA connector.

## Design

The standard formulas give a patch width of 33.13 mm and, with the fringing-field correction, a length of 26.06 mm. The input impedance at the patch edge is about 251 Ω, so we cut an inset into the patch to match it to the 50 Ω feed. The textbook inset formula gave a starting gap, but HFSS showed that it moved the resonance, so we swept the ratio of gap to feed-line width in steps of 0.1 and chose 1.3, a 4.5 mm gap with a 6.83 mm inset depth. That puts the simulated resonance at 2.991 GHz.

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

We measured S11 on a FieldFox VNA. For the radiation patterns we mounted the antenna in the MSU anechoic chamber with a Vivaldi antenna as the receiver, and rotated it in 5° steps, once for the E-plane and once for the H-plane. The measured co-polar patterns match the HFSS patterns closely. The cross-polar patterns do not, which we put down to mounting and polarization alignment, since the antenna was held with tape. With the two-antenna method we measured a gain of about 4.6 dB.

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
