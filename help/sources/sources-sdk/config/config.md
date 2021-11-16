---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
title: 源SDK中的配置选项
topic-legacy: overview
description: 本文档概述了使用源SDK需要准备的配置。
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 1%

---

# 源SDK中的配置选项

>[!IMPORTANT]
>
>Sources SDK当前处于测试阶段，您的组织可能尚未访问该SDK。 本文档中描述的功能可能会发生更改。

本文档概述了使用源SDK需要准备的配置。

## 连接规范

连接规范返回源的连接器属性。 它们包括与创建基连接和源连接相关的验证规范，以及分配给特定源的固定连接规范ID。 连接规范与租户和IMS组织无关。 典型的连接规范包含有关给定源的基本信息以及三个不同的部分： `authSpec`, `sourceSpec`和 `exploreSpec`.

| 规格 | 描述 |
| --- | --- |
| `authSpec` | 的 `authSpec` 数组包含有关将源连接到平台所需的身份验证参数的信息。 任何给定的源都可以支持多种不同类型的身份验证。 |
| `sourceSpec` | 的 `sourceSpec` 数组包含与源有关的常规信息，包括有关在UI中呈现源所需属性的信息、文档链接以及有关分页、标题、正文和计划的参数。 此外， `sourceSpec` 描述从基本连接创建源连接所需参数的架构，创建源连接时需要此架构。 |
| `exploreSpec` | 的 `exploreSpec` 数组定义浏览和检查源中包含的对象所需的参数。 的 `exploreSpec` 还定义在探索和检查对象时返回的响应格式。 |

{style=&quot;table-layout:auto&quot;}

## 填充连接规范值

连接规范可分为三个不同的部分：验证规范、源规范和浏览规范。

有关如何填充连接规范每个部分的值的说明，请参阅以下文档：

* [配置身份验证规范](./authspec.md)
* [配置源规范](./sourcespec.md)
* [配置浏览规范](./explorespec.md)


