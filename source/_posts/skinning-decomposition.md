---
title: Skinning Decomposition
id: 355
categories:
  - CG
date: 2016-08-28 22:33:28
tags:
---

**Skining Decomposition**这一术语由Kavan等人在2010年发表的文章Fast and efficient skinning of animated meshes中提出。它是从一个样本姿势集合中指**提取骨骼变换(bone transformations)或控制点** 和 **骨骼顶点的影响力(bone-vertex influences)或权重** 的问题。

Kavan et al. [2010] officially coined the term skinning decomposition, and it refers to the problem of extracting both the bone transformations (or the control points) and the bone-vertex influences (or the weights) from a set of example poses. 
In their model, the vertices of example poses, denoted as a matrix A, are decomposed to A = T X, where T represents the transformation and X represents the combination of the weight matrix and the rest pose.

> Reference：K AVAN , L., S LOAN , P.-P., AND O’S ULLIVAN , C. 2010\. Fast and efficient skinning of animated meshes. Comput. Graph. Forum 29, 2, 327–336.
>   [Smooth Skinning Decomposition with Rigid Bones](http://graphics.cs.uh.edu/ble/papers/2012sa-ssdr/)