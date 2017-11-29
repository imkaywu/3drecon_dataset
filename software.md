---
layout: page
title: Software
permalink: /software/
---

## Table of content
* [Structure of source code](#structure)
* [Algorithms](#algorithms)
* [Calibration results](#calibration)
* [Datasets](#datasets)
* [Execution & evaluation pipeline](#run_eval)

In this section, we will give detailed introduction of our software that is used to run and evaluate all the implemented algorithms. The source code is available [here](https://github.com/imkaywu/3DReconKit).

## Structure of source code <a name="structure"></a>
The structure of the toolbox is as follows

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
└── README.md
```

## Algorithms <a name="algorithms"></a>
We have implemented four classes of algorithms, they are summarized in the table below

| Algo Class |  Algo  | Summary  | Source code |
| :--------- | :----- | :------- | :---------- |
| MVS        | PMVS   | Patch based Multi-View Stereo | [PMVS](https://www.di.ens.fr/pmvs/) |
| PS         | EPS    | Example-base Photometric Stereo | [PSKit](https://github.com/imkaywu/PSKit) |
| PS         | LLS-PS | Least squares Photometric Stereo | [PSKit](https://github.com/imkaywu/PSKit) |
| SL         | GSL    | Gray-coded Structured Light | [SLKit](https://github.com/imkaywu/SLKit) |
| VH         | VH     | Volumetric Visual Hull | |

## Calibration results <a name="calibration"></a>

The format of calibration result can be found in the Documentation page.



## Datasets <a name="datasets"></a>

## Execution & evaluation pipeline <a name="run_eval"></a>

## Data generation
The blender projects and python scripts are [here](https://github.com/imkaywu/blender_scripts). The command is
```
blender proj/mvs.blend -b -P scripts/pairwise/mvs.py
```

```
.
├── proj
|   ├── mvs.blend
|   ├── ps.blend
|   ├── sl.blend
|   └── [other blender projects]
├── scripts
|   └── pairwise
|       ├── mvs.py
|       ├── ps.py
|       ├── sl.py
|       └── vh.py
|   └── train
|       ├── mvs.py
|       ├── ps.py
|       ├── ps_baseline.py
|       ├── sl.py
|       └── sc.py
|   └── test
|       ├── mvs.py
|       ├── ps.py
|       ├── ps_baseline.py
|       ├── sl.py
|       └── sc.py
|   └── util
|       ├── helper.py
|       ├── mask.py
|       ├── ps_mask.py
|       ├── ps_ref.py
|       ├── sl_calib.py
|       └── sl_gt.py
└── README.md
```