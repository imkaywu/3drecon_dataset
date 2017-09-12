---
layout: page
title: Results
permalink: /result/
---

Given a specific description, the proof-of-concept interpreter will select an algorithm, and any object that matches this description should be well reconstructed by this algorithm. We use the descriptions that match the problem conditions of the testing objects so that each object should at least return one well reconstructed result. Since a problem condition could be mapped to multiple algorithms, an object that doesn’t match the description could potentially have a satisfactory result as well.

## Synthetic dataset
We generate a dataset of four objects, see `Dataset` and `Recon` page. The mapping from problem conditions to algorithms are summarized in the table below. The reconstruction results of test objects and those of the baseline method are shown in the figure below. See the corresponding videos for mor details.

| Class # | Object | Texture | Albedo | Specular | Rough | Mapping |
| :------ | :----- | :------ | :----- | :------- | :---- | :-----: |
| 1       | barrel | 0.8     | 0.8    | 0.2      | 0.8   | PMVS, EPS, GSL |
| 2       | vase0  | 0.8     | 0.8    | 0.8      | 0.2   | PMVS, EPS |
| 3       | bust   | 0.2     | 0.8    | 0.2      | 0.8   | EPS, GSL |
| 4       | vase1  | 0.2     | 0.8    | 0.8      | 0.2   | EPS |

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/results/synth.png" style="border:none;">
<div class="thecap">The evaluation of interpreter using synthetic objects. The first column presents the description provided to the interpreter. Description $$i$$ matches with condition $$i$$ in the table above. The last column is the algorithm selected by the interpreter. The object of which condition matches the description is labeled in green rectangle. Since the interpreter would return a successful reconstruction given a description that matches the condition, the quality of reconstruction of the labeled objects indicates success/failure of the interpreter.</div>
</div>

### synthetic object 1: barrel
[TBD]

### synthetic object 2: vase0
[TBD]

### synthetic object 3: bust
[TBD]

### synthetic object 4: vase1
[TBD]


## Real-world dataset
We generate a real-world dataset, see page `Dataset` and `Recon`. The mapping from problem conditions to algorithms are summarized in the table below.

| Class # | Object | Texture | Albedo | Specular | Rough | Mapping |
| :------ | :----- | :------ | :----- | :------- | :---- | :-----: |
| 1       | pot    | 0.8     |0.8(0.2)| 0.2      | 0.8   | PMVS, GSL |
| 2       | vase   | 0.8     |0.5(0.2)| 0.5      | 0.2   | PMVS |
| 3       | status | 0.2     | 0.8    | 0.2      | 0.8   | EPS, GSL |
| 4       | cup    | 0.2     | 0.8    | 0.5      | 0.2   | EPS, GSL |

<div class="imgcap">
<img src="{{site.url}}/{{site.baseurl}}/assets/results/real.png" style="border:none;">
<div class="thecap">Results of real-world objects</div>
</div>

### real-world object 1: pot
<iframe width="560" height="315" src="https://www.youtube.com/embed/eI83_ww79YY" frameborder="0" allowfullscreen></iframe>

### real-world object 2:vase
<iframe width="560" height="315" src="https://www.youtube.com/embed/lz7_c8o4FHo" frameborder="0" allowfullscreen></iframe>

### real-world object 3: statue
<iframe width="560" height="315" src="https://www.youtube.com/embed/riQifaIcMdg" frameborder="0" allowfullscreen></iframe>

### real-world object 4: cup
<iframe width="560" height="315" src="https://www.youtube.com/embed/K0TpjIC07Vk" frameborder="0" allowfullscreen></iframe>
