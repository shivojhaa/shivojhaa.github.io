---
layout: page
title: FABRICATION AND VALIDATION OF SI RESISTOR
description: A diffused resistor fabricated in the cleanroom (ECE 877), modeled analytically, in Python and in Sentaurus, and compared with the measurement. The measured resistance came out far below the predictions.
img: assets/img/projects/resistor_section.png
importance: 7
category: coursework
---

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/resistor_section.png" title="Cross-section of the resistor" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Cross-section of the resistor.
</div>

In ECE 877 (Cleanroom Procedures) we worked through the full process of designing, fabricating and testing semiconductor devices, including diodes, FETs, basic CMOS circuits and resistors. This page is about Resistor Six (R6), a 2D diffused resistor on a p-type silicon wafer. The goal was to understand both the theoretical and practical sides of device engineering and to compare the fabricated device with the modeled one.

## Fabrication

We grew oxide with PECVD and patterned it with g-line lithography and an HF etch. We then did diffusion doping with phosphosilicate glass to make the n-type region (a 60 minute predeposition at 950 °C, then a 50 minute drive-in with thermal oxidation), and deposited about 500 nm of aluminum for the contact pads by e-beam evaporation. We measured the device with a four-point probe sweep from -5 V to 5 V.

## Analysis and validation

From the four-point probe measurements the wafer has a sheet resistance of 366 Ω/□, which gave us the substrate doping. From the diffusion steps I calculated the junction depth and the dopant concentration analytically, and then the resistance. I also built a Sentaurus SDE model of the process and wrote my own Python solvers (Newton-Raphson and a nonlinear Poisson solver), because no single result can be relied on for total accuracy.

The results did not agree. The calculation gives about 226 Ω, Sentaurus gives about 167 Ω, and the fabricated resistor measured about 83 Ω. I think the oxide was not good enough during the diffusion doping, either because it was too thin or because the patterning failed, so a thin n+ film formed on the p-type substrate. That gives extra conduction paths and lowers the resistance.
