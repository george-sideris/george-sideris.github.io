---
layout: page
title: Learning log pile clearing
description: Grasp targeting from raw point clouds, trained in simulation and deployed unchanged on a hydraulic forestry crane
img: assets/img/projects/crane_demo.gif
importance: 2
category: research
related_publications: true
---

Mill yards receive wood in dense piles that a grapple-equipped log loader must clear, cycle after cycle, all shift long. The task breaks most grasping assumptions: hundreds of near-identical logs rest in frictional contact, the grapple captures several at once, every grasp reshapes the pile, and the machine only sees a partial, noisy surface.

My master's thesis learns *where to grasp* directly from raw, unsegmented point clouds and carries the learned policy onto a physical forestry crane.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        <img src="/assets/img/projects/crane_demo.gif" alt="Eight simulated cranes clearing log piles in parallel, then the real crane clearing a pile in a field trial" class="img-fluid rounded z-depth-1" style="width:100%;">
    </div>
</div>
<div class="caption">
    Eight environments clearing in parallel in simulation, then the same policy on the trailer-mounted hydraulic crane during a field trial. Full <a href="https://youtu.be/woyDNW_oN7A">supplementary video</a>.
</div>

**Approach**

- **Simulation.** A GPU-parallel Isaac Lab environment of the crane, grapple and log pile, tuned from field measurements, supports demonstration collection and on-policy training across dozens of environments at once.
- **Policy.** A PointNet-based network classifies at which observed point to grasp and predicts depth and grapple orientation there. The same outputs support behavior cloning from a privileged-state expert, reinforcement-learning fine-tuning (BC→RL) or training from scratch, and deployment.
- **Sim-to-real.** A calibration campaign, carried out during a Mitacs Accelerate internship with FPInnovations, aligns simulated sensing and control with the physical testbed, and the policies run unchanged on the crane.

**Results**

In simulation, behavior cloning clears 98 of 100 piles of 200 logs, and BC→RL improves load stability. Twelve field trials compared a geometric heuristic baseline (which I also implemented), RL from scratch, BC, and BC→RL through complete grasp-transport-deposit cycles. BC and BC→RL deposited 93.8% and 88.9% of the pooled log inventory, against 80.4% for the heuristic, and BC→RL deposited logs on 83.6% of its cycles, against 79.6% for the heuristic and 65.7% for BC. The learned policies did this while observing unfiltered point clouds that still contained the storage rack's rails and poles.

The paper is on [arXiv](https://arxiv.org/abs/2610.07613) and under review for ICRA 2027 {% cite sideris2026grasp %}. The work was supported by an FRQNT master's scholarship and a Mitacs Accelerate internship with FPInnovations, and is the subject of my M.Sc. thesis {% cite sideris2026thesis %} in the Department of Mechanical Engineering at McGill under Prof. Inna Sharf.
