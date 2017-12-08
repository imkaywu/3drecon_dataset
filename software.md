---
layout: page
title: Software
permalink: /software/
---

## Table of content
* [Overview](#overview)
* [Dependencies](#dependency)
* [Structure of source code](#structure)
* [Demos](#demo)
* [Sub-routines](#subroutine)
* [Calibration results](#calibration)
* [Execution & evaluation pipeline](#run_eval)

## Overview <a name="overview"></a>
This toolkit contains Matlab and C++ code for running a variety of 3D reconstruction and evaluation pipelines. The source code is available [here](https://github.com/imkaywu/3DReconKit).

## Dependencies <a name="dependency"></a>
* Matlab
* [eigen3-nnls](https://github.com/hmatuschek/eigen3-nnls): Non-negative least squares algorithm for Eigen

## Structure of source code <a name="structure"></a>
The structure of the toolbox is as follows:

```
.
├── algo
|   └── MVS
|   	└── PMVS
|           └── bin_x64
|   └── PS
|   	├── EPS
|       └── LLS-PS
|   ├── SL
|   └── VH
├── eval
|   ├── include
|   ├── io
|   └── real_world
|       └── run.m
|   └── synth
|       └── eval_prop
|           ├── run.m
|           └── evaluate.m
|       └── eval_algo
|           ├── run.m
|           └── evaluate.m
|       └── eval_interp
|           ├── run.m
|           └── evaluate.m
```

* The `algo` directory contains various 3D reconstruction algorithms, see the table below for details:

	| Algo Class |  Algo  | Summary  | Source code |
	| :--------- | :----- | :------- | :---------- |
	| MVS        | PMVS   | Patch based Multi-View Stereo | [PMVS](https://www.di.ens.fr/pmvs/) |
	| PS         | EPS    | Example-base Photometric Stereo | [PSKit](https://github.com/imkaywu/PSKit) |
	| PS         | LLS-PS | Least squares Photometric Stereo | [PSKit](https://github.com/imkaywu/PSKit) |
	| SL         | GSL    | Gray-coded Structured Light | [SLKit](https://github.com/imkaywu/SLKit) |
	| VH         | VH     | Volumetric Visual Hull | |
	{:.mbtablestyle}

* The `eval` directory contains the evaluation pipelines for different stages discussed in [Results](/3drecon_dataset/result/) page

The image data and calibration data structure is as follows: 
```
├── calib
|   └── result
|       ├── real
|       └── synth
|   ├── include
|   └── src
├── data
|   └── real
|       └── cup
|           ├── mvs
|           ├── ps
|           ├── sl
|           └── vh
|   └── synth
|       ├── eval_prop
|       ├── eval_algo
|       └── eval_interp
└── README.md
```

## Demos <a name="demo"></a>
1. Run 3D reconstruction algorithms on synthtic dataset to discover the effective properties, run
```
eval/synth/eval_prop/run.m
eval/synth/eval_prop/evaluate.m
```
2. Run 3D reconstruction algorithms on synthtic dataset to discover the mapping between problem conditions and algorithms, run
```
eval/synth/eval_algo/run.m
eval/synth/eval_algo/evaluate.m
```
3. Run 3D reconstruction algorithms on synthtic dataset to evaluate the performance of interpreter, run
```
eval/synth/eval_interp/run.m
```
4. Run 3D reconstruction algorithms on real-world datasets to evaluate the performance of interpreter, run
```
eval/real_world/run.m
```

## Sub-routines <a name="subroutine"></a>


## Calibration results <a name="calibration"></a>

The format of calibration result can be found in the Documentation page.


## Execution & evaluation pipeline <a name="run_eval"></a>

## Data generation
The blender projects and python scripts are [here](https://github.com/imkaywu/blender_scripts). The command is
```
blender proj/mvs.blend -b -P scripts/pairwise/mvs.py
```
