---
layout: page
title: STEPPED-IMPEDANCE LOW-PASS FILTER
description: A fifth-order Chebyshev stepped-impedance microstrip low-pass filter for 1.1 GHz, designed in ADS, fabricated on Rogers RO4350 and measured to meet its specifications.
img: assets/img/projects/lpf_layout.png
importance: 4
category: coursework
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/lpf_layout.png" title="Layout of the filter" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Layout of the filter.
</div>

An ECE 404 project, done with a lab partner. The filter is a fifth-order equal-ripple (Chebyshev) low-pass design on a Rogers RO4350 board (ε_r = 3.55, 1.524 mm thick) in a 50 Ω system. The specification: under 0.5 dB insertion loss up to 1.1 GHz, more than 16.5 dB attenuation from 1.7 GHz up, and more than 12 dB return loss in the passband, in under 4 in × 1.5 in with no line narrower than 0.4 mm.

## Design

We took normalized Chebyshev element values for 0.2 dB ripple and scaled them to lumped capacitors and inductors, then replaced each one with a section of line, alternating 15 Ω and 120 Ω. A Python script turned the element values into electrical lengths, and ADS LineCalc turned those into widths and lengths. We simulated the ideal and the microstrip circuit, then laid it out and ran an electromagnetic simulation. The first EM run was too lossy at 1.1 GHz (0.8 dB), and a small adjustment of the line dimensions brought it into specification.

## Results

In the EM simulation the passband ripple peaks at 0.38 dB, the attenuation at 1.7 GHz is about 25 dB, and the worst-case return loss is 12.4 dB. We then measured the fabricated filter on a VNA from 0.1 to 1.8 GHz after a full two-port SOLT calibration. It met the specification: more than 16.5 dB of attenuation at 1.7 GHz and a maximum ripple of 0.356 dB, with a near-perfect match at 0.8 and 1.1 GHz on the Smith chart.

The measured response sits slightly lower in frequency than the circuit simulation. We attribute that to the EM meshing, fabrication tolerance and variation in the substrate.
