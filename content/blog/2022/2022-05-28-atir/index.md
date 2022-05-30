+++
title = "ATIR / 一个学习向游戏引擎"
description = "名字源于某次经典typo (original: ATRI)"
draft = false

[taxonomies]
tags = ["Game development", "Rhythm Game", "Game Engine"]

[extra]
feature_image = "IMG_20220528_221059.jpg"
feature = true
link = "" 
+++

### 本文主要记录立项调研内容，决定最终方向的各种考虑

#### 该项目旨在学习，完善过程中可能会出现巨大结构变动或者风格差异

### 需求

2D 轻量引擎

多线程

可视化 Editor

ECS 架构 （Entity Component System）

### 大纲

![ATIR Draft](ATIR.png)
图中只展示了部分系统，实际复杂度可能远不止此，仅做讲解设计思路参考

（注，第三方内容并不是实际技术选型，只是为了展示该层宏观定位）

首先我会问自己游戏引擎是什么以及我想要什么。

游戏引擎提供一个提供一系列工具、核心框架，使开发人员无需重复构建基础设施，甚至忽略平台差异进行高效的制作。

在曾经，游戏和引擎的划分界线往往非常模糊。
早期受限于硬件性能以及兼容性，引擎通常只满足游戏设计最低限度的功能实现。那时的引擎不能算是通用引擎。

现如今各种引擎Unreal，Unity，Godot都将通用性表现得淋漓尽致。
我可以只使用 2D 场景来构建一个2D卡牌游戏。接着可以加入 3D 场景，现在我甚至能够在一个 3D 游戏中与朋友一起游玩我的上一个卡牌游戏。its cool

但付出的代价是什么呢

越是追求通用性，就意味着接受更多妥协来兼容各种应用场景。为了解决这样的问题已经有了不少解决方案，特定的渲染管线就是其中一种（通常游戏引擎都会自带一套默认渲染管线，根据自身开发方向以及美术需求对其进行定制往往能获得事半功倍的效果）

可以说，游戏引擎越通用，在特定平台上的性能就越一般。

现在我大概能明确我的目标，我想要一个针对 2D画面延迟敏感场景的游戏引擎。而她最合适的应用场景正是音游。

#### 功能

接下来我会按照大纲图内的模块开始陈述

##### 游戏流程

游戏往往伴随着目标，为了达到目标而设定的规则集（**Rulesets**）我在这里将其称为游戏流程。考虑到开发调试、热更新等需求，用原生代码编写规则集不是好主意。大部分游戏引擎会内置另一种脚本语言用于解释需要灵活性的组件。

那么我们需要为脚本开发一系列规则，使其满足大部分场景需求

示例（可能会变动）

```lua
require "atir"

local World = atir.get_world()
local SplashScreenEntity = atir.get_entity_by_uuid(uuid) -- we can do something on entity later

local function _on_startup()
    print("Loaded") -- when this script loaded
end

local function _on_update(delta)
    print(string.format("Time elapsed: %s", delta)) -- call every frame
end

local on_dispose()
    print("Disposed") -- when this script dispose
end

function singal_tx()
    atir.emit_singal(uuid)
end

function singal_rx(uuid)
    print("got singal")
end
```

同上述，虽然这里使用了lua写法，但依旧不代表最终选型
