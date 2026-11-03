---
layout: post
title: "Hello, World"
description: "First post — what this blog is for, and a quick test of math and code rendering."
tags: [meta]
math: true
---

Welcome to my blog! I plan to write here about things I'm learning and working on — diffusion models,
RL post-training for language models, and research notes in general.

## Math works

The forward process of a diffusion model adds Gaussian noise:

$$
q(x_t \mid x_0) = \mathcal{N}\!\left(x_t;\ \sqrt{\bar\alpha_t}\, x_0,\ (1-\bar\alpha_t) I\right),
$$

and inline math like $\nabla_x \log p_t(x)$ works too.

## Code works

```python
import torch

def q_sample(x0, t, alpha_bar):
    noise = torch.randn_like(x0)
    return alpha_bar[t].sqrt() * x0 + (1 - alpha_bar[t]).sqrt() * noise
```
