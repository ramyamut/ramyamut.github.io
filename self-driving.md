---
layout: page
title: "Self-driving Fetal Brain MRI"
permalink: /self-driving-mri/
---
<h4 style="text-align: center;">Prospective motion correction via adaptive imaging plane prescription</h4>
<div class="container">
  <div id="authors">
      <div class="row mt-3">
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://ramyamut.github.io" target="_blank">Ramya<br> Muthukrishnan</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://lcn.martinos.org/people/pwighton/" target="_blank">Paul<br> Wighton</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://www.nmr.mgh.harvard.edu/user/3986021" target="_blank">Robert<br> Frost</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://www.nmr.mgh.harvard.edu/user/5804" target="_blank">Andre J.<br> van der Kouwe</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://labs.childrenshospital.org/mortonlab/people/aryn-lee" target="_blank">Aryn<br> Lee</a></div>
      </div>
      <div class="row mt-3">
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://imes.mit.edu/people/adalsteinsson-elfar" target="_blank">Elfar<br> Adalsteinsson</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://research.childrenshospital.org/researchers/patricia-ellen-grant" target="_blank">P. Ellen<br> Grant</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://people.csail.mit.edu/polina/" target="_blank">Polina<br> Golland</a></div>
          <div class="col-sm mt-3 mt-md-0 text-center"><a href="https://connects.catalyst.harvard.edu/Profiles/display/Person/105811" target="_blank">Borjan<br> Gagoski</a></div>
      </div>
      <div class="row mt-3">
          <div class="col-sm mt-3 mt-md-0 text-center">MIT <br> CSAIL</div>
          <div class="col-sm mt-3 mt-md-0 text-center">Martinos Center<br> for Biomedical Imaging</div>
          <div class="col-sm mt-3 mt-md-0 text-center">Boston Children's<br> Hospital</div>
          <div class="col-sm mt-3 mt-md-0 text-center">Harvard <br> Medical School</div>
      </div>
  </div>

</div>
<br>
<h2 style="text-align: center;">Abstract</h2>
<p style="text-align: center;">To diagnose fetal neurodevelopmental abnormalities, radiologists rely on stacks of high-resolution T2-weighted 2D anatomical (HASTE) slices acquired along the axial, sagittal, and coronal planes. Head motion between consecutive slices hinders radiological interpretability by producing double-oblique slices and introducing unintended gaps in spatial brain coverage. In current clinical practice, this necessitates re-acquisition of the whole stack, leading to long scan times and limited diagnostic utility if no high quality stack can be acquired. Before every HASTE readout, we insert a fast EPI volumetric navigator (EPI-vNav) that is used to estimate the current fetal head pose, center the next EPI-vNav on the head, and translate/rotate the HASTE imaging plane to account for the head motion. We implemented our automated acquisition system on a 3T fetal MRI scanner. In preliminary <i>in utero</i> experiments, the EPI-vNavs and HASTE slices acquired by our method accurately follow the translational and full rigid movements of the fetal head in real time. Furthermore, our HASTE stacks demonstrate mitigated motion effects compared to those acquired without any motion correction. Our work promises to improve radiological assessments, reduce scan time, and alleviate pregnant patients’ discomfort.</p>

<h2 style="text-align: center;">Method</h2>
<div class="row mt-3">
        {% include figure.html path="/assets/img/interleaved.png" class="img-fluid rounded z-depth-1"%}
</div>
<div class="caption">
    <b>Interleaved acquisition of 3D EPI-vNavs and 2D (axial) HASTE slices.</b> To correct for fetal head motion, our proposed system aims to automatically adjust the imaging plane \(P_{k+1}\) to account for the current head pose \(T_k\), which is estimated from the previous EPI-vNav scan $f_k$. Pose estimation from EPI-vNavs is a challenging task due to low signal-to-noise ratio and low resolution. Furthermore, EPI-vNavs include spin-history artifacts (yellow arrows) from the preceding HASTE readout due to the short time interval (1.5 s) between the two acquisitions. 

</div>
<div class="row mt-3">
        {% include figure.html path="/assets/img/feedback.png" class="img-fluid rounded z-depth-1"%}
</div>
<div class="caption">
    <b><i>In utero</i> implementation.</b> Our real-time system employs an interleaved sequence running on a 3T Siemens scanner, connected to a server hosted on a GPU-enabled laptop. At the start of the sequence, we define the target imaging planes \(P_1,...,P_k\) of all HASTE slices in the stack relative to a canonical anatomical coordinate system. At time step \(k\), the server receives the most recent EPI-vNav \(f_k\), from which we estimate the rigid transform \(T_k=t_k\circ R_k\) from the anatomical to scanner coordinate systems. We then prescribe the next HASTE imaging plane to be \(\tilde{P}_k=T_kP_k\) and shift the next EPI-vNav field-of-view (FOV) by \(t_k\).

</div>

<h2 style="text-align: center;"><i>In utero</i> demos</h2>

<h4 style="text-align: center;">EPI-vNavs</h4>

<div class="row mt-3">
        {% include figure.html path="/assets/gif/vnav_shift.gif" class="img-fluid rounded z-depth-1"%}
</div>
<div class="caption">
    Example of dynamically translated EPI-vNavs "chasing" the head in a 31 week old fetus.

</div>

<h4 style="text-align: center;">HASTE slices</h4>

<div class="row mt-3">
        <div class="col-sm mt-3 mt-md-0">{% include video.html path="/assets/video/axial.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}</div>
        <div class="col-sm mt-3 mt-md-0">{% include video.html path="/assets/video/sagittal.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}</div>
        <div class="col-sm mt-3 mt-md-0">{% include video.html path="/assets/video/coronal.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}</div>
</div>
<div class="caption">
    Our automatically prescribed HASTE slices align with the target anatomical orientation (<i>left to right: axial, sagittal, coronal</i>).

</div>

<h4 style="text-align: center;">HASTE stacks</h4>

<div class="row mt-3">
        <div class="col-sm mt-3 mt-md-0 text-center">{% include figure.html path="/assets/gif/axial_comparison.gif" class="img-fluid rounded z-depth-1"%}</div>
        <div class="col-sm mt-3 mt-md-0 text-center">{% include figure.html path="/assets/gif/sagittal_comparison.gif" class="img-fluid rounded z-depth-1"%}</div>
        <div class="col-sm mt-3 mt-md-0 text-center">{% include figure.html path="/assets/gif/coronal_comparison.gif" class="img-fluid rounded z-depth-1"%}</div>
</div>
<div class="caption">
    We compare HASTE stacks acquired by our method to those acquired without motion correction in a subject (GA=30w2d) with significant fetal motion. The examples demonstrate that our method promises to mitigate motion effects by improving the spatial alignment of slices within the stack.

</div>