---
permalink: /
title: "Welcome!"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

My PhD dissertation is available on [mediatum.ub.tum.de](https://mediatum.ub.tum.de/doc/1720613/1720613.pdf), before you read it please note:

- In the related work I listed traditional grid-based RBPFs (e.g. {% cite murphy1999bayesian grisetti2005rbpfslam %}) next to landmark-based methods which was not the right place, particularly because the following paragraphs were a comment on preprocessed observations.
Also, I should have pointed out that classical *grid-based* RBPFs already had an integration of a dense map in an SSM and raw range observations, even if lower-dimensional than modern dense RGB-D SLAM.
The method in {% cite fairfield2007realtime %} also used a 3D ray-tracing sonar emission, with a small number of rays for speed.
Notions from this line of work can be traced all the way back to {% cite moravec1985occupancymaps %} and also appear in the dissertation (e.g. grids, occupancy, stepping along rays, closed-form map updates alike those in PRISM, etc.).
And of course RBPFs provide complete posterior distributions, just like the other classical-era SLAMs in the related work (e.g. EKFs), which the dissertation strives to do as well, but with different inference algorithms (e.g. PRISM has a similar Bayes-filter recursion, but works differently).
Combined, these analogies span the spectrum of thesis aspects (see sec. 3.3), the difference in the thesis is in the underlying model assumptions & inference methods, designed to fit both RGB-D sensors and free 6-DoF movement.
Please note the similarity of such methods and interpret the contributions in that context.

- To add to the above: if I am not mistaken {% cite haehnel2003efficient %} was the first grid-based RBPF to be applied to real-world 2D data; you can also see {% cite hoehner2018particle %} for a modern attempt to mix a particle filter (not Rao-Blackwellized) with a 3D TSDF map, using a non-ray-tracing implicit emission.

- In general, classical-era EKF & RBPF SLAMs from the 2000s already had a unity of probalistic SSM & spatial assumptions (I hope this is clear from the related work on robotics, as I noted there they are POMDP-compliant). The aim of the thesis is to provide a similar unified perspective for modern RGB-D dense SLAM.

- On p. 68, line 3 I discuss a dynamics term in eq. 5.19 as new.
When I wrote this line I was not aware of some overlap with prior works (e.g. {% cite wagner2014humanoid klingensmith2016armslam scona2017proprioception laidlow2017rgbdinertial houseago2019kofusion %}) which fuse dense visual frame-to-model tracking with external pose estimates (e.g. from wheel encoders, robot joint measurements or IMU data).
This is the same idea as eq. 5.19, I believe with some minor technical differences (e.g. map and rendering details) and possibly a slight difference in perspective (controlled transition vs. motion prior from measurements).

- On p. 74 I mention that there is some novelty in basing infogain exploration on VSSM-LM's rendering and PRISM's map filter (see Ziqing's work on exploration).
Here I want to point out {% cite saulnier2020information %} which uses 2D TSDF maps and is overall quite similar, particularly in its map updates (modulo some technicalities: 2D vs. 3D, rendering, map update & uncertainty truncation, candidate generation).
Note that such exploration is very traditional, if you are interested some early works are {% cite stachniss2003exploring triebel2004first stachniss2009exploration %} and you can find a few more modern 3D ones in the related work.

- Apropos: classical grid-based RBPFs also harmonize with such exploration (see {% cite stachniss2009exploration %}).

After the defense, I added {% cite wagner2014humanoid klingensmith2016armslam scona2017proprioception %} last-minute as part of a more general discussion in the related work section, but I did not point out the above.
Please take care if you cite.

## References
{% bibliography --cited_in_order %}
