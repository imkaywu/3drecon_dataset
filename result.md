---
layout: page
title: Results
permalink: /result/
---

## Synthetic dataset

### Mappings
We use the training dataset to evaluate the performance of each algorithm under all combinations of effective properties. The performance of each algorithm is compared to that of baseline method to determine if the result is acceptable or not. A mapping is determined for each method containing all the problem conditions that this specific algorithm can reliably work under.

#### Mapping of PMVS
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/training/mvs_training.pdf" style="border:none;">
<div class="thecap">Training results of PMVS</div>
</div>

|  Metrix  | Texture | Albedo | Specular | Rough |
| :------- | :-----: | :----: | :------: | :---: |
| Acc/Cmpt | 0.5     | 0.5    | 0.2      | -     |
|          | 0.5     | 0.8    | 0.2      | -     |
|          | 0.5     | 0.8    | 0.5      | -     |
|          | 0.8     | 0.2    | 0.2      | -     |
|          | 0.8     | 0.5    | 0.2      | -     |
|          | 0.8     | 0.8    | 0.2      | -     |
|          | 0.8     | 0.5    | 0.5      | -     |
|          | 0.8     | 0.8    | 0.5      | -     |
|          | 0.8     | 0.5    | 0.8      | -     |
|          | 0.8     | 0.8    | 0.8      | -     |

#### Mapping of EPS
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/training/ps_training.pdf" style="border:none;">
<div class="thecap">Training results of EPS</div>
</div>

|  Metrix  | Texture | Albedo | Specular | Rough |
| :------- | :-----: | :----: | :------: | :---: |
| Ang Err  | -       | 0.2    | 0.2      | 0.8   |
|          | -       | 0.2    | 0.5      | 0.8   |
|          | -       | 0.2    | 0.8      | 0.8   |
|          | -       | 0.5    | 0.2      | 0.8   |
|          | -       | 0.5    | 0.5      | 0.8   |
|          | -       | 0.5    | 0.8      | 0.8   |
|          | -       | 0.8    | 0.2      | 0.2   |
|          | -       | 0.8    | 0.2      | 0.8   |
|          | -       | 0.8    | 0.5      | 0.2   |
|          | -       | 0.8    | 0.5      | 0.8   |
|          | -       | 0.8    | 0.8      | 0.2   |
|          | -       | 0.8    | 0.8      | 0.8   |

#### Mapping of GSL
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/training/sl_training.pdf" style="border:none;">
<div class="thecap">Training results of GSL</div>
</div>

|  Metrix  | Texture | Albedo | Specular | Rough |
| :------- | :-----: | :----: | :------: | :---: |
| Acc/Cmpt | -       | 0.8    | 0.2      | 0.2   |
|          | -       | 0.8    | 0.5      | 0.2   |
|          | -       | 0.8    | 0.8      | 0.2   |
|          | -       | 0.8    | 0.2      | 0.8   |
|          | -       | 0.8    | 0.5      | 0.8   |
|          | -       | 0.8    | 0.8      | 0.8   |


### Testing
To validate that the mapping derived using the training dataset can be successfully applied to an object with a different shape, we need to generate a new test dataset with different objects. However, the sheer volume of shape variation make it practically impossible to carry out the evaluation. Therefore, we focus on evaluating the robustness of mapping with respect to ONE geometric property - concavity. The reason why we choose this property is that it cause global light transport thus can potentially pose challenge to some reconstruction algorithms.

We select three objects with increasing degree of concavity: bottle, knight, and king. The image examples are as follows:

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/synth_results/bottle.pdf" style="border:none;">
<div class="thecap">Results of bottle</div>
</div>

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/synth_results/knight.pdf" style="border:none;">
<div class="thecap">Results of knight</div>
</div>

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/synth_results/king.pdf" style="border:none;">
<div class="thecap">Results of king</div>
</div>


## Real-world dataset
See the `recon` page for more results.

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/real_results.pdf" style="border:none;">
<div class="thecap">Results of real-world objects</div>
</div>
