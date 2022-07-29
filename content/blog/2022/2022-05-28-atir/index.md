+++
title = "ATIR / 一个学习向游戏引擎"
description = ""
draft = false

[taxonomies]
tags = ["Game development", "Rhythm Game", "Game Engine"]

[extra]
feature_image = "IMG_20220528_221059.jpg"
feature = true
link = "" 
+++

本文主要记录立项调研内容，决定最终方向的各种考虑

该项目旨在学习，完善过程中可能会出现巨大结构变动或者风格差异

## 需求

多线程

可视化 Editor

ECS 架构 （Entity Component System）

## 大纲

![ATIR Draft](ATIR.png)
图中只展示了部分系统，实际复杂度可能远不止此，仅做讲解设计思路参考

（注，第三方内容并不是实际技术选型，只是为了展示该层宏观定位）

首先我会问自己游戏引擎是什么以及我想要什么。

游戏引擎提供一个提供一系列工具、核心框架，使开发人员无需重复构建基础设施，甚至忽略平台差异进行高效的制作。

在曾经，游戏和引擎的划分界线往往非常模糊。
早期受限于硬件性能以及兼容性，引擎通常只满足游戏设计最低限度的功能实现。那时的引擎不能算是通用引擎。

现如今各种引擎Unreal，Unity，Godot都试图为用户提供尽可能多的通用性。

但付出的代价是什么呢

越是追求通用性，就意味着接受更多妥协来兼容各种应用场景。可以说，游戏引擎越通用，在特定平台上的性能就越一般。

而我明确我的目标为针对 2D画面延迟敏感场景。合适的应用场景包括音游等高度依赖用户反应能力的游戏。

### 游戏流程

游戏往往伴随着目标，为了达到目标而设定的规则集（**Rulesets**）我在这里将其称为游戏流程。考虑到开发调试、热更新等需求，用原生代码编写规则集不是好主意。大部分游戏引擎会内置另一种脚本语言用于解释需要灵活性的组件。

示例

```python

func startup():
    do_something()
    pass

func update():
    update_components()
    pass

func singal_rx():
    do_someting()
    pass

func final():
    dispose_resources()
    pass

```



### ECS

Entity - Component - System

ECS解决了OOP模式下GameObject过多造成的耦合难以维护，

