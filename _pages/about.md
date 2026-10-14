---
layout: about
title: about
permalink: /
subtitle: Robotics Research Engineer, <a href="https://bracketbot.com/">Bracket Bot</a> · M.Sc. Mechanical Engineering, <a href="https://www.mcgill.ca/mecheng/">McGill University</a>

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>San Francisco, CA</p>

selected_papers: true # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page

announcements:
  enabled: false
  scrollable: true
  limit: 5

latest_posts:
  enabled: false
  scrollable: true
  limit: 3
---

I work on learning-based manipulation. Since October 2026 I am a Robotics Research Engineer at Bracket Bot in San Francisco. My interests are moving toward world models and reinforcement learning for manipulation.

During my M.Sc. in Mechanical Engineering at McGill (expected Fall 2026), with [Prof. Inna Sharf](https://www.mcgill.ca/mecheng/people/staff/inna-sharf) at the [Aerospace Mechatronics Lab](https://aerospacemechatronics.lab.mcgill.ca/), I taught a hydraulic forestry crane to clear dense log piles. A policy that reads raw point clouds decides where to sink the grapple, is trained by imitation and reinforcement learning in a GPU-parallel Isaac Lab simulation, and was deployed unchanged in field trials on the crane, where it cleared more of the pile than the geometric heuristic baseline I had also implemented ([arXiv](https://arxiv.org/abs/2610.07613), under review at ICRA 2027). Part of that work was a Mitacs Accelerate internship with FPInnovations.

Before that, I led a four-student team at the [NeuroImaging and Surgical Technologies Lab](https://nist.mni.mcgill.ca/) (Prof. D. Louis Collins) at [The Neuro](https://www.mcgill.ca/neuro/) (Montreal Neurological Institute-Hospital) building [LARK](/projects/lark/), a multi-camera optical tracker for image-guided surgery that reaches sub-millimeter accuracy with under US$1,000 of hardware ([arXiv](https://arxiv.org/abs/2610.07561), submitted to Medical Image Analysis). I co-founded OPSIS to explore commercializing the tracker; we completed McGill Engine's TechAccel program and received the Ian McLachlin Prize for Entrepreneurship.

Even before that, I interned at Lockheed Martin CES and Bombardier Aerospace, and led student design teams: the McGill Vertical Flight Society drone team as captain and co-captain, and competition robotics teams at Marianopolis College in the Canadian Robotics Competition.

<div class="row mt-4 mb-2">
    <div class="col-sm-6 mt-3 mt-sm-0">
        <a href="/projects/log-pile-clearing/">
            <img src="/assets/img/projects/crane_demo.gif" alt="Learned grasp targeting: eight simulated cranes clearing log piles in parallel, then the real crane in a field trial" class="img-fluid rounded z-depth-1" style="width:100%;">
        </a>
        <div class="caption"><a href="/projects/log-pile-clearing/">Learning log pile clearing</a>: trained in parallel simulation, deployed unchanged on a hydraulic crane.</div>
    </div>
    <div class="col-sm-6 mt-3 mt-sm-0">
        <a href="/projects/lark/">
            <img src="/assets/img/projects/lark_demo.gif" alt="LARK tracking a surgical pointer on a head phantom from five cameras with a live visualization" class="img-fluid rounded z-depth-1" style="width:100%;">
        </a>
        <div class="caption"><a href="/projects/lark/">LARK</a>: live multi-camera, plain-RGB, sub-millimeter tracking of a surgical pointer on a head phantom.</div>
    </div>
</div>

The best feedback loop is learning to build and building to learn.
