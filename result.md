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


#### Bottle
The first test object is a bottle, which has shallow indentations on the surface, *i.e.,* low level concavity. The first column presents the results of the mapping, and the algorithms that produce acceptable results are labeled in the green box. All quantitative and qualitative results align with those of the mapping, so we claim that the mapping is successfully applied to a surface with low concavity.
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/synth_results/bottle.pdf" style="border:none;">
<div class="thecap">Results of bottle</div>
</div>

#### Knight
The second object is a knight chess piece, which has medium concavity. In this case, we can see that the results of PMVS and GSL are still consistent with the mapping. However, the EPS fails to return reliable reconstruction in cases of high specular, such as (b) and (d), which is manifested by an increase in the variation of the angular error, represented by standard variation and the interquartile range. Thus, we claim that the mapping is still valid for PMVS, GSL and for EPS in low specular cases.
<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/synth_results/knight.pdf" style="border:none;">
<div class="thecap">Results of knight</div>
</div>

#### King
The last synthetic object is the king chess piece, which has the largest concavity. In the case of high concavity, quantitative results of PMVS and GSL are still consistent with that of the mapping. However, the results of the EPS become inconsistent, which is a result of the cast shadow from the large concavity. Though the result of EPS under conditions (a) and (c) are still better than that of the baseline, the median angular error is above the acceptable threshold, which is $$10^\circ$$ in most cases. We can see with more clarity from the normal maps that the cast shadow on the "cross" leads to completely inaccurate normal estimation, which is labeled by a red rectangle.
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
