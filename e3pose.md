---
layout: page
title: "E(3)-Pose"
permalink: /e3-pose/
---
<h4 style="text-align: center;">Equivariant symmetry-aware head pose estimation for fetal MRI</h4>
<div class="container">
  <div id="authors">
      <div class="row mt-3">
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://ramyamut.github.io" target="_blank">Ramya<br> Muthukrishnan</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://connects.catalyst.harvard.edu/Profiles/display/Person/105811" target="_blank">Borjan<br> Gagoski</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://labs.childrenshospital.org/mortonlab/people/aryn-lee" target="_blank">Aryn<br> Lee</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://research.childrenshospital.org/researchers/patricia-ellen-grant" target="_blank">P. Ellen<br> Grant</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://imes.mit.edu/people/adalsteinsson-elfar" target="_blank">Elfar<br> Adalsteinsson</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://people.csail.mit.edu/polina/" target="_blank">Polina<br> Golland</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://bbillot.github.io/" target="_blank">Benjamin<br> Billot</a></div>
      </div>
      <div class="row mt-3">
          <div class="col-sm mt-3 mt-md-0 text-center">MIT <br> CSAIL</div>
          <div class="col-sm mt-3 mt-md-0 text-center">Boston Children's<br> Hospital</div>
          <div class="col-sm mt-3 mt-md-0 text-center">Harvard <br> Medical School</div>
          <div class="col-sm mt-3 mt-md-0 text-center">Inria<br> Université Côte d’Azur</div>
      </div>
  </div>
  <div style="clear: both">
      <div class="row mt-3 text-center">
          <a class="col-sm mt-3 mt-md-0 btn btn-paper mx-2" href="https://arxiv.org/abs/2512.04890">Paper</a>
          <a class="col-sm mt-3 mt-md-0 btn btn-code mx-2" href="https://github.com/MedicalVisionGroup/E3-Pose" target="_blank">Code</a>
          <a class="col-sm mt-3 mt-md-0 btn btn-code mx-2" href="https://drive.google.com/drive/folders/1r6FVzXG9VLH-0MtMnD2hwjzdDqss1DSE" target="_blank">Model</a>
          <a class="col-sm mt-3 mt-md-0 btn btn-data mx-2" href="https://drive.google.com/file/d/1yO2o2sNNNEfcB_-ZDcVvHyCGxqk6SYyE/view?usp=drive_link" target="_blank">Data</a>
      </div>
  </div>
</div>
<br>
<h2 style="text-align: center;">Abstract</h2>
<p style="text-align: center;">We present E(3)-Pose, a novel fast pose estimation method that jointly and explicitly models rotation equivariance and object symmetry. Our work is motivated by the challenging problem of accounting for fetal head motion during a diagnostic MRI scan. We aim to enable automatic adaptive prescription of 2D diagnostic MRI slices with 6-DoF head pose estimation, supported by 3D MRI volumes rapidly acquired before each 2D slice. Existing methods struggle to generalize to clinical volumes, due to pose ambiguities induced by inherent anatomical symmetries, as well as low resolution, noise, and artifacts. In contrast, E(3)-Pose captures anatomical symmetries and rigid pose equivariance by construction, and yields robust estimates of the fetal head pose. Our experiments on publicly available and representative clinical fetal MRI datasets demonstrate the superior robustness and generalization of our method across domains. Crucially, E(3)-Pose achieves state-of-the-art accuracy on clinical MRI volumes, supporting future clinical translation.</p>

<h2 style="text-align: center;">Method</h2>
<div class="row mt-3">
        {% include figure.html path="/assets/img/teaser.png" class="img-fluid rounded z-depth-1"%}
</div>
<div class="caption">
    <b>E(3)-Pose is a rotation-equivariant and symmetry-aware framework for 6-DoF pose estimation. </b><i>Left:</i> a rapid navigator volume is inserted between every two 2D diagnostic MRI slices. It is used to estimate the fetal head pose to adjust imaging plane prescription in real time. <i>Right:</i> To enable robust performance, the network architecture employs E(3)-equivariant convolutional filters to capture pose equivariance and pseudovectors to account for left-right head symmetry.

</div>
<div class="row mt-3">
        {% include figure.html path="/assets/img/method_overview.png" class="img-fluid rounded z-depth-1"%}
</div>
<div class="caption">
    <b>Overview of E(3)-Pose.</b> We first train a CNN \(\psi\) to segment the object. We estimate translation based on the center-of-mass of the predicted mask and then crop the 3D volumes around this mask using a 40% margin. The cropped volumes are fed to an E(3)-CNN \(\phi\) trained independently to regress the orthonormal basis of the object frame, parametrized as one pseudovector (red) and two vectors (blue and green). The output is later constrained to represent a rotation matrix by applying SVD and then choosing the pseudovector \(e_x\) direction that results in a proper rotation without reflection (i.e., \(\det(M(\hat{R})) = 1\)).
</div>

<h2 style="text-align: center;">Results</h2>
<div class="row mt-3">
        {% include figure.html path="/assets/img/all_examples.png" class="img-fluid rounded z-depth-1"%}
</div>
<div class="caption">
    <b>Example results.</b> Volumes are displayed before (row 1) and after (rows 2-6) alignment to the canonical object frame. The brain mask is also aligned to the GT (green outline) and predicted (red outline) frames. Navigator volumes include spin history artifacts (blue arrows) and low resolution/SNR, posing challenges for pose estimation. While baseline methods struggle (red Xs, rotation error\(> 60^\circ\)) in younger fetuses (column 3) and navigator volumes (columns 4-6), E(3)-Pose correctly predicts pose in all cases. E(3)-Pose remains accurate under significant pose ambiguity, e.g. when the artifact intersects both eyes, large voxel size obscures brain structure, and the fetal brain is close to a sphere (column 6).
</div>
<div class="row mt-3">
        {% include figure.html path="/assets/img/simulation_study.png" class="img-fluid rounded z-depth-1"%}
</div>
<div class="caption">
    <b>Simulation results.</b> <i>Left:</i> Quantitative comparison of diagnostic slice stacks obtained using motion-blind prescription and E(3)-Pose. Mean ± standard deviation statistics are displayed. * indicates statistical significance (\(p<0.05\), pairwise Wilcoxon). <i>Right:</i> Brain coverage of the diagnostic slice stacks prescribed by each method, for three different example subjects and target anatomical orientations. Coverage gap (red) and obliqueness (purple, \(^\circ\)) metrics are respectively displayed. Spatial coverage gap regions are outlined in red.

</div>

<h2 style="text-align: center;">In-utero demo</h2>

<p style="text-align: center;">We implemented a feedback loop system that dynamically translates the navigator field-of-view (FOV) to follow the translational movements of the fetal head. We provide examples in a 31 and 28 week old fetus, respectively.</p>

<div class="row mt-3">
        {% include video.html path="/assets/video/vnav_shift_1_audio_GOOD.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
</div>
<div class="row mt-3">
        {% include video.html path="/assets/video/vnav_shift_2_audio_GOOD.mp4" class="img-fluid rounded z-depth-1" controls=true %}
</div>
<div class="caption">
    <i>Left:</i> the navigator FOV center (red) is dynamically translated to accurately follow the ground-truth fetal head center-of-mass (blue). <i>Middle:</i> our translated navigator volumes minimize the distance between the two. <i>Right:</i> translated navigator volumes align the FOV center (star) with the estimated brain segmentation mask (green outline). The dark bands in the navigator volumes represent spin history artifacts from the diagnostic slices.
</div>