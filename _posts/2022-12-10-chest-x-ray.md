---
layout: post
title:  "Chest X-ray Classification"
date:   2022-12-10
title_include: true
categories: project
image_url: ""
---

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  <!-- tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}, -->
  jax: ["input/TeX","output/HTML-CSS"],
  displayAlign: "left",
  "HTML-CSS": { scale: 110}
});
</script>

<style>body {text-align: justify}</style>

## Abstract
Chest X-rays scans are among the most accessible ways to diagnose lung diseases. This study tries to compare the detection of lung diseases using these scans from three different datasets using deep neural networks. Three different backbone architectures,
ResNet34, MobileNet V3 Large and EfficientNet B1 were used along with a set of models trained using transfer learning. It was observed that MobileNet takes the least amount of time to train while ResNet converges the fastest. Also, EfficientNet performs the best most of the times on Chest X-ray scans. An F1 score of 0.8 for the pneumonia dataset was obtained, 0.98 for the COVID-19 dataset and 0.46 for the multilabel chest X-ray 8 dataset. Finally, models are visualized using t-SNE and gradCAM to understand the features learned by the models and correlate them with the actual effect of the diseases on the lungs.

<img style="float: right;" src="/assets/img/chest-x-ray/lung-xray.png" width="300"> 