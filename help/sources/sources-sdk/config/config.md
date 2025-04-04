---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源sdk；sdk；SDK
title: 自助源(批处理SDK)中的配置选项
description: 本文档概述了为使用自助源(批处理SDK)而需要准备的配置。
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# 自助源(批处理SDK)中的配置选项

本文档概述了为使用自助源(批处理SDK)而需要准备的配置。

## 连接规范

连接规范返回源的连接器属性。 它们包括与创建基础连接和源连接相关的身份验证规范，以及分配给特定源的固定连接规范ID。 连接规范与租户和组织无关。 典型的连接规范包含有关给定源的基本信息以及三个不同的部分： `authSpec`、`sourceSpec`和`exploreSpec`。

| 规范 | 描述 |
| --- | --- |
| `authSpec` | `authSpec`数组包含有关将源连接到Experience Platform所需的身份验证参数的信息。 任何给定的源都可以支持多种不同类型的身份验证。 |
| `sourceSpec` | `sourceSpec`数组包含与源相关的一般信息，包括在UI中显示源所需的属性信息、文档链接，以及有关分页、标题、正文和计划的参数。 此外，`sourceSpec`还描述了从基本连接创建源连接所需的参数的架构，这是创建源连接所必需的。 |
| `exploreSpec` | `exploreSpec`数组定义浏览和检查源中包含的对象所需的参数。 `exploreSpec`还定义了探索和检查对象时返回的响应格式。 |

{style="table-layout:auto"}

## 填充连接规范值

连接规范可以分为三个不同的部分：身份验证规范、源规范以及探索规范。

有关如何填充连接规范每个部分的值的说明，请参阅以下文档：

* [配置您的身份验证规范](./authspec.md)
* [配置源规范](./sourcespec.md)
* [配置浏览规范](./explorespec.md)
