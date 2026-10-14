---
layout: page
title: Log-loader grapple perception and anti-sway testbed
description: A lab-scale stand-in for a forestry crane's swaying grapple, and image datasets for grapple characterization (ICRA 2025)
img: assets/img/projects/testbed_setup.jpg
importance: 4
category: research
related_publications: true
---

Forestry machines are large, expensive and hard to experiment with: testing a new controller means outdoor space, permits and a full-size crane. As a SURE undergraduate researcher at the [Aerospace Mechatronics Lab](https://aerospacemechatronics.lab.mcgill.ca/) in summer 2023, I worked on two pieces of the lab's push toward autonomous log loaders, both aimed at making that experimentation possible indoors.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/testbed_setup.jpg" title="Kinova arm with the passive grapple linkage" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The passive end-effector linkage mounted on the Kinova Jaco2 arm, which replays log-loader trajectories so the sway of the suspended load can be measured.
</div>

**Anti-sway testbed**

A log loader positions its grapple with four hydraulic joints, but the grapple hangs from two passive support joints, so every fast motion sets it swinging. To validate an anti-sway trajectory planner without a crane, the lab emulates the machine with a Kinova Jaco2 arm carrying a custom passive linkage that behaves like the real support-joint-and-grapple assembly at reduced scale.

I designed and manufactured that linkage:

- **Kinematics.** A fixed mount, two passive revolute joints offset by 90 degrees and a payload at the free end, replicating the log loader's passive support joints. Rotation limits of ±130° and ±45° are cut into the hinges so the load cannot swing into the arm.
- **Low friction.** Clevis joints on press-fit flanged ball bearings, so the sway is amplified rather than damped and can be measured cleanly.
- **Construction.** Machined aluminum links (about 16 inches end to end in the working configuration) with a 3D-printed mount bracket that clips onto the arm's gripper through its camera stand and gives the fingers a handle to grasp, all under the 2 kg budget left by the arm's payload limit.
- **Instrumentation and modularity.** A printed bracket carries an IMU on the last link to quantify sway, and stackable 0.5 kg pucks let the payload be set to 0.5, 1 or 1.5 kg depending on the sway range wanted.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/testbed_linkage.jpg" title="The linkage" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/testbed_linkage_cad.jpg" title="Linkage CAD" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: the linkage with its clevis joints and IMU bracket. Right: the CAD model, with the mount bracket, links L0 to L2 and the two passive joints.
</div>

On this testbed, the lab's dynamic-programming anti-sway planner was evaluated on point-to-point moves, each repeated at least six times, and showed strong sway damping with good repeatability. The work was published at ICRA 2025 {% cite jebellat2025antisway %}.

**Grapple characterization from images**

The second piece was perception: estimating from a camera what the grapple is doing. I built the image datasets and trained a CNN for grapple and log segmentation, grapple-opening prediction and log counting, and integrated a draw-wire sensor on the grapple so the network's opening estimates could be validated against a physical measurement.
