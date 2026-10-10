MobileGlues-plugin
====

> [!WARNING]
> 
> **This repository may contain unreleased Dev versions**
>
> If you are a regular user, **do not use these versions**, as they may cause **serious rendering issues**.  
> Please visit [MobileGlues-release](https://github.com/MobileGL-Dev/MobileGlues-release) to get the latest stable release.

Please see [MobileGlues](https://github.com/MobileGL-Dev/MobileGlues) and [MobileGlues-release](https://github.com/MobileGL-Dev/MobileGlues-release) to get more information.

License
====
MobileGlues is licensed under **GNU LGPL-2.1 License**.

Please see [LICENSE](https://github.com/MobileGL-Dev/MobileGlues-plugin/blob/main/LICENSE).

Third party components
====
For the components used by the renderer itself, please see [MobileGlues-release](https://github.com/MobileGL-Dev/MobileGlues-release).

The plugin application additionally uses:

**Miuix** by **compose-miuix-ui** - [Apache License 2.0](https://github.com/compose-miuix-ui/miuix/blob/main/LICENSE): [github](https://github.com/compose-miuix-ui/miuix)

**Jetpack Compose** by **Android Open Source Project (AOSP)** - [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt): [Android Developers](https://developer.android.com/jetpack/compose)

**AndroidX** by **Android Open Source Project (AOSP)** - [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt): [Android Developers](https://developer.android.com/jetpack/androidx)

**kotlinx.coroutines** by **JetBrains** - [Apache License 2.0](https://github.com/Kotlin/kotlinx.coroutines/blob/master/LICENSE.txt): [github](https://github.com/Kotlin/kotlinx.coroutines)

**Gson** by **Google** - [Apache License 2.0](https://github.com/google/gson/blob/main/LICENSE): [github](https://github.com/google/gson)

Check signature of your release
====
This portion is a guide to help you identify if your apk is an official release from
MobileGlues dev.

In your Android build-tools, find `apksigner`. Then run the following command:
```bash
apksigner verify --print-certs path/to/MobileGlues-plugin.apk
```

It should print out:
```bash
Signer #1 certificate DN: CN=MGDev, OU=MGDev, O=MGDev, L=Unknown, ST=Unknown, C=CN
Signer #1 certificate SHA-256 digest: 324f4efaff81632373dec9bc714a904b64740249410b551b61805340e42ff5d5
Signer #1 certificate SHA-1 digest: 615bc8b2741c24e7e5847b0c5c1d6816d5b0763a
Signer #1 certificate MD5 digest: 320ede9d22c709fe3792c804d5e00153
```

Check whether the `certificate DN` and `certificate digest` portion matches exactly like above.

In order that you may want to check against public key file, `pub.cer` and `pub.pem` are also provided.
You can use your utility as you like to check your apk against those files.

---

## MGCE Community Edition / MGCE 社区版

This repository is a community-maintained fork of MobileGlues, adding
experimental support for Minecraft 26.3+ on Mali GPUs.

本仓库为 MobileGlues 的社区维护分支，为 Mali GPU 设备增加对
Minecraft 26.3+ 的实验性支持。

### Credits / 署名

| Role / 角色 | Author / 作者 | Project / 项目 |
|---|---|---|
| Original renderer / 原渲染器核心 | @BZLZHH, @Swung0x48 | [MobileGlues](https://github.com/MobileGL-Dev/MobileGlues) |
| vkshim source / vkshim 源码 | FCL-Team | [FoldCraftLauncher](https://github.com/FCL-Team/FoldCraftLauncher) |
| CE integration / 社区版整合 | isaquxet08-ai | This repo / 本仓库 |

### Package Naming Convention / 包名命名规则

| Suffix / 后缀 | Package Name / 完整包名 | Stage / 阶段 |
|---|---|---|
| `.dbg` | `com.fcl.plugin.mobileglues.dbg` | Debug / 调试版 |
| `.ala` | `com.fcl.plugin.mobileglues.ala` | Alpha / 内测版 |
| `.bta` | `com.fcl.plugin.mobileglues.bta` | Beta / 公测版 |
| `.rese` | `com.fcl.plugin.mobileglues.rese` | Release / 正式版 |

**Different suffixes = different apps.** Uninstall old version before
installing a different stage.

**不同后缀 = 不同应用。** 切换阶段需先卸载旧版本。

### Icon Color Convention / 图标颜色规则

Each stage has a unique base color on the app icon.

每个阶段在图标底部有专属颜色。

| Stage / 阶段 | Color / 颜色 |
|---|---|
| Debug | 🔴 Red / 红色 |
| Alpha | 🟠 Orange / 橙色 |
| Beta | 🔵 Blue / 蓝色 |
| Release | 🟣 Magenta / 洋红 |

### License / 许可证

This project is released under **GNU LGPL-2.1**, consistent with the
upstream MobileGlues project.

本项目以 **GNU LGPL-2.1** 发布，与上游 MobileGlues 保持一致。

See `LICENSE` for details. / 详见 `LICENSE`。

---

## Known Issues / 已知问题

### Transparency rendering / 透明渲染

**Status: Partially broken / 部分异常**

27 shaders related to OIT (Order-Independent Transparency) fail to compile
on Mali GPUs. As a result, transparent blocks may render incorrectly or not
at all.

27 个与 OIT（顺序无关透明）相关的着色器在 Mali GPU 上编译失败。
因此透明方块可能渲染异常或完全不渲染。

**Affected / 受影响:**
- Water / 水
- Glass / 玻璃
- Ice / 冰
- Certain particles / 部分粒子效果

**Not affected / 不受影响:**
- Opaque terrain blocks (grass, stone, dirt, wood, etc.)
- 不透明地形方块（草地、石头、泥土、木头等）

**Root cause / 根因:**

GLES 3.2 requires fragment output array indices to be compile-time constants.
Minecraft 26.3's OIT shaders use dynamic indices, which GLES rejects. A fix
based on static index expansion is under development.

GLES 3.2 要求片元输出数组的索引必须是编译期常量。Minecraft 26.3 的 OIT
着色器使用了动态索引，被 GLES 拒绝。基于静态索引展开的修复正在开发中。

### Tested configuration / 已测试配置

- Device / 设备: Vivo PD2019 (V2002A)
- GPU: Mali-G76
- CPU: Exynos 880
- Android: 10
- FCL: 1.3.3.7
- Java: JRE 25

Other devices may behave differently. Reports are welcome.
其他设备表现可能不同，欢迎反馈。

---

## Requirements / 使用要求

Before launching Minecraft 26.3+ with this renderer:
使用本渲染器启动 Minecraft 26.3+ 前：

1. Set **OpenGL Error Setting** to **"Ignore shader/program/framebuffer error"**
2. 将 **OpenGL 报错设置** 设为 **"忽略 shader/program/framebuffer 报错"**

Without this setting, the game will crash on shader compile failure.
不设置此项，游戏会在着色器编译失败时崩溃。
