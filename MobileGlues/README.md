“# MobileGlues

**MobileGlues**, which stands for "(on) Mobile, GL uses ES", is a GL implementation running on top of host OpenGL ES 3.x (best on 3.2, minimum 3.0), with running Minecraft: Java Edition in mind.

# For Shader Developers

1. MobileGlues automatically:
   - Converts desktop GLSL → GLSL ES
   - Removes `layout(binding)` syntax
   - Handles version directives
   - Always declare precision explicitly:
     ```glsl
     precision highp float;
     precision highp int;
     ```

2. MobileGlues (since V1.2.6) injects these macros into your shaders:
   ```glsl
   #define MG_MOBILEGLUES                   // Indicates MobileGlues environment
   #define MG_MOBILEGLUES_VERSION 1260      // Version number (e.g. 1260 = V1.2.6)
   ```

   Use these macros for platform-specific logic:
   ```glsl
   #ifdef MG_MOBILEGLUES
       #if MG_MOBILEGLUES_VERSION >= 1270
           // Logic for MobileGlues (version >= V1.2.7)
       #else
           // Logic for MobileGlues (version < V1.2.7)
       #endif
   #else
       // ...
   #endif
   ```

3. If encountering issues:
   - Enable `Ignore shader/program error`, and check the logs (located at `/sdcard/MG/latest.log`).

# License

MobileGlues is licensed under **GNU LGPL-2.1 License**.

Please see [LICENSE](https://github.com/MobileGL-Dev/MobileGlues/blob/main/LICENSE).

# Third-party components

**SPIRV-Cross** by **KhronosGroup** - [Apache License 2.0](https://github.com/KhronosGroup/SPIRV-Cross/blob/master/LICENSE): [github](https://github.com/KhronosGroup/SPIRV-Cross)

**glslang** by **KhronosGroup** - [Various Licenses](https://github.com/KhronosGroup/glslang/blob/main/LICENSE.txt): [github](https://github.com/KhronosGroup/glslang)

**cJSON** by **DaveGamble** - [MIT License](https://github.com/DaveGamble/cJSON/blob/master/LICENSE): [github](https://github.com/DaveGamble/cJSON)

**FidelityFX-FSR** by **AMD** - [MIT License](https://github.com/GPUOpen-Effects/FidelityFX-FSR/blob/master/license.txt): [github](https://github.com/GPUOpen-Effects/FidelityFX-FSR) 

**Perfetto** by **Google** - [Apache License 2.0](https://github.com/google/perfetto/blob/main/LICENSE): [github](https://github.com/google/perfetto)

**xxHash** by **Yann Collet** - [BSD 2-Clause License](https://github.com/Cyan4973/xxHash/blob/dev/LICENSE): [github](https://github.com/Cyan4973/xxHash)

**flat_hash_map** by **Malte Skarupke** - [Boost Software License 1.0](https://github.com/MobileGL-Dev/flat_hash_map/blob/master/LICENSE): [github](https://github.com/MobileGL-Dev/flat_hash_map) (fork of [skarupke/flat_hash_map](https://github.com/skarupke/flat_hash_map), carrying a fix that lets the header be included on 32-bit targets)
# MobileGlues CE (Community Edition)

MobileGlues 的社区维护版本，由社区开发者维护，非官方版本。

## 这是什么

[MobileGlues](https://github.com/MobileGL-Dev/MobileGlues) 是一个
在 Android 上运行 OpenGL 4.0 的实现，主要用于在手机上运行
Minecraft Java 版。

本仓库是 MobileGlues 的**社区维护分支**，主要目标：

- 为 Mali GPU 设备提供 MC 26.3+ 的兼容性支持
- 集成 FCL 的 vkshim 层，绕过 Vulkan 版本检查
- 探索旧 GPU 设备运行新版 MC 的可能性

**本版本不是官方版本，所有核心渲染逻辑版权归 MobileGlues 原作者所有。**

## 与官方版的区别

| 项目 | 官方版 | 本社区版 |
|---|---|---|
| MC 26.3 支持 | 有限 | 集成 vkshim 优化 |
| Mali GPU 适配 | 通用 | 针对性优化 |
| 维护者 | MobileGL-Dev | isaquxet08 |
| 稳定性 | 官方保证 | 实验性 |

## 署名

- **原项目**：MobileGlues (MobileGL-Dev)
- **原作者**：@BZLZHH、@Swung0x48
- **vkshim 源码**：FCL-Team
- **本社区版维护**：isaquxet08

## 许可证

- MobileGlues 核心：GNU LGPL-2.1
- vkshim 集成部分：GNU GPL-3.0
- 本仓库修改：与上游保持一致
