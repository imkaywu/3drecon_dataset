---
layout: page
title: Documentation
permalink: /document/
mathjax: true
---
## Table of content
* [Overview of real-world dataset](#real_world_overview)
* [Real-world MVS data](#real_mvs_data)
	* [Setup](#real_mvs_setup)
	* [Calibration](#real_mvs_calib)
	* [Data formats](#real_mvs_format)
* [Real-world PS data](#real_ps_data)
	* [Setup](#real_ps_setup)
	* [Calibration](#real_ps_calib)
	* [Data formats](#real_ps_format)
* [Real-world SL data](#real_sl_data)
	* [Setup](#real_sl_setup)
	* [Calibration](#real_sl_calib)
	* [Data formats](#real_sl_format)
* [Real-world VH data]()
* [Overview of synthetic dataset](#synth_overview)
* [Synthetic data](#synth_dataset)
	* [Structure of dataset](#struct_synth)
	* [Effects of properties](#prop_effect)
* [Evaluation](#eval)

## 1. Overview of real-world objects <a name="real_world_overview"></a>
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/doc/real_world_dataset.png" style="border:none;">
<div class="thecap">Images of real-world objects</div>
</div>

## 2. Real-world MVS data <a name="real_mvs_data"></a>
The directory structure and naming convention are the same as those of [PMVS](https://www.di.ens.fr/pmvs/documentation.html). The directory structure is as follows:
```
.
├── model
├── txt
├── visualize
└── option.txt
```

### 2.1. Setup <a name="real_mvs_setup"></a>
For MVS, we capture the dataset by positioning the camera in three different heights. The objects are about 30-50cm away from the camera, and stays fixed on a turntable. We have followed the following two steps to acquire data: 1) put the camera at a different height, adjust the orientation so that the object in at the center of the frame; 2) take pictures while rotating the table. The table rotates approximately 30  every time. We rotate it 12 times and in total, we can obtain 12 image per height.

### 2.2. Calibratoin <a name="real_mvs_calib"></a>
For MVS, a calibration pattern proposed in Bo Li is imaged under the object, which is used for calibrating the camera position and orientation by Structure from Motion softwares, such as VisualSfM. The focal length is known a priori and remains fixed duing the image capturing process. Thus the extrinsic parameters of the camera can be retrieved up to a similarity transformation, and the reconstruction result is a metric/euclidean recontruction.

### 2.3. Data format <a name="real_mvs_format"></a>
Images are captured by Nikon D70S camera with a $$18-70mm$$ lens in the `jpeg` format. The naming convension of images follows that of PMVS developed by Furukawa. For instance, the images are named as `00000000.xxx`, `00000001.xxx`, and so on. The images are stored in the `visualize` directory.

The `txt` directory contains the camera calibration results. The files must be named as `00000000.txt`, `00000001.txt`, and so on. The format of the camera parameter also follows that of PMVS, which is
```
CONTOUR
P[0][0] P[0][1] P[0][2] P[0][3]
P[1][0] P[1][1] P[1][2] P[1][3]
P[2][0] P[2][1] P[2][2] P[2][3]
```

## 3. Real-world PS data <a name="real_ps_data"></a>
The directory structure of PS dataset is as follows
```
.
├── ref_obj
|   └── 0000
|       ├── 000000xx.jpg
|       └── mask.bmp
|   └── 0001
|       ├── 000000xx.jpg
|       └── mask.bmp
├── 000000xx.jpg
├── mask.bmp
└── nomral.png
```

### 3.1. Setup <a name="real_ps_setup"></a>
For PS, a 70-200mm lens, a handheld lamp, and two reference objects (dif- fuse and glossy) are used. The objects are positioned about 3m from the camera to approximate orthographic projection. To avoid inter-reflection, all data are cap- tured in a dark room with everying covered by black cloth except the target object. We use a hand-held lamp as the light source and choose close to frontal viewpoints to avoid severe self-shadowing effect. We take 20 images per object and select 15 plus images depending on the severity of the self-shadow effect.

### 3.2. Calibration <a name="real_ps_calib"></a>
For most PS algorithms, i.e., calibrated PS algorithms, it is necessary to esti- mate the light direction and intensity. However, the selected PS algorithm can deal Appearance with unknown light sources and spatially-varying BRDFs. Thus, light calibration is not a required step. Though it is preferable to correct the non-linear response of camera, Hertzmann and Seitz discovered that it was unnecessary for EPS. Thus, we did not perform the radiometric calibration step. No geometric calibration of the camera is needed.

### 3.3. Data format <a name="real_ps_format"></a>
Images are captured by Nikon D70S camera with a $$70-200mm$$ lens in the `jpeg` format. Images are named following the convention: the first image is named as `00000000.xxx`, the second is named as `00000001.xxx`, and so on.

## 4. Real-world SL data <a name="real_sl_data"></a>

### 4.1. Setup
For SL, we use a Sanyo Pro xtraX Multiverse projector with a resolution of $$1024\times 768$$. The baseline angle of the camera projector pair is approximately 10  . To alleviate the effect of ambient light, all images are captured with room lights off. To counteract the effect of inter-reflection, additional images are captured by projecting an all-white and all-black patterns.

The Structure Light datasets contain images captured under the projection of column and row patterns. For each projection pattern, the reverse pattern is projected as well to eliminate the effects of global light transport. The resolution of the projector is 1024*768, thus, 10 temporally encoded patterns are needed. Two images with light on and off are captured to help the decoding process. Thus, the total number of images are $$2\times 2\times 10+2=42$$.

### 4.2. Calibration
For SL, a opensource camera-projector calibration software developed by Moreno and Taubin is used for calibration. This technique works by projecting temporal patterns onto the calibration pattern, and uses local homography to individually translate each checkerboard corner from the camera plane to the projector plane. This technique can estimate both the intrinsic parameter and camera and projector, and the relative position and orientation.

### 4.3. Data formats
Images are captured by Nikon D70S camera with a $$18-70mm$$ lens in the `jpeg` or `bmp` format. Images are named following the convention: the first image is named as `0000.xxx`, the second is named as `0001.xxx`, and so on.

<!-- * `file.txt` contains the names of all the images in the directory, including names of target, reference, and mask images. The structure of this file is as follows
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
* `normal.png` is the estimated normal map.-->

## 5. Overview of synthetic dataset <a name="synth_dataset"></a>
<div class="container">
	<div class="imgmul4">
	<img src="{{site.url}}{{site.baseurl}}/assets/doc/bust.jpg" style="border:none;">
	<h6>Bust</h6>
	</div>

	<div class="imgmul4">
	<img src="{{site.url}}{{site.baseurl}}/assets/doc/vase0.jpg" style="border:none;">
	<h6>Vase 0</h6>
	</div>

	<div class="imgmul4">
	<img src="{{site.url}}{{site.baseurl}}/assets/doc/barrel.jpg" style="border:none;">
	<h6>Barrel</h6>
	</div>

	<div class="imgmul4">
	<img src="{{site.url}}{{site.baseurl}}/assets/doc/vase1.jpg" style="border:none;">
	<h6>Vase 1</h6>
	</div>
</div>

## 6. Synthetic dataset <a name="synth_dataset"></a>

Synthetic data is used:
* discover the properties that have a significant main effect or interaction effect on algorithm performance (termed *effective properties*);
* evaluate algorithm performance under conditions consisting solely of *effective properties*;
* evaluate the performance of interprete.

### 6.1. Structure of dataset <a name="struct_synth"></a>
Thus the structure of the first two synthetic datasets are similar, they have the following structure. The source code used to generate these dataset can be found in the Software page.

```
.
├── prob_cond_1
|    ├── mvs
|    ├── ps
|    └── sl
...
├── prob_cond_N
|    ├── mvs
|    ├── ps
|    └── sl
```

<!-- ### Structure of synthetic datasets <a name="struct_synth"></a>
For each synthetic object, there needs to be a dataset for each combination of hardware setups (3: MVS, PS, SL), visual, and geometric properites (number_of_prop_conds * perm_of_prop_vals), as shown in the figure below. The directory structure under each individual dataset follows that of the real-world datasets.
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/doc/dataset_structure.pdf" style="border:none;">
<div class="thecap">Directory structure of synthetic datasets.</div>
</div> -->

### 6.2. Effect of property <a name="prop_effect"></a>
Here we show the visual effect of change each property from 0 to 1.
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/doc/tex.png" style="border:none;">
<div class="thecap">Visual effect of texture changing from 0 to 1.</div>
</div>

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/doc/alb.png" style="border:none;">
<div class="thecap">Visual effect of albedo changing from 0 to 1.</div>
</div>

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/doc/spec.png" style="border:none;">
<div class="thecap">Visual effect of specularity changing from 0 to 1.</div>
</div>

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/doc/rough.png" style="border:none;">
<div class="thecap">Visual effect of roughness changing from 0 to 1.</div>
</div>

<!-- ### Generation of datasets <a name="gen_synth_dataset"></a>

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
where `XX` can be any value combination since the corresponding property doesn't have an influence on the algorithm. From this dataset, we determine the mapping that is from problem condition to appropriate algorithms. -->

<!-- #### Testing
To validate that the mapping derived using the training dataset can be successfully applied to an object with a different shape, we need to generate a new test dataset with different objects. However, the sheer volume of shape variation make it practically impossible to carry out the evaluation. Therefore, we focus on evaluating the robustness of mapping with respect to ONE geometric property - concavity. The reason why we choose this property is that it cause global light transport thus can potentially pose challenge to some reconstruction algorithms.

We select three objects with increasing degree of concavity: bottle, knight, and king. The image examples are as follows:

<div class="container">
	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/doc/bottle_mvs.jpg" style="border:none;">
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/doc/bottle_ps.jpg" style="border:none;">
	<h6>Synthetic object 1: bottle</h6>
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/doc/bottle_sl.jpg" style="border:none;">
	</div>
</div>

<div class="container">
	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/doc/knight_mvs.jpg" style="border:none;">
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/doc/knight_ps.jpg" style="border:none;">
	<h6>Synthetic object 2: knight</h6>
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/doc/knight_sl.jpg" style="border:none;">
	</div>
</div>

<div class="container">
	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/doc/king_mvs.jpg" style="border:none;">
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/doc/king_ps.jpg" style="border:none;">
	<h6>Synthetic object 3: king</h6>
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}/{{site.baseurl}}/assets/doc/king_sl.jpg" style="border:none;">
	</div>
</div> -->

## 7. Evaluation <a name="eval"></a>
**Accuracy**: the distance between the points in the reconstruction $$R$$ and the nearest points on ground truth $$G$$ is computed, and the distance $$d$$ such that $$X\%$$ of the points on $$R$$ are within distance $$d$$ of $$G$$ is considered as accuracy. A reasonable $$d$$ value is between $$[3, 5]mm$$, and $$X$$ is set as $$95$$. The lower the accuracy value, the better the reconstruction result. Note that as the accuracy improves, the *accuracy value* goes down.

**Completeness**: we compute the distance from $$G$$ to $$R$$. Intuitively, points on $$G$$ are not covered if no suitable nearest points on $$R$$ are found. A more practical approach computes the fraction of points of $$G$$ that are within an allowable distance $$d$$ of $$R$$. Note that as the completeness improves, the *completeness value* goes up.

**Angular error**: depth information is lost since only one viewpoint is used. Thus, the previous metrics are not applicable. Here we employ another evaluation criteria that is widely adopted, which is based on the statistics of angular error. For each pixel, the angular error is calculated as the angle between the estimated and ground truth normal, *i.e.* $$arccos$$($$n_g^T n$$), where $$n_g$$ and $$n$$ are the ground truth and estimated normals respectively. In addition to the mean angular error, we also calculate the standard deviation, minimum, maximum, median, first quartile, and third quartile of angular errors for each estimated normal map.

<div class="container">
	<div class="imgmul3">
	<img src="{{site.url}}{{site.baseurl}}/assets/doc/acc.png" style="border:none;">
	<h6>To compute accuracy, for each vertex on R, we find the nearest point on G. We augment G with a hole filled region (solid red) to give a mesh G'. Vertices (shown in red) that project to the hole filled region are not used in the accuracy metric.</h6>
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}{{site.baseurl}}/assets/doc/cmplt.png" style="border:none;">
	<h6>To measure completeness, for each vertex on G, we find the nearest points on R (where the dotted lines terminate on R). Vertices (shown in red) that map to the boundary of R or are beyond an “inlier distance” from R to G are treated as not covered by R.</h6>
	</div>

	<div class="imgmul3">
	<img src="{{site.url}}{{site.baseurl}}/assets/doc/angular_error.pdf" style="border:none;">
	<h6>Angular error</h6>
	</div>
</div>
