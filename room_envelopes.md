---
layout: nerfies
title: "Room Envelopes: A Synthetic Dataset for Indoor Layout Reconstruction from Images"
description:
authors:
  - name: Sam Bahrami
    url: https://sambahrami.github.io
  - name: Dylan Campbell
    url: https://sites.google.com/view/djcampbell
keywords: 3D Scene Reconstruction, Indoor Scene Understanding, Layout Estimation, Synthetic Data
links:
  - text: Paper
    url: "https://arxiv.org"
    icon: "fas fa-file-pdf"
    primary: true
  - text: Code (Coming Soon)
    url: "#"
    icon: "fab fa-github"
  - text: Dataset (Coming Soon)
    url: "#"
    icon: "fas fa-database"
---

We introduce Room Envelopes, a synthetic dataset that provides **dual pointmap representations** for indoor scene reconstruction. Each image comes with three complementary views: RGB image, visible surface (depth and normals), and layout surface (depth and normals), with examples below. The **visible surface** captures all directly visible geometry including furniture and objects, while the **layout surface** shows structural elements as they would appear without occlusion. This dual representation enables direct supervision for layout reconstruction in occluded regions.

## Dataset Examples

<div class="columns is-centered">
  <div class="column is-full-width">
    <div class="columns is-vcentered">
      <div class="column has-text-centered" style="display: flex; flex-direction: column;">
        <div style="flex: 1; display: flex; align-items: center; justify-content: center;">
          <img src="photos/room_envelopes/examples/ai_011_009-cam_00-9_image.png" style="width: 100%; border-radius: 10px;">
        </div>
        <p class="has-text-weight-bold">RGB Image</p>
      </div>
      <div class="column has-text-centered">
        <img src="photos/room_envelopes/examples/ai_011_009-cam_00-9_first_depth.png" style="width: 100%; border-radius: 10px; margin-bottom: 0.5rem;">
        <img src="photos/room_envelopes/examples/ai_011_009-cam_00-9_first_normal.png" style="width: 100%; border-radius: 10px;">
        <p class="has-text-weight-bold">Visible Surface</p>
        <p class="is-size-7">Depth & Normals</p>
      </div>
      <div class="column has-text-centered">
        <img src="photos/room_envelopes/examples/ai_011_009-cam_00-9_layout_depth.png" style="width: 100%; border-radius: 10px; margin-bottom: 0.5rem;">
        <img src="photos/room_envelopes/examples/ai_011_009-cam_00-9_layout_normal.png" style="width: 100%; border-radius: 10px;">
        <p class="has-text-weight-bold">Layout Surface</p>
        <p class="is-size-7">Depth & Normals</p>
      </div>
    </div>

    <div class="columns is-vcentered" style="margin-top: 3rem;">
      <div class="column has-text-centered" style="display: flex; flex-direction: column;">
        <div style="flex: 1; display: flex; align-items: center; justify-content: center;">
          <img src="photos/room_envelopes/examples/ai_030_009-cam_00-70_image.png" style="width: 100%; border-radius: 10px;">
        </div>
        <p class="has-text-weight-bold">RGB Image</p>
      </div>
      <div class="column has-text-centered">
        <img src="photos/room_envelopes/examples/ai_030_009-cam_00-70_first_depth.png" style="width: 100%; border-radius: 10px; margin-bottom: 0.5rem;">
        <img src="photos/room_envelopes/examples/ai_030_009-cam_00-70_first_normal.png" style="width: 100%; border-radius: 10px;">
        <p class="has-text-weight-bold">Visible Surface</p>
        <p class="is-size-7">Depth & Normals</p>
      </div>
      <div class="column has-text-centered">
        <img src="photos/room_envelopes/examples/ai_030_009-cam_00-70_layout_depth.png" style="width: 100%; border-radius: 10px; margin-bottom: 0.5rem;">
        <img src="photos/room_envelopes/examples/ai_030_009-cam_00-70_layout_normal.png" style="width: 100%; border-radius: 10px;">
        <p class="has-text-weight-bold">Layout Surface</p>
        <p class="is-size-7">Depth & Normals</p>
      </div>
    </div>
  </div>
