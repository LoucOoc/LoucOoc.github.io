---
title: Home
layout: home
---
{: .hightlight}
>Motivation:  
>Many images captured at night or in dim indoor environments are extremely dark. Important regions such as faces, hands, roads, and objects become very difficult to see, which hurts both human perception and downstream vision algorithms. Naïvely brightening these images tends to amplify sensor noise and produce overexposed, unnatural results. To address this, I build on the Retinex assumption that an observed image can be decomposed into reflectance (intrinsic scene structure) and illumination (lighting). In particular, I adopt the weighted variational Retinex model proposed by Fu et al., which is designed to better preserve fine details while correcting low-light illumination.



The Approach:
[Retinex_formular]
According to Retinex assumption, the image can be seperated into reflectance and illumination. The core insight of the weighted variational Retinex model is to estimate reflectance and illumination from the source image, gamma correct the derived illumination, and conduct dot product of the corrected illumination with the reflectance to enhance image lighting/illumination.
[Model]
The objective function have two assumption:
1: Illumination is smooth (Simple Lighting condition).
2: Reflectance changes sharply (Different objects tend to have discrete reflectance).
Follwing these two assumption, the illumination term is penalized by L2 norm to enforce spatial smoothness, and the reflectance is penalized by L1 norm to enforce spatial smoothness.
The fidelity term penalized the difference of the restored image and the origional image.
All term are in log-domain so S=L⋅R in Retinex assumption can be transformed into s=l+r which, which allows the fidelity term to be convex for convenience to solve.




This is a *bare-minimum* template to create a Jekyll site that uses the [Just the Docs] theme. You can easily set the created site to be published on [GitHub Pages] – the [README] file explains how to do that, along with other details.

If [Jekyll] is installed on your computer, you can also build and preview the created site *locally*. This lets you test changes before committing them, and avoids waiting for GitHub Pages.[^1] And you will be able to deploy your local build to a different platform than GitHub Pages.

More specifically, the created site:

- uses a gem-based approach, i.e. uses a `Gemfile` and loads the `just-the-docs` gem
- uses the [GitHub Pages / Actions workflow] to build and publish the site on GitHub Pages

Other than that, you're free to customize sites that you create with this template, however you like. You can easily change the versions of `just-the-docs` and Jekyll it uses, as well as adding further plugins.

[Browse our documentation][Just the Docs] to learn more about how to use this theme.

To get started with creating a site, simply:

1. click "[use this template]" to create a GitHub repository
2. go to Settings > Pages > Build and deployment > Source, and select GitHub Actions

If you want to maintain your docs in the `docs` directory of an existing project repo, see [Hosting your docs from an existing project repo](https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md#hosting-your-docs-from-an-existing-project-repo) in the template README.

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).

[Just the Docs]: https://just-the-docs.github.io/just-the-docs/
[GitHub Pages]: https://docs.github.com/en/pages
[README]: https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md
[Jekyll]: https://jekyllrb.com
[GitHub Pages / Actions workflow]: https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/
[use this template]: https://github.com/just-the-docs/just-the-docs-template/generate
[Retinex_formular]: ./imgs/Retinex_formular.png
[Model]: ./imgs/model.png
