---
layout: page
title: "E(3)-Pose: Equivariant symmetry-aware head pose estimation for fetal brain MRI"
permalink: /e3-pose/
---

COMING SOON!

## Abstract ##
We present E(3)-Pose, a novel fast pose estimation method that jointly and explicitly models rotation equivariance and object symmetry. Our work is motivated by the challenging problem of accounting for fetal head motion during a diagnostic MRI scan. We aim to enable automatic adaptive prescription of 2D diagnostic MRI slices with 6-DoF head pose estimation, supported by 3D MRI volumes rapidly acquired before each 2D slice. Existing methods struggle to generalize to clinical volumes, due to pose ambiguities induced by inherent anatomical symmetries, as well as low resolution, noise, and artifacts. In contrast, E(3)-Pose captures anatomical symmetries and rigid pose equivariance by construction, and yields robust estimates of the fetal head pose. Our experiments on publicly available and representative clinical fetal MRI datasets demonstrate the superior robustness and generalization of our method across domains. Crucially, E(3)-Pose achieves state-of-the-art accuracy on clinical MRI volumes, paving the way for clinical translation.

## Method ##

## Results ##

## In-utero Demo ##

We implemented a feedback loop system that dynamically translates the navigator field-of-view (FOV) to follow the translational movements of the fetal head. We provide examples in a 31 and 28 week old fetus, respectively.

<div class="row mt-3">
        {% include video.html path="/assets/video/vnav_shift_1_audio_GOOD.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
</div>
<div class="row mt-3">
        {% include video.html path="/assets/video/vnav_shift_2_audio_GOOD.mp4" class="img-fluid rounded z-depth-1" controls=true %}
</div>
<div class="caption">
    <i>Left:</i> the navigator FOV center (red) is dynamically translated to accurately follow the ground-truth fetal head center-of-mass (blue). <i>Middle:</i> our translated navigator volumes minimize the distance between the two. <i>Right:</i> translated navigator volumes align the FOV center (star) with the estimated brain segmentation mask (green outline). The dark bands in the navigator volumes represent spin history artifacts from the 2D diagnostic MRI slices.
</div>