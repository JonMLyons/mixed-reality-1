---
title: OpenXR performance
description: Debug the GPU performance of your OpenXR applications.
author: thetuvix
ms.author: alexturn
ms.date: 2/28/2020
ms.topic: article
keywords: OpenXR, Khronos, BasicXRApp, DirectX, native, native app, custom engine, middleware, performance, optimization, GPU debugging, RenderDoc, PIX
---



# OpenXR performance

On HoloLens 2, there are a number of ways to submit composition data through `xrEndFrame` which will result in post-processing that will have a noticeable performance penalty.
To avoid performance penalities, [submit a single `XrCompositionProjectionLayer`](openxr-best-practices.md#use-a-single-projection-layer) with the following characteristics:
* [Use a texture array swapchain](openxr-best-practices.md#render-with-texture-array-and-vprt)
* [Use the primary color swapchain format](openxr-best-practices.md#select-a-swapchain-format)
* [Use the recommended view dimensions](openxr-best-practices.md#render-with-recommended-rendering-parameters-and-frame-timing)
* Do not set the `XR_COMPOSITION_LAYER_UNPREMULTIPLIED_ALPHA_BIT` flag
* Set the `XrCompositionLayerDepthInfoKHR` `minDepth` to 0.0f and `maxDepth` to 1.0f

Additional considerations will result in better performance:
* [Use the 16-bit depth format](openxr-best-practices.md#choose-a-reasonable-depth-range)
* [Make instanced draw calls](openxr-best-practices.md#render-with-texture-array-and-vprt)

## Graphics debugging

You can debug the GPU performance of your OpenXR applications using <a href="https://renderdoc.org/" target="_blank">RenderDoc</a>:
* For debugging **Win32 OpenXR applications** for immersive desktop headsets, the <a href="https://renderdoc.org/" target="_blank">mainline version of RenderDoc</a> should work as is.
* For debugging **UWP OpenXR applications** on HoloLens 2, you can use a <a href="https://github.com/brycehutchings/renderdoc" target="_blank">UWP fork of RenderDoc</a>.

PIX support for OpenXR applications is coming soon.
