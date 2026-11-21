---
layout: page
title: STEPPED-IMPEDANCE LOW-PASS FILTER
description: Design, simulation, fabrication and testing of a fifth-order Chebyshev stepped-impedance low-pass filter with a cutoff of 1.1 GHz on a Rogers RO4350 substrate. It met the design specifications.
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

This ECE 404 project, done with Avery Wiklund (now at CU Boulder, working with Dr. Taylor Barton), was the design, simulation, fabrication and testing of a fifth-order (N = 5) stepped-impedance equal-ripple (Chebyshev) low-pass filter on a Rogers RO4350 substrate (εr = 3.55, tan δ = 0.003, thickness = 1.524 mm). The filter is for a 50 Ω system with less than 0.5 dB insertion loss at 1.1 GHz and below, greater than 16.5 dB attenuation at 1.7 GHz and above, and greater than 12 dB return loss in the S11 passband. It had to be under 4 in x 1.5 in and could not use lines less than 0.4 mm in width or length.

## Design

We used a table of normalized Chebyshev element values, like the ones in Pozar's Microwave Engineering, and Python to get the lumped component values. We turned those into stepped-impedance sections of 15 and 120 Ω using impedance scaling and LineCalc in Keysight ADS. We simulated the ideal (TLIN) and the microstrip (MLIN) circuits, laid it out in the ADS layout tool and ran an EM simulation. We struggled to get the EM simulation to match at first, because we were at -0.8 dB insertion loss at 1.1 GHz, so we had to adjust the lengths and widths of the lines.

## Results

In the EM simulation the passband insertion loss peaks at -0.38 dB, we have about 25 dB of attenuation at 1.7 GHz and the peak of S11 is -12.4 dB. After fabrication we measured the filter on a VNA from 0.1 to 1.8 GHz with a full two-port SOLT calibration. We met our design specifications: greater than 16.5 dB of attenuation at 1.7 GHz and a maximum ripple of 0.356 dB. The Smith charts show a near-perfect match at 0.8 and 1.1 GHz.

The measured response is shifted slightly left of the circuit simulation. We attribute this to the EM meshing, fabrication tolerances, connector losses and variations in the substrate.
