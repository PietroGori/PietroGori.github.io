---
layout: page
title: Self-supervised Learning
description: 
img: assets/img/SSL.png
importance: 1
category: Current
related_publications: true
permalink: /projects/SSL
---


<div class="text-center">
    {% include figure.liquid path="assets/img/Team-CL.png" width="80%" max-width="100%" %}
</div>

**Context**  Many specific tasks in Computer Vision, such as object detection (e.g., YOLOv71), image classification (e.g., ResNet-50), or semantic segmentation (e.g., UNet, Swin Transformer) have reached astonishing results in the last years. This has been possible mainly because large (N > $$10^6$$), labeled data-sets were easily accessible and freely available. However, many applications in medical imaging lack such large datasets and annotation might be very time-consuming and difficult even for experienced medical doctors. For instance, predicting mental or neurodevelopmental disorders from neuroanatomical imaging data (e.g., T1-w MRI) has not yet achieved the expected results (i.e., AUC ≥ 90 {% cite dufumier_exploring_2024 %}). Furthermore, recent studies yielded contradictory results when comparing Deep Learning with Standard Machine Learning (SML) on top of classical feature extraction {% cite dufumier_exploring_2024 %}.  

 
**Challenges** The first challenge concerns the small number of pathological samples. In supervised learning, when dealing with a small labeled dataset, the most used and well-known solution is supervised Transfer Learning from ImageNet (or other large vision datasets). However, it has been recently shown that this strategy is useful, namely features are re-used, only when there is a high visual similarity
between the pre-train and target domain (e.g., low Fréchet inception distance (FID)). This is not the case when comparing natural and medical images. Furthermore, many medical images, and in particular brain MRI scans, are 3D volumes, differently from the 2D images of ImageNet. This
entails a great domain gap between the large labeled datasets used in computer vision and medical images. Another approach comprises self-supervised learning (SSL) methods which leverage an annotation-free pretext task to provide a surrogate supervision signal for feature learning. Nonetheless, these methods still need large (unannotated) datasets, which should comprise, to reduce the domain gap, data similar to the ones in the (labeled) target dataset, namely pathological patients. However, the large majority of images currently stored in hospitals and clinical laboratories belong to healthy subjects. Indeed, the largest datasets currently available (e.g., UKBioBank and OpenBHB) mostly contain data of healthy subjects. Furthermore, these datasets usually comprise one or multiple imaging modalities, as well as clinical data, such as age, gender and weight. The research challenge thus becomes how to leverage large datasets of healthy subjects and combine the heterogeneous sources of information (i.e., clinical and imaging data) to improve the diagnostic and understanding of patients.  

A second challenge concerns the data biases. In our work, we define data biases as the visual patterns that correlate with the target task and/or are easy to learn, but are not relevant for the target task. For instance, the site effect in MRI images refers to systematic variations or discrepancies in feature distributions across different imaging sites, that arise from differences in equipment, protocols, or
settings , and are not related to a disease (i.e., target task). When working with MRI samples in a binary classification problem (healthy Vs patients), these spurious differences can be visually more accentuated, and thus easy to learn, than the relevant differences between the two
classes. This can result in a biased model, whose predictions majorly rely on the bias attributes and not on the true, generalizable, and discriminative features.   

<div class="text-center">
    {% include figure.liquid path="assets/img/toy_example_transfer_learning_v2.jpg" width="80%" max-width="100%" %}
</div>
<div class="caption">
    In this project, we propose a new paradigm where, instead than learning a network from scratch using a small pathological dataset, we first pre-train it on a large dataset of healthy subjects, thus learning a representation space describing the healthy population. We leverage our new weakly-supervised contrastive loss, combining clinical, biological and imaging data. Then, we transfer it and fine-tune it on the small pathological dataset. 
</div>


**Contributions** In this project, we have proposed a new geometric approach for contrastive learning {% cite barbano_unbiased_2023 %} that can be used in different settings:  
1. unsupervised (i.e., no labels) {% cite sarfati_learning_2023 %}, {% cite ruppli_optimizing_2022 %}, {% cite barbano_unbiased_2023 %},  
2. supervised (i.e., class labels) {% cite barbano_unbiased_2023 %}, and 
3. weakly-supervised (i.e., weak attributes or regression) {% cite dufumier_contrastive_2021 %} {% cite barbano_contrastive_2023 %}  {% cite dufumier_integrating_2023 %},  {% cite ruppli_decoupled_2023 %},  {% cite dufumier_conditional_2021 %}.    

It is well adapted to integrate prior information, such as weak attributes or representations learned from generative models, and can thus be used to learn a representation of the healthy population by leveraging both clinical and imaging data.  

<div class="text-center">
    {% include figure.liquid path="assets/img/geometric-CL.png" width="80%" max-width="100%" %}
</div>
<div class="caption">
In a) we show a visual explanation of the proposed geometric approach for Contrastive Learning. We aim at increasing the minimal margin ϵ, between the distance d+ of a positive sample x+ (+ symbol inside and yellow color) from an anchor x and the distance d− of the closest negative sample x− (− symbol inside and blue color). By increasing the margin, we can achieve a better separation between positive and negative samples. In b) and c), we show two different scenarios without margin (b) and with margin (c). Filling colors of datapoints represent different biases. In both b) and c) the contrastive conditions are fulfilled and thus the loss is minimized (i.e., positives are closer to the anchor than the negatives). However, we observe that, without imposing a margin, biased clusters might appear containing both
positive and negative samples (b). This issue can be mitigated by increasing the ϵ margin (c) and using the proposed regularization loss Fair KL {% cite barbano_unbiased_2023 %}.
</div>

<div class="text-center">
    {% include figure.liquid path="assets/img/pic-MICCAI-2021.png" width="70%" max-width="100%" %}
</div>
<div class="caption">
Using standard Contrastive Learning losses (e.g., SimCLR), samples are uniformly scattered in the representation space, without considering their clinical variables (metadata, y), such as age. By employing our weakly-supervised losses, two subjects with similar metadata are mapped closer in the representation space compared to two subjects with different metadata.
</div>

Based on the proposed geometric approach, we show why recent contrastive losses (InfoNCE, SupCon, etc.) can fail when dealing with biased data and derive a new debiasing regularization loss, that work well even with extremely biased data. {% cite barbano_unbiased_2023 %}. You can find a visual explanation below using the color-MNIST dataset.

<div class="text-center">
    {% include figure.liquid path="assets/img/bias.png" width="80%" max-width="100%" %}
</div>
<div class="caption">
A positive bias-aligned sample x+,b is semantically similar (positive) to the anchor (same digit) but it has also the same bias b (yellow color). A positive bias-conflicting sample shares the same digit but it has a different bias b′(different color). Here, the color is defined as a data bias since it’s a visual feature that is correlated with the semantic content related to the target task (digit recognition), but it doesn’t characterize it.
</div>


<div class="text-center">
    {% include figure.liquid path="assets/img/bias-distance.png" width="100%" max-width="100%" %}
</div>
<div class="caption">
In {% cite barbano_unbiased_2023 %}, we propose the FairKL regularization term for debiasing. Ideally, we would like that the distances between all positive (resp. negative) samples and the anchor, whatever their bias, are equal. However, this condition is very strict, as it would enforce uniform distance among all positive (resp. negative) samples. We have proposed a more relaxed condition where we force the distributions of distances of positives with different biases to be similar (same for negative). Assuming that the distance distributions follow a normal distribution, we propose to minimize the Kullback-Leibler divergence of the two distributions obtaining a closed form solution that we called FairKL.
</div>












