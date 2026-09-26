---
layout: page
title: Learning log pile clearing
description: Grasp targeting from raw point clouds, trained in simulation and deployed on a hydraulic forestry crane
img: assets/img/projects/crane_card.jpg
importance: 2
category: research
related_publications: sideris2026grasp, sideris2026thesis
---

Mill yards receive wood in dense piles that a grapple-equipped log loader must clear, cycle after cycle, all shift long. The task breaks most grasping assumptions: hundreds of near-identical logs rest in frictional contact, the grapple captures several at once, every grasp reshapes the pile, and the machine only sees a partial, noisy surface.

My master's thesis learns *where to grasp* directly from raw, unsegmented point clouds and carries the learned policy onto a physical forestry crane.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include video.liquid path="assets/video/crane_demo.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true loop=true muted=true %}
    </div>
</div>
<div class="caption">
    The Isaac Lab simulation: a crane clears a pile and stacks logs on a trailer, with continuous collision detection for clean contact resolution.
</div>

**Approach**

- **Simulation.** A GPU-parallel Isaac Lab environment of the crane, grapple and log pile, tuned from field measurements, supports demonstration collection and on-policy training across dozens of environments at once.
- **Policy.** A PointNet-style network scores every observed point, grasps at the highest-scoring one, and predicts grasp depth and grapple yaw there. It is trained by behavior cloning of a privileged-state expert and fine-tuned with PPO, using the same per-point scores as a categorical action distribution.
- **Sim-to-real.** A calibration campaign aligns simulated sensing and control with the physical testbed before deployment.

**Results**

In simulation, behavior cloning fully clears 98 of 100 piles of 200 logs, and RL fine-tuning improves load stability. In twelve field trials on the crane across three pile shapes, the learned policies deposited a larger share of the log inventory than the geometric heuristic previously deployed on the machine, and the fine-tuned policy had the highest rate of successful grasp-and-deposit cycles.

The work is supported by an FRQNT master's scholarship and a Mitacs Accelerate award with FPInnovations. A paper is under review for ICRA 2027, and the thesis is being completed in the Department of Mechanical Engineering at McGill under Prof. Inna Sharf.
