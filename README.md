<!---
Copyright 2020 The HuggingFace Team. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://huggingface.co/datasets/huggingface/documentation-images/raw/main/transformers-logo-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://huggingface.co/datasets/huggingface/documentation-images/raw/main/transformers-logo-light.svg">
    <img alt="Hugging Face Transformers Library" src="https://huggingface.co/datasets/huggingface/documentation-images/raw/main/transformers-logo-light.svg" width="352" height="59" style="max-width: 100%;">
  </picture>
  <br/>
  <br/>
</p>


<h3 align="center">
    <p>State-of-the-art Machine Learning for JAX, PyTorch and TensorFlow</p>
</h3>

<h3> This fork adds multiple images per text input support to InstructBLIP.</h3>

Vanilla InstructBLIP can only take (image, text) pair as input. This fork effectively allows ([image1,image2,...,imageM], text)
From a high level, the ViT and the QFormer treat images from one text input as a minibatch. The QFormer's outputs are reshaped and concatenated. Then it is prepended to the text embeddings fed to the Language Model. InstructBLIP can now successfully pull information from multiple images per text input, however it doesn't understand that it's looking at M separate images, treating all M images as part of the same scene.

This model can be trained normally but both training and inference speeds are moderately bottlenecked due to the need to process multiple images. The current implementation has a runtime of $O(LanguageModel(N) + QFormer\_ViT(N \times M))$ instead of $O(LanguageModel(N) + QFormer\_ViT(N))$.

[Test Demo](https://www.kaggle.com/sameen53/instructblip-multi-image-test)


