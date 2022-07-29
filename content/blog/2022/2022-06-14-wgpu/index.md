+++
title = "wgpu学习记录1"
description = ""
draft = true

[taxonomies]
tags = ["Game development", "Game Engine"]

[extra]
feature_image = "logo.png"
feature = true
link = "" 
+++

## wgpu?

wgpu是一个跨平台，基于Rust编写的 WebGPU 实现。原生支持了 Vulkan, Metal, D3D12, D3D11, OpenGLES 主流图形API。我决定选用它作为我项目的GPU base。

| API    | Windows         | Linux & Android | MacOS & IOS |
| ------ | --------------- | --------------- | ----------- |
| Vulkan | ✅               | ✅               | 🆗           |
| Metal  | N/A             | N/A             | ✅           |
| DX12   | ✅ (Win10+ only) | N/A             | N/A         |
| DX11   | ❌ (WIP)         | N/A             | N/A         |
| GLES3  | ❌               | 🆗               | ❌           |
| Angle  | 🆗               | 🆗               | 🆗           |

✅ = Full support   🆗 = Basically support  ❌ = Unsupported

### wgpu shader

wgpu 支持 [WGSL](https://gpuweb.github.io/gpuweb/wgsl/), SPIR-V, GLSL 三种 shader 语言，得益于 [HLSL](https://github.com/Microsoft/DirectXShaderCompiler) 和 [GLSL](https://github.com/KhronosGroup/glslang) 都能被转译为 SPIR-V，这些 shader 能在不同后端中通用。

## Get Started