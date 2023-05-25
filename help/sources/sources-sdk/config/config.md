---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK；SDK
title: 自助源中的配置选项(Batch SDK)
description: 本文档概述了要使用自助源(Batch SDK)需要准备的配置。
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 自助源中的配置选项(Batch SDK)

本文档概述了要使用自助源(Batch SDK)需要准备的配置。

## 连接规范

连接规范返回源的连接器属性。 它们包括与创建基本连接和源连接相关的身份验证规范，以及分配给特定源的固定连接规范ID。 连接规范与租户和组织无关。 典型的连接规范包含有关给定源的基本信息，以及三个不同的部分： `authSpec`， `sourceSpec`、和 `exploreSpec`.

| 规格 | 描述 |
| --- | --- |
| `authSpec` | 此 `authSpec` 数组包含有关将源连接到Platform所需的身份验证参数的信息。 任何给定源都可以支持多种不同类型的身份验证。 |
| `sourceSpec` | 此 `sourceSpec` 数组包含与源相关的一般信息，其中包括在UI中显示源所需的属性信息、文档链接，以及有关分页、标题、正文和调度的参数。 此外， `sourceSpec` 描述从基本连接创建源连接所需的参数的架构，在创建源连接时需要用到这些参数。 |
| `exploreSpec` | 此 `exploreSpec` 数组定义浏览和检查源中包含的对象所需的参数。 此 `exploreSpec` 还定义了探索和检查对象时返回的响应格式。 |

{style="table-layout:auto"}

## 填充连接规范值

连接规范可以分为三个不同的部分：身份验证规范、源规范和浏览规范。

有关如何填充连接规范每个部分的值的说明，请参阅以下文档：

* [配置身份验证规范](./authspec.md)
* [配置源规范](./sourcespec.md)
* [配置浏览规范](./explorespec.md)
