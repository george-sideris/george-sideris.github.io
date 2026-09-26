---
layout: page
title: LARK
description: Low-cost, occlusion-resilient multi-camera optical tracking for image-guided surgery
img: assets/img/projects/lark_card.jpg
importance: 1
category: research
related_publications: sideris2025lark
---

Commercial optical trackers for image-guided surgery cost $8,000 to $25,000 and lose the instrument the moment a hand or a drape blocks the line of sight. LARK is an open-source alternative that puts a ring of RGB cameras on the surgical light itself, so that some camera almost always sees the tool, and fuses their estimates with an adaptive Kalman filter.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include video.liquid path="assets/video/lark_demo.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true loop=true muted=true %}
    </div>
</div>
<div class="caption">
    Real-time tracking of a surgical pointer during a head-phantom trial.
</div>

**What it does**

- Tracks a surgical pointer and a static patient reference with ArUco fiducials seen from multiple calibrated cameras.
- Reaches median target registration errors of 0.64 mm (static) and 0.73 mm (dynamic).
- Degrades gracefully under partial occlusion instead of dropping out.
- Costs about $1,000 USD in parts, an order of magnitude below commercial systems.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/lark_overview.png" title="System overview" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/lark_ring.png" title="Ring fixture model" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: camera ring, pointer, static reference and head phantom. Right: the ring fixture that mounts on the operating-room light.
</div>

**My role**

I led the four-student team, co-designed and fabricated the light-mounted camera fixture, co-implemented multi-camera calibration and fiducial tracking, and designed the adaptive Kalman-filter fusion. The project won 2nd place in the McGill Engine Capstone Design Prize for Entrepreneurship and grew into [OPSIS](/cv/), a startup I co-founded to bring the tracker toward clinical use.

Code, calibration tools, marker generation and Raspberry Pi camera nodes are on [GitHub](https://github.com/george-sideris/LARK). The preprint is on [Research Square](https://www.researchsquare.com/article/rs-7622287/v1) and the manuscript is under review at IEEE Transactions on Robotics.
