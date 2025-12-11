---
title: Home
layout: home
---
{: .hightlight}
>Motivation:  
>Many images captured at night or in dim indoor environments are extremely dark. Important regions such as faces, hands, roads, and objects become very difficult to see, which hurts both human perception and downstream vision algorithms. Naïvely brightening these images tends to amplify sensor noise and produce overexposed, unnatural results. To address this, I build on the Retinex assumption that an observed image can be decomposed into reflectance (intrinsic scene structure) and illumination (lighting). In particular, I adopt the weighted variational Retinex model proposed by Fu et al., which is designed to better preserve fine details while correcting low-light illumination.



The Approach:

![Retinex_formula](./imgs/Retinex_formular.png)

According to Retinex assumption, the image can be separated into reflectance and illumination. The core insight of the weighted variational Retinex model is to estimate reflectance and illumination from the source image, gamma correct the derived illumination, and conduct dot product of the corrected illumination with the reflectance to enhance image lighting/illumination.

![2](./imgs/2.png)

The objective function has two assumptions:

1: Illumination is smooth (Simple Lighting condition).

2: Reflectance changes sharply (Different objects tend to have discrete reflectance).

Given those two assumptions, the illumination term is penalized by L2 norm to enforce spatial smoothness, and the reflectance is penalized by L1 norm to enforce spatial smoothness.

The fidelity term penalizes the difference of the restored image and the original image.

All terms are in log-domain so S=L⋅R in Retinex assumption can be transformed into s=l+r which, which allows the fidelity term to be convex for convenience to solve.

However, the objective function (2) is not convex giving the multiplication inside L1 norm and L2 norm. For convenience to solve, Fu et al. proposes an iterative method to approach the objective function (2):

![Model](./imgs/model.png)

To clarify a Q&A question during my presentation, the minimization problem with objective (3) does have a global minimum and it is a convex problem since we can consider r ^ (k-1) and l ^ (k-1) as constants. Moreover, the original problem with objective function (2) is not convex and is hard to tell whether a global minimum exists.

TO SOLVE this objective function, Fu et al. proposes to use ADMM, and the augmented Lagrangian (the dual problem) is constructed as the following:

![Lagrangian](./imgs/lagrangian.png)

According to ADMM theory, solving this Lagrangian is equivalent to solving the original objective function.


----

[Retinex_formula]: ./imgs/Retinex_formular.png
[Model]: ./imgs/model.png
[Lagrangian]: ./imgs/lagrangian.png
[2]: ./imgs/2.png
