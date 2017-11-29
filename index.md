---
layout: page
title: Introduction
mathjax: true
comments: false
exclude_from_nav: true
---

The past few decades have witnessed many successful 3D reconstruction technique being developed. However, there are mainly two challenges that prevent the wide adoption of these techniques. First, most vision techniques, 3D reconstruction techniques included, only work for a specific category of objects or under a specific problem condition. Second, the working conditions of each class of algorithms are largely known, or only known empirically, without a well defined problem condition.

## Goal
The goal of this research topic is to address the two aforementioned issues: construct a 3D reconstruction interface that targets objects with large ranges of geometric and material properites, and secondly, discover the well defined working conditions of each algorithm so that an appropriate algorithm can be selected as the reconstruction technique.

## Contribution
The main contribution of this paper is the development and application of an interface for a subset of 3D reconstruction problem, which hides algorithmic details and allows users to describe conditions surrounding the problem. This described conditions, which consists of varied visual and geometric properties, can be interpreted so that an appropriate algorithm is chosen to reconstruct a successful result. This endeavor is non-trivial for two reasons:

1. currently, most approaches can only achieve satisfactory results on a limited set of categories of objects;
2. a solid understanding of reconstruction algorithm details is a prerequisite to fully take advantage of the existing techniques, which is difficult for application developers to obtain.

To some extent, our interface attempts to expand the problem space by incorporating multiple algorithms. Though it can cover a wider range of problem space than a single algorithm, it is still confined within the space covered by currently existing techniques. Thus, our evaluation is carried out within the problem space covered by the selected algorithms.

## Existing benchmarks
There are two limitations to current existing 3D datasets or benchmarks
1. they target one specific class of algorithms;
2. they use objects with fixed geometric or material properties.

We generated both real-world and synthetic datasets, they are used to evaluate the performance of the interpreter. More specifically:

* Can the proof of concept interpreter return one of the best-suited algorithms that achieves a successful reconstruction given the correct description?
* Will an inaccurate description give a poorer reconstruction result than an accurate description?