</div>


## Key Contributions

1. **Room Envelopes Dataset**: An indoor synthetic dataset providing an image, a visible surface pointmap, and a layout surface pointmap for each camera pose

2. **Feed-forward Scene Reconstruction**: A model demonstrating effective room layout estimation using this dataset

3. **Novel Representation**: The only dataset providing both first visible depth and layout depth representations for comprehensive indoor scene understanding

## Why Room Envelopes?

Current models for indoor scene reconstruction typically use depth images or layered depth representations for training, but these formats have inherent limitations:

- **Depth maps** only capture the first visible surface, losing information about underlying room structure
- **Layered depth** creates artificial discontinuities where continuous surfaces are fragmented across layers
- Feed-forward models struggle at **occlusion edges**, predicting averaged depth rather than decisive geometry
- Many existing layout estimation methods rely on a **planar assumption**, assuming all room surfaces (walls, floors, ceilings) are perfectly flat planes, which limits their applicability to more complex architectural geometries

Room Envelopes addresses these limitations by providing:

- **Structural Clarity** - Unoccluded views of room boundaries  
- **Direct Supervision** - Pixel-aligned supervision for layout estimation  
- **Less Ambiguity** - No uncertainty about layer assignment  

## Layout Estimation on Real-World Examples

We trained a layout estimation model by fine-tuning a feed-forward depth estimator, and ran it on real-world indoor scenes. The model, trained exclusively on our synthetic dataset, shows promising generalization capabilities to real-world environments.

<div class="columns">
  <div class="column has-text-centered">
    <p class="has-text-weight-bold is-size-6">Real-World RGB Image</p>
  </div>
  <div class="column has-text-centered">
    <p class="has-text-weight-bold is-size-6">Predicted Layout Depth</p>
  </div>
  <div class="column has-text-centered">
    <p class="has-text-weight-bold is-size-6">Predicted Layout Normals</p>
  </div>
</div>

<div class="columns">
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/6.jpg" style="width: 100%; border-radius: 10px;">
  </div>
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/6.jpg_layout_depth_colorised.png" style="width: 100%; border-radius: 10px;">
  </div>
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/6.jpg_layout_normals.png" style="width: 100%; border-radius: 10px;">
  </div>
</div>

<div class="columns">
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/2.jpg" style="width: 100%; border-radius: 10px;">
  </div>
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/2.jpg_layout_depth_colorised.png" style="width: 100%; border-radius: 10px;">
  </div>
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/2.jpg_layout_normals.png" style="width: 100%; border-radius: 10px;">
  </div>
</div>

<div class="columns">
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/3.jpg" style="width: 100%; border-radius: 10px;">
  </div>
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/3.jpg_layout_depth_colorised.png" style="width: 100%; border-radius: 10px;">
  </div>
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/3.jpg_layout_normals.png" style="width: 100%; border-radius: 10px;">
  </div>
</div>

<div class="columns">
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/4.jpg" style="width: 100%; border-radius: 10px;">
  </div>
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/4.jpg_layout_depth_colorised.png" style="width: 100%; border-radius: 10px;">
  </div>
  <div class="column has-text-centered">
    <img src="photos/room_envelopes/4.jpg_layout_normals.png" style="width: 100%; border-radius: 10px;">
  </div>
</div>

## BibTeX

```bibtex
@article{bahrami2025roomenvelopes,
  title={Room Envelopes: A Synthetic Dataset for Indoor Layout Reconstruction from Images},
  author={Bahrami, Sam and Campbell, Dylan},
  journal={arXiv preprint arXiv:XXXX.XXXXX},
  year={2025}
}
```
