---
layout: page
title: Hierarchical RL for crane log grasping
description: Open-source Isaac Lab environment where a policy picks grasp targets and a state machine executes the pick-place cycle
img: assets/img/projects/crane_training.png
importance: 3
category: research
---

An open-source simulation environment for learning forestry crane manipulation with hierarchical reinforcement learning in NVIDIA Isaac Lab. It is the public precursor to the [log pile clearing](/projects/log-pile-clearing/) work.

**Architecture**

- **High-level RL policy** selects a grasp target (x, y, z, yaw).
- **Low-level FSM controller** executes a 10-phase pick-place cycle with inverse kinematics.
- **Reward** is multiplicative (logs grasped × alignment) with a bonus for well-aligned loads.

One policy step runs one complete grasp cycle, roughly 900 physics steps, so the RL problem is a short sequence of high-value decisions rather than a long stream of joint commands. The environment supports up to 64 parallel simulations, a dual-stack deposition system with spatial constraints, and a heuristic baseline (grasp the highest visible log) for comparison.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/crane_training.png" title="Training curves" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Training curves for the grasp-targeting policy.
</div>

Code: [github.com/george-sideris/crane-hierarchical-rl](https://github.com/george-sideris/crane-hierarchical-rl)
