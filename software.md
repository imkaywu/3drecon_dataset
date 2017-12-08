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
* [License](#license)

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

#### Surface integration from surface gradients or normals
```
algo/PS/DfN/compute_heightMap.m
algo/PS/DfN/integrate_horn2.m
algo/PS/DfN/DepthFromGradient.m
```

#### Encode and decode a normal map into a color map
```
algo/PS/include/encode.m
algo/PS/include/decode.m
```

#### Convert a normal map to a `N x 3` matrix
```
algo/PS/include/nmap2norm.m
algo/PS/include/norm2nmap.m
```

#### Shape estimation from surface normals: depends on sub-routines in `algo/PS/DfN`
```
algo/PS/include/esti_surf.m
```

#### Display normal vectors as arrows
```
algo/PS/include/show_surfNorm.m
```

#### Write to a PLY file: vertex, normal, color
```
algo/PS/io/write_ply.m
```

#### Main example-based Photometric Stereo algorithm for spatially-varying BRDF: read file names
```
algo/PS/src/EPS/main_svbrdf.m
```

#### Main example-based Photometric Stereo algorithm for spatially-invarient BRDF
```
algo/PS/src/EPS/main_ivbrdf.m
```

#### Sub-routine of example-based Photometric Stereo for spatially-varying BRDF: read images, and pre-processing
```
algo/PS/src/EPS/src/exmp_based_ps_sv.m
```

#### Sub-routine of example-based Photometric Stereo: estimate normal for surfaces with spatially-varying BRDFs
```
algo/PS/src/EPS/src/normal_esti_coarse2fine_ps.hpp
algo/PS/src/EPS/src/normal_esti_coarse2fine_ps.cpp
algo/PS/src/EPS/src/mex_normal_esti_coarse2fine_ps.cpp
algo/PS/src/EPS/src/normal_esti_coarse2fine_ps.mexw64
```

#### Main linear least squares Photometric Stereo
```
algo/PS/src/LLS-PS/main_lls_ps
```

#### Sub-routine linear least squares Photometric Stereo
```
algo/PS/src/LLS-PS/PhotometricStereo.m
```

#### Load input images for photometric stereo
```
algo/PS/src/LLS-PS/PSLoadProcessedImages.m
```


#### Evaluate scaled normal estimation by intensity error
```
algo/PS/src/LLS-PS/EvalNEstimateByIError.m
```

#### Run Gray-coded Structured Light algorithm
```
algo/SL/slRecon.m
```

#### Compute additional data for triangulation step
```
algo/SL/slCalib.m
```

#### Convert a binary or Gray sequence to a decimal
```
algo/SL/utilities/bin2dec.m
algo/SL/utilities/gray2dec.m
```

#### Generate binary or Gray codes for vertical and horizontal stripe patterns
```
algo/SL/utilities/bincode.m
algo/SL/utilities/graycode.m
```

#### Display the camera-projector calibration result
```
algo/SL/utilities/disp_calib.m
```

#### Least-squares plane fitting
```
algo/SL/utilities/fitPlane.m
```

#### Efficient 3D scatter plot
```
algo/SL/utilities/fscatter3.m
```

#### Find the intersection of a line with a plane
```
algo/SL/utilities/intersect_line_plane.m
```

#### Find the line of sight for a given image pixel
```
algo/SL/utilities/pixel2ray
```

#### Write to a PLY file: vertex, color
```
algo/SL/utilities/write_ply.m
```

#### Create heatmaps
```
eval/include/heatmaps/heatmap.m
```

#### Compute `accuracy` and `completeness`
```
eval/include/eval_acc_cmplt.m
```

#### Compute `angular error`
```
eval/include/eval_angle.m
```

#### Various IO routines
```
eval/io/ply_read_vc.mexw64
eval/io/ply_read_vf.mexw64
eval/io/ply_read_vnc.mexw64
eval/io/ply_read_vnf.mexw64
```

#### Run and evaluate 3D reconstruction algorithms on synthtic dataset
```
eval/synth/eval_prop/run.m
eval/synth/eval_prop/evaluate.m
eval/synth/eval_algo/run.m
eval/synth/eval_algo/evaluate.m
eval/synth/eval_interp/run.m
eval/synth/eval_interp/evaluate.m
```

#### Run and evaluate 3D reconstruction algorithms on real-world dataset
```
eval/real_world/run.m
```

<!-- ## Data generation
The blender projects and python scripts are [here](https://github.com/imkaywu/blender_scripts). The command is
```
blender proj/mvs.blend -b -P scripts/pairwise/mvs.py
``` -->

## License
See the file `./License.md'
