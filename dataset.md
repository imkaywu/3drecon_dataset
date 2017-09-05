---
layout: page
title: Dataset
permalink: /dataset/
---

[Download real-world dataset]()

The real-world dataset provided here is for non-commercial research/educational use only.

[Download synthetic projects](https://github.com/imkaywu/blender_scripts)

We provide the Blender projects and scripts that are used to generate the synthetic datasets.

## Real-world dataset
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/dataset/real_world_dataset.png" style="border:none;">
<div class="thecap">Images of real-world objects</div>
</div>


## Synthetic dataset

### Effect of property
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

### Generation of datasets

#### Pairwise
First, we need to evaluate the pairwise relation between any two properties and the effect on algorithms. Therefore, the **first** synthetic dataset consists of **six** sub-groups.

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

#### Training
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