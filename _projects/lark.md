---
layout: page
title: LARK
description: Low-cost, occlusion-resilient multi-camera optical tracking for image-guided surgery
img: assets/img/projects/lark_card.jpg
importance: 1
category: research
related_publications: true
---

Commercial optical trackers for image-guided surgery cost US$8,000 to US$25,000 and lose the instrument the moment a hand or a drape blocks the line of sight. LARK is an open-source alternative that puts a ring of RGB cameras on the surgical light itself, so that some camera almost always sees the tool, and fuses their estimates with an adaptive Kalman filter.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        <img src="/assets/img/projects/lark_demo.gif" alt="LARK tracking a surgical pointer on a head phantom: five camera views and the live visualization" class="img-fluid rounded z-depth-1" style="width:100%;">
    </div>
</div>
<div class="caption">
    Live trajectory tracking on the head phantom: the five camera views and the live visualization as the pointer follows grooves on the cranial surface. Full <a href="https://youtu.be/ApZ8q9DjB-4">supplementary video</a>.
</div>

**What it does**

- Tracks a surgical pointer and a static patient reference with ArUco fiducials seen from multiple calibrated cameras, using two complete methods: multi-view monocular pose fusion and multi-view triangulation.
- Reaches median target registration errors of 0.64 mm (static) and 0.73 mm (dynamic).
- Degrades gracefully as cameras are occluded or removed, instead of dropping out.
- Tracking hardware costs under US$1,000, an order of magnitude below commercial systems.

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

I led the four-student team, co-designed and fabricated the light-mounted camera fixture, co-implemented multi-camera calibration and fiducial tracking, and developed the adaptive Kalman-filter fusion with online per-camera noise estimation. The project won 2nd place in the McGill Engine Capstone Design Prize for Entrepreneurship and grew into OPSIS, which I co-founded through McGill Engine's TechAccel program (2024–2026) to bring the tracker toward clinical use.

The preprint is on [arXiv](https://arxiv.org/abs/2610.07561) and the manuscript is submitted to Medical Image Analysis {% cite sideris2026lark %}. Code, calibration tools, marker generation and Raspberry Pi camera nodes are on [GitHub](https://github.com/george-sideris/LARK); hardware designs and software are also published on the [NIST lab software page](https://nist.mni.mcgill.ca/software/), with datasets on the [data page](https://nist.mni.mcgill.ca/data/).
