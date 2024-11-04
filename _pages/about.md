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
Also, I should have pointed out that classical grid-based RBPFs already had an integration of a dense map in an SSM and raw range observations, even if lower-dimensional than modern dense RGB-D SLAM.

    The RBPF method in {% cite fairfield2007realtime %} also used a 3D ray-tracing sonar emission, with a small number of rays for speed.
    Its setup is different (underwater coarse octree maps, tunnel movement, water-pressure altitude sensors, 54 sonar beams shaped as pencils, etc.) from the RGB-D one I focused on, but it is similar in trying to scale grid-based probabilistic SLAM to 3D.
    I wish I had included it for that aspect, IIRC I found it after submitting the thesis and meant to add it for a while, but around the defense I focused on a few other SSM-like RGB-D methods I wanted to cite and decided not to add it in the end, and I think that was a mistake.

    More generally, notions from the grid-based RBPF line of work can be traced all the way back to {% cite moravec1985occupancymaps %} and also appear in the dissertation (e.g. grids, occupancy, stepping along rays and raytracing, closed-form map updates alike those in PRISM, etc.).
    And of course RBPFs provide complete posterior distributions, just like the other classical-era SLAMs in the related work (e.g. EKFs), which the dissertation strives to do as well, but with different inference algorithms (e.g. PRISM has a similar Bayes-filter recursion, but works differently).
    Combined, these analogies span the spectrum of thesis aspects (see sec. 3.3), the difference in the thesis is in the underlying model assumptions & inference methods, designed to fit both RGB-D sensors and free 6-DoF movement.
    Please note the similarity of such methods and interpret the contributions in that context.

- To add to the above: if I am not mistaken {% cite haehnel2003efficient %} was the first grid-based RBPF to be applied to real-world 2D data.
You can also see {% cite hoehner2018particle %} for a modern attempt to mix a particle filter (not Rao-Blackwellized) with a 3D TSDF map and a non-ray-tracing implicit emission -- this one is for RGB-D data like my work, it is another late find I decided not to add while I could and I should have.
It is related in general and also to PRISM, with a different inference algorithm and a glimpse at PF robustness.
From what I understand it seems it used a zero-mean Gaussian motion model without controls -- in theory replacing that with a control-driven transition should be straightforward, which could then be used for predictive rollouts and then one could see the whole as an alternative probabilistic dense RGB-D SSM-and-filter combo for model-based control.
This is how it connects to my perspective.

- In summary, classical-era EKF & RBPF SLAMs from the 2000s already had a unity of probabilistic SSM & spatial assumptions (I hope this is clear from the related work on robotics, as I noted there they are POMDP-compliant).
And as you can see from the above, grid RBPFs already had an SSM with a dense map, and at least one paper (e.g. {% cite fairfield2007realtime %}) was about scaling that to 3D.
The aim of my thesis was to present a similar unified perspective for modern RGB-D dense SLAM and highlight the link to control, hopefully adding to the perspectives that exist already (see my related work, the RBPFs and {% cite hoehner2018particle %} above, etc.).

    I think the last point should be clear if you read end-to-end, and if you see isolated mentions of "dense SLAM" and it is unclear what I meant from the context, note that the go-to prototypical example I had in mind was generating images with thousands of pixels (e.g. as in contemporary direct RGB-D or NERF methods).
    I do not recall how well I separated modern high-resolution (colored) 3D lidars in my mind in these cases, but in hindsight I think it is cleaner to treat them as separate, because the thesis has solely RGB-D results and I am also more aware of RGB(-D) than lidar trends.

- On p. 68, line 3 I discuss a dynamics term in eq. 5.19 as new.
When I wrote this line I was not aware of some overlap with prior works (e.g. {% cite wagner2014humanoid klingensmith2016armslam scona2017proprioception laidlow2017rgbdinertial houseago2019kofusion %}) which fuse dense visual frame-to-model tracking with external pose estimates (e.g. from wheel encoders, robot joint measurements or IMU data).
This is the same idea as eq. 5.19, I believe with some minor technical differences (e.g. map and rendering details) and possibly a slight difference in perspective (controlled transition vs. motion prior from measurements).

- On p. 74 I mention that there is some novelty in basing infogain exploration on VSSM-LM's rendering and PRISM's map filter (see Ziqing's work on exploration).
Here I want to point out {% cite saulnier2020information %} which uses 2D TSDF maps and is overall quite similar, particularly in its map updates (modulo some technicalities: 2D vs. 3D, rendering, map update & uncertainty truncation, candidate generation).
Note that such exploration is very traditional, if you are interested some early works are {% cite stachniss2003exploring triebel2004first stachniss2009exploration %} and you can find a few more modern 3D ones in the related work.

- Apropos: classical grid-based RBPFs also harmonize with such exploration (see {% cite stachniss2009exploration %}).

After the defense, I added {% cite wagner2014humanoid klingensmith2016armslam scona2017proprioception %} last-minute as part of a more general discussion in the related work section, but I did not point out the above.
Please take care if you cite.

On a different note: appendix C extends the background in Part I, the sources on p. 9 apply here too.
On the whole, the background theory should be covered by those textbooks and the inline references, though I remember consulting a few more sources on these topics I did not cite and I spotted one I did not cite well, so I want to highlight them here.
Modulo only notation, the importance sampling derivation in C.29-C.31 and the reparam. trick formulation in C.26 are the same as in {% cite soelch2021uncovering %} by Maximilian Sölch and the POMDP transition definition in equation 1.33 is the same as in {% cite kayalibay2024control %} by Baris Kayalibay, I remember replicating them in my work (by the way, $$1/\mathcal{Z}$$ in C.30 should be $$\mathcal{Z}$$).
I believe {% cite soelch2021uncovering %} also influenced my probabilistic background section overall, as I read it right before writing for inspiration.
Appendix C.2 is a brief recap of Gauss-Newton and MAP -- here I cited *"Factor Graphs for Robot Perception"* by Dellaert and Kaess at the end of the section when I mentioned sparsity, but I fear what did not come across is that the book is a holistic reference, note that you can get most of what I had to say in C.2 from it.
I also remember looking up the generalized Gauss-Newton equations in C.2 in [this lecture](https://www.youtube.com/watch?v=SuqEx_wPPwI) by Fred Roosta, that would be equations C.15-C.18.
For the theory on cameras, rotations and Lie groups I used [these lectures](https://www.youtube.com/playlist?list=PLTBdjV_4f-EJn6udZ34tht9EVIW7lbeo4) by Daniel Cremers (e.g. the definitions 2.16-2.18; also, almost all equations in C.8,C.9 and the Lie-group parts in 2.1 are both from there and the micro-Lie-theory tutorial I referenced).

## References
{% bibliography --cited_in_order %}
