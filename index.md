---
layout: page
title: Introduction
mathjax: true
comments: false
exclude_from_nav: true
---

## Intro
The past few decades have witnessed many successful 3D reconstruction technique being developed. However, there are mainly two challenges that prevent the wide adoption of these techniques. First, most vision techniques, 3D reconstruction techniques included, only work for a specific category of objects or under a specific problem condition. Second, the working conditions of each class of algorithms are largely known, or only known empirically, without a well defined problem condition.

## Goal
The goal of my research is to address the two aforementioned issues: construct a 3D reconstruction framework that targets objects with large ranges of geometric and material properites, and secondly, discover the well defined working conditions of each algorithm so that an appropriate algorithm can be selected as the reconstruction technique.

## Existing benchmarks
There are two limitations to current existing 3D datasets or benchmarks
1. they target one specific class of algorithms;
2. they use objects with fixed geometric or material properties.

We generated both real-world and synthetic datasets. The synthetic dataset is used to evaluate the performance of each algorithm under a variety of problem conditions. The real-world dataset is used to validate the robustness of the framework. More specifically:

* a real-world dataset with 11 objects captured for Multi-view Stereo, Photometric Stereo, and Structured Light techniques.
* multiple blender projects used to generate synthetic datasets with varied material and geometric properties

## Setups
