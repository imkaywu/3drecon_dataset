---
layout: page
title: Dataset
permalink: /dataset/
---
## Table of content
* [Real-world dataset](#real_world_dataset)
	* [Overview](#real_world_overview)
	* [Structure of MVS datasets](#struct_mvs)
	* [Structure of PS datasets](#struct_ps)
	* [Structure of SL datasets](#struct_sl)
* [Synthetic dataset](#synth_dataset)
	* [Structure of datasets](#struct_synth)
	* [Effects of properties](#prop_effect)
	* [Generate synthetic datasets](#gen_synth_dataset)
* [Downloads](#download)

## Real-world dataset <a name="real_world_dataset"></a>

### Overview of real-world objects <a name="real_world_overview"></a>
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/real_world_dataset.png" style="border:none;">
<div class="thecap">Images of real-world objects</div>
</div>

### Structure of MVS datasets <a name="struct_mvs"></a>
The directory structure and naming convention are the same as those of [PMVS](https://www.di.ens.fr/pmvs/documentation.html). The directory structure is as follows:
```
.
├── model
├── txt
├── visualize
├── option.txt
```
* The `model` directory contains the reconstructed model.
* the `txt` directory contains the camera calibration results. The files must be named as `00000000.txt`, `00000001.txt`, and so on. The format of the camera parameter also follows that of PMVS, which is 
```
CONTOUR
P[0][0] P[0][1] P[0][2] P[0][3]
P[1][0] P[1][1] P[1][2] P[1][3]
P[2][0] P[2][1] P[2][2] P[2][3]
```
* the `visualize` directory contains the captured images, The images are named as `00000000.jpg`, `00000001.jpg`, and so on.

### Structure of PS datasets <a name="struct_ps"></a>
The directory structure of PS datasets are as follows
```
.
├── file.txt
├── mask
|   ├── mask_tar.png
|   ├── mask_ref_diff.png
|   ├── mask_ref_spec.png
|   └── mask.txt
├── tar_obj
├── ref_obj
└── nomral.png
```
* `file.txt` contains the names of all the images in the directory, including names of target, reference, and mask images. The structure of this file is as follows
```
[num_of_imgs] [num_of_ref_objects]
[names of ref_1 under various lighting]
[names of ref_2 under various lighting]
[names of target under various lighting]
[num_of_ref_objects]
[name of mask of ref_1]
[name of mask of ref_2]
[name of mask of target]
``` 
* `mask` contains mask images, and `mask.txt` file, which gives information regarding the size of the mask images, and center and radius of the imaged reference objects.
* `tar_obj` contains images of the target objects.
* `ref_obj` contains images of the reference objects.
* `normal.png` is the estimated normal map.

### Structure of SL datasets <a name="struct_sl"></a>
The Structure Light datasets contain images captured under the projection of column and row patterns. For each projection pattern, the reverse pattern is projected as well to eliminate the effects of global light transport. The resolution of the projector is 1024*768, thus, 10 temporally encoded patterns are needed. Two images with light on and off are captured to help the decoding process. Thus, the total number of images are 2*2*10+2=42.

## Synthetic dataset <a name="synth_dataset"></a>

### Structure of synthetic datasets <a name="struct_synth"></a>
For each synthetic object, there needs to be a dataset for each combination of hardware setups (3: MVS, PS, SL), visual, and geometric properites (number_of_prop_conds * perm_of_prop_vals), as shown in the figure below. The directory structure under each individual dataset follows that of the real-world datasets.
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/dataset_structure.pdf" style="border:none;">
<div class="thecap">Directory structure of synthetic datasets.</div>
</div>

### Effect of property <a name="prop_effect"></a>
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/tex.png" style="border:none;">
<div class="thecap">Visual effect of texture changing from 0.1 to 1.</div>
</div>

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/alb.png" style="border:none;">
<div class="thecap">Visual effect of albedo changing from 0.1 to 1.</div>
</div>

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/spec.png" style="border:none;">
<div class="thecap">Visual effect of specularity changing from 0.1 to 1.</div>
</div>

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/rough.png" style="border:none;">
<div class="thecap">Visual effect of roughness changing from 0.1 to 1.</div>
</div>

### Generation of datasets <a name="gen_synth_dataset"></a>

#### Stage 1: discover *effective properties*
First, we need to find the effective properties for each algorithm to reduce the dimension of problem space. A reasonable approach is to evaluate the performance of the algorthm under **one** changing property. However, this might not successful, an intuitive example is: the impact of roughness is insignificant when surface is purely diffuse. We can only discover the effct of roughness when the surface reflectance (specularity) is changing at the same time. Thus, we need to evaluate the pairwise relation between any two properties and their effect on the algorithm. Therefore, the **first** synthetic dataset consists of **six** sub-groups.

```
.
├── pairwise
|   └── tex_alb
|   	├── 0202
|   	├── 0205
|   	├── 0208
|   	├── 0502
|   	├── 0505
|   	├── 0508
|   	├── 0802
|   	├── 0805
|   	└── 0808
|   └── tex_spec
|   	└── ...
|   └── tex_rough
|   	└── ...
|   └── alb_spec
|   	└── ...
|   └── alb_rough
|   	└── ...
|   └── spec_rough
|   	└── ...
```

#### Stage 2: discover the *effective problem domain*
Once we have identified the properties that have an impact on the algorithm, we proceed to generate a dataset consisting of all parameter combinations of effective properties. For instance, if the first two out of three properties are effective, then the training dataset has the following structure
```
.
├── training
|   ├── 0202XX
|   ├── 0205XX
|   ├── 0208XX
|   ├── 0502XX
|   ├── 0505XX
|   ├── 0508XX
|   ├── 0802XX
|   ├── 0805XX
|   └── 0808XX
```
where `XX` can be any value combination since the corresponding property doesn't have an influence on the algorithm. From this dataset, we determine the mapping that is from problem condition to appropriate algorithms.

#### Testing
To validate that the mapping derived using the training dataset can be successfully applied to an object with a different shape, we need to generate a new test dataset with different objects. However, the sheer volume of shape variation make it practically impossible to carry out the evaluation. Therefore, we focus on evaluating the robustness of mapping with respect to ONE geometric property - concavity. The reason why we choose this property is that it cause global light transport thus can potentially pose challenge to some reconstruction algorithms.

We select three objects with increasing degree of concavity: bottle, knight, and king. The image examples are as follows:

<div class="container">
	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/bottle_mvs.jpg" style="border:none;">
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/bottle_ps.jpg" style="border:none;">
	<h6>Synthetic object 1: bottle</h6>
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/bottle_sl.jpg" style="border:none;">
	</div>
</div>

<div class="container">
	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/knight_mvs.jpg" style="border:none;">
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/knight_ps.jpg" style="border:none;">
	<h6>Synthetic object 2: knight</h6>
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/knight_sl.jpg" style="border:none;">
	</div>
</div>

<div class="container">
	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/king_mvs.jpg" style="border:none;">
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/king_ps.jpg" style="border:none;">
	<h6>Synthetic object 3: king</h6>
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/king_sl.jpg" style="border:none;">
	</div>
</div>

## Downloads <a name="download"></a>
[Download real-world dataset]()

The real-world dataset provided here is for non-commercial research/educational use only.

[Download synthetic projects](https://github.com/imkaywu/blender_scripts)

We provide the Blender projects and scripts that are used to generate the synthetic datasets.