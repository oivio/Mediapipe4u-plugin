---
layout: default
nav_order: 1
title: 环境要求
parent: 安装和配置
---

# 环境要求   

*请仔细阅读以下章节，确认你的环境是否满足 **MediaPipe4U** 要求。*


## 环境要求

|软件|版本|
|--------|--------------|
|操作系统|Windows10/11 x64|
|Unreal Engine |5.0.x, 5.1.x|
|Visual Studio 2022 | 17.5 or later|
|Windows SDK|10.0.22621 or later|
|Visual C++ Redistributable|14.35 or later|

{: .warning}
> **MediaPipe4U** 不支持移动平台（手机端）和 Mac 平台。   
> **MediaPipe4U** 不支 x86 平台。

|硬件|版本|
|--------|--------------|
| 磁盘空间 | 开发：5G, 部署：200M|

{: .important}
> 插件由于采用预编译，包含大量 C++ 链接符号和调试符号，解压后会占用 **5G** 磁盘空间（大部分为 Intermediate 中的 UE 生成代码）
> 
> 你不需要担心磁盘占用问题，这只是开发期间的磁盘占用，在项目打包后，插件磁盘占用大约是 **200M**（主要为 GStreamer 动态库）


## 模型要求

### 骨骼

模型需要满足最小人形骨骼定义，定义如下：

[![骨骼示意图](images/avatar_bones.jpg "Shiprock")](images/avatar_bones.jpg)


图片中骨骼颜色标记说明：

- 红色: 必须提供，否则无法正常工作
- 黄色: 建议提供，否则影响部分功能
- 灰色：可以不提供，后续版本可能会使用
- 未标记：可以不提供（长期不会使用）


骨骼结构注意事项：

1. 除脊柱（Spine）和盆骨（Hips）外，骨骼必须具有正确的父子关系（父骨骼旋转能供移动子骨骼)，例如：LeftHand 必须是 LeftLowerArm 的直接子骨骼。 
2. 手掌部分骨骼必须全部提供，每根手指需要三根骨骼
3. 其他多余的骨骼不影响功能
4. 脊柱（Spine）可以是任意数量，但是盆骨（Hips）必须是他的祖先，脊柱(Spine)和盆骨（Hips）不要求直接父子关系，你可以使用任意一根脊柱骨骼来控制腰身的旋转

### 初始POSE

MediaPipe4U 适应任意的角色模型的初始 POSE （例如可以是 T-POSE，也可以是 A-POSE）, 但是角色必须面朝向 **Y** 轴正方向。

**但是**，如果你使用运行时重定向功能，原始骨骼和目标骨骼必须具有相同的骨骼结构（包括层级关系和各个骨骼的转轴朝向），也要求必须使用相同的 POSE 类型。


## 动画蓝图

使用 **MediaPipe4U** 的动补功能，你的动画蓝图必须使用插件中的 **MediaPipeAnimInstance** 作为基类。

## 面部驱动（实验性）

可以不依赖 Iphone 设备，仅使用普通摄像头来驱动角色的 BlendShape，并且完全兼容 LiveLink 协议，使用它就像和使用 Iphone Arkit 捕捉表情完全一样。 

{: .important}
> 这是一个实验性功能，驱动的表情数量有限，并且对摄像头角度、光线等要求苛刻，不建议写实风格的角色使用。

面部驱动兼容苹果 Arkit 表情，你的 MorphTarget 名称必须满足苹果命名规范，当然你可以通过 RetargetAsset 来适应任意的名称。

---

