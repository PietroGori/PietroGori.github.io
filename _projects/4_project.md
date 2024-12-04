---
layout: page
title: Contrastive Analysis
description: 
img: assets/img/CA-hetero.png
importance: 2
category: Current
related_publications: true
permalink: /projects/CA
---

<div class="text-center">
    {% include figure.liquid path="assets/img/Team-CA.png" width="90%" max-width="100%" %}
</div>

**Context** Learning disentangled generative factors in an unsupervised way has gathered much attention lately since it is of interest in many domains, such as medical imaging. Most approaches look for factors that capture distinct, noticeable and semantically meaningful variations in one dataset (e.g., presence of hat or glasses in CelebA). Authors usually propose well adapted regularizations, which may promote, for instance, ”uncorrelatedness” (e.g., FactorVAE) or ”informativeness” (e.g., InfoGAN).   
In this project, we focus on a related but different problem, that has been named Contrastive Analysis (CA). We wish to discover in an unsupervised way what is added or modified on a target dataset compared to a control (or background) dataset, as well as what is common between the two domains. For example, in medical imaging, one would like to discover the salient variations characterizing a pathology that are only present in a population of patients (tumors or glasses in the figure below) and not in a population of healthy controls. Both the target (patients) and the background (healthy) datasets are supposed to share uninteresting (healthy) variations. 


<div class="text-center">
    {% include figure.liquid path="assets/img/CA.png" width="80%" max-width="100%" %}
</div>
<div class="caption">
    Two examples of datasets for Contrastive Analysis. <strong>First dataset</strong>: Brain MRI images with/without tumors. Top: MRI images of healthy brains (control dataset). Bottom: MRI images of brains with tumor (target dataset). <strong>Second dataset</strong>: CelebA dataset. Top: control dataset with regular faces (no smile, no glasses). Bottom: target dataset that contains smiling faces with glasses. 
</div>

**Goal** The goal is to identify and separate the generative factors common to both populations from the ones distinctive (i.e., specific) only of the target dataset


**Contributions**
Lately, we have proposed three new CA methods based on: 
1. Variational AutoEncoders (VAE), {% cite louiset_sepvae_2024 %}
2. Generative Adversarial Network (GAN) {% cite carton_double_2024 %}, and
3. Contrastive Learning {% cite louiset_separating_2024 %}


**Results**
Let $$X={x_i}$$ and $$Y={y_j}$$ be the background (or control) and target datasets of images repsectively. Both $${x_i}$$ and $${y_j}$$ are assumed to be i.i.d. from two different and unknown distributions ($$P(x)$$ and $$P(y)$$) that depend on a pair of latent variables $$(c, s)$$. Here, $$s$$ is assumed to capture the salient generative factors proper only to $$Y$$ whereas $$c$$ should describe the common generative factors between $$X$$ and $$Y$$.   
At inference, each one of the proposed CA method can estimate the common $$c_t$$ and salient $$s_t$$ factors specific to a test image $$t$$. We can thus test the performance of the algorithm by evalating its reconstruction quality and by swapping the salient factors between a background and target image, as shown in the figure below (each row presents a different result). 


<div class="text-center">
    {% include figure.liquid path="assets/img/DoubleInfoGAN.png" width="80%" max-width="100%" %}
</div>
<div class="caption">
 Image reconstruction and swap with the CelebA with accessories dataset.
</div>
