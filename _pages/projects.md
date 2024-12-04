---
layout: page
title: Projects
permalink: /projects/
description: 
nav: true
nav_order: 3
display_categories: [Current,Past]
horizontal: true
---

I focus my research efforts on developing AI methods that answer specific needs and constraints of the medical imaging data (e.g., low-data regime, data biases, lack of labeling data) leveraging multiple modalities, clinical knowledge and (healthy) unlabeled data. From a methodological perspective, my research follows three main axes:
1. **Modeling** medical knowledge and anatomy and integrating it into machine learning models.
2. **Learning** compact, relevant and explanatory representations of anatomical imaging data.
3. **Transferring** anatomical representations between domains (i.e., different modalities, data-sets,
populations) to increase downstream performance (e.g., segmentation, classification, regres-
sion) or to discover new pathological biomarkers.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/researchDir.png" %}
    </div>
</div>


Here, you can find a list of (some of) my current and past projects   


<!-- pages/projects.md -->
<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.projects | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>
