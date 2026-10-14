---
layout: page
title: Camera-glove data capture for Bracket Bot
description: A UMI-style handheld rig that turns bimanual human demonstrations into robot training episodes, without teleoperation
img: assets/img/projects/glove_card.gif
importance: 3
category: research
---

Demonstrations are the bottleneck for learning manipulation, and teleoperating a robot to collect them is slow and ties up a machine. [UMI](https://umi-gripper.github.io/) showed that a wrist camera on a handheld gripper can record demonstrations with no robot in the loop. I brought that to [Bracket Bot](https://bracketbot.com/): in four and a half days in May 2026 I built a two-handed capture rig and the full pipeline behind it, from two Insta360 cameras on real Bracket Bot grippers through marker tracking, visual-odometry gap filling, smoothing, hand-eye alignment and inverse kinematics, ending in episode files that drop straight into their existing training pipeline.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        <img src="/assets/img/projects/glove_demo.gif" alt="Both wrist cameras during a bimanual pick, with tracked pose axes, detected markers and live trajectory insets" class="img-fluid rounded z-depth-1" style="width:100%;">
    </div>
</div>
<div class="caption">
    Both wrist cameras during a bimanual pick: the tracked camera pose (axes), the detected workspace and jaw markers, the gripper opening angle, and live top and isometric views of each hand's trajectory.
</div>

**How it works**

- **Hardware.** Two grippers salvaged from broken Bracket Bots, so the captured embodiment is identical to the robot's, retrofitted with 3D-printed finger slots for manual open/close and a printed mount for an Insta360 (X2 on one hand, X3 on the other). The motor lead is left exposed for a future powered open/close with encoder feedback.
- **Capture.** Each camera streams dual-fisheye H.264 video and a 6-axis IMU over USB. One process per camera, barrier-synced at 20 fps so both hands' frames line up; the IMU is recorded raw. 20 fps was deliberate: at 30 fps the inter-frame baseline is too short for stable visual odometry.
- **Pose tracking.** The workspace-facing lens sees a 20-tag AprilGrid; after fisheye calibration, multi-marker PnP gives a metric 6-DoF camera pose. When the markers drop out, ORB visual odometry bridges the gap, with its scale recovered from the metric marker poses at either end. A constant-velocity Kalman filter on translation, SLERP on rotation and an outlier gate (0.07 m or 15° off the prediction) turn the jittery raw track into a clean trajectory.
- **Gripper angle.** Fiducials on each jaw give the opening angle from their relative rotation, with pose-ambiguity disambiguation to kill sign flips, spike rejection and smoothing.
- **Robot alignment.** A measured camera-to-end-effector offset composed with the URDF, first-frame anchoring onto each arm's home pose, then Bracket Bot's own IK solver maps every pose to 8-DoF arm commands, verified by replaying recorded trajectories on the robot model in an interactive viewer.
- **Output.** Per episode: metric, timestamped trajectories for both arms, synchronized wrist video and raw IMU, written in Bracket Bot's episode schema. One command records, processes, opens the viewer and asks keep or reject.

<div class="row">
    <div class="col-sm-8 mt-3 mt-md-0">
        <img src="/assets/img/projects/glove_rerun_live.gif" alt="Rerun viewer replaying an episode: both hands' 3D trajectories over the workspace markers, with the two wrist camera streams" class="img-fluid rounded z-depth-1" style="width:100%;">
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/glove_ik_replay.jpg" title="IK replay on the robot model" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: an episode in the Rerun viewer, with both hands' tracked trajectories (left red, right blue) above the workspace markers, alongside the two wrist camera streams. Right: the same kind of trajectory replayed through inverse kinematics on the Bracket Bot model.
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        <img src="/assets/img/projects/glove_postprocessing.gif" alt="Four-stage trajectory post-processing animation: raw PnP, Kalman and SLERP, visual-odometry fill, outlier rejection" class="img-fluid rounded z-depth-1" style="width:100%;">
    </div>
</div>
<div class="caption">
    One bimanual episode (left hand red, right hand blue) at each post-processing stage, left to right: the raw per-frame marker PnP, jittery with gaps; after the Kalman filter on translation and SLERP on rotation smooth it; after ORB visual odometry fills the gaps where the markers were lost; and after the outlier gate removes the remaining PnP flips.
</div>

<div class="row">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/glove_rig.jpg" title="The capture rig" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        <img src="/assets/img/projects/glove_hand.gif" alt="A gripper-glove held in one hand, jaws opened and closed by the fingers, with the Insta360 mounted on top" class="img-fluid rounded z-depth-1" style="width:100%;">
    </div>
</div>
<div class="caption">
    Left: two Bracket Bot grippers with printed camera mounts and finger slots, and the AprilGrid workspace board that anchors the tracking. Right: one glove in hand, jaws worked by the fingers, camera on top.
</div>

**Outcome**

About 80 bimanual episodes, roughly 21 minutes of synchronized data, were delivered in Bracket Bot's training format together with the repository they re-run on their own robot to extend the dataset. The next steps I scoped are motorized grippers with encoder readout, a ChArUco board that I benchmarked to about twice the AprilGrid's detection range, operator-anchored capture using the idle second lens, and reusing the pose-to-IK path for live teleoperation. The code was delivered to Bracket Bot as a private repository.
