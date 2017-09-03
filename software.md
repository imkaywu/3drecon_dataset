---
layout: page
title: Software
permalink: /software/
---

In this section, we will give detailed introduction of our software that is used to run and evaluate all the implemented algorithms. The source code is available [here](https://github.com/imkaywu/3DRecon_Algo_Eval).

## Structure
The structure of the toolbox is as follows

```
.
├── algo
|   └── MVS
|   	└── PMVS
|           └── bin_x64
|   └── PS
|   	├── EPS
|       └── PSBox
|   ├── SL
|   └── VH
├── data
|   └── real
|       └── cup
|           ├── mvs
|           ├── ps
|           ├── sl
|           └── vh
|   └── synth
|       ├── sphere
|       ├── bottle
|       └── ref_obj
├── eval
|   ├── include
|   ├── io
|   └── real_world
|       ├── run.m
|       └── vis.m
|   └── synth
|       └── pairwise
|           ├── run.m
|           └── analysis.m
|       └── train
|           ├── train.m
|           └── analysis2.m
|       └── test
|           ├── test.m
|           └── analysis.m
├── groundtruth
|   ├── calib_result
|   ├── include
|   └── src
└── README.md
```

## Algorithms
We have implemented four classes of algorithms, they are summarized in the table below

| Class of Algo | Algo     | Summary  |
| ------------- | -------- | ---------|
| MVS           | PMVS  | patch based multi-view stereo |
| PS            | EPS   | example-base photometric stereo |
| PS            | LS-PS | least squares photometric stereo |
| SL            | GSL   | Gray-code structured light |
| VH            | VH    | visual hull |


## Evaluation
There are three metrics used
* accuracy
* completeness
* angular error

The `analysis.m` script in the corresponding directory can generate the final plot. Please to the `result` page for the plots of the results.

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