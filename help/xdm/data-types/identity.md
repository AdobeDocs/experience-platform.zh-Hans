---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；身份；数据类型；数据类型；
solution: Experience Platform
title: 身份数据类型
description: 了解Identity XDM数据类型。
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 4%

---

# [!UICONTROL 标识] 数据类型

[!UICONTROL 标识] 是一种标准XDM数据类型，用于明确区分与数字体验互动的人。 身份由身份提供者建立，身份提供者本身在中被引用。 `namespace` 属性。 在每个 `namespace`，则标识是唯一的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `namespace` | 对象 | 包含单个字符串字段(`code`)，它指示与提供的关联的命名空间 `id` 属性。 |
| `authenticatedState` | 字符串 | 观察到“体验事件”时此标识的身份验证状态。 请参阅 [附录](#authenticatedState) 以获取接受的值和定义。 |
| `id` | 字符串 | 消费者在相关命名空间中的身份。 |
| `primary` | 布尔值 | 指示这是否为个人的主要身份。 每个个人只能有一个主要身份。 |
| `xid` | 字符串 | 如果存在，则此值表示跨命名空间标识符，该标识符在所有命名空间中的所有命名空间范围内的标识符中是唯一的。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附录

以下部分包含有关 [!UICONTROL 标识] 数据类型。

## authenticatedState的接受值 {#authenticatedState}

下表概述了接受的值 `authenticatedState` 以及它们的相关含义：

| 值 | 描述 |
| --- | --- |
| `ambiguous` | 身份验证状态不明确。 |
| `authenticated` | 用户由观察事件时有效的登录或类似操作标识。 |
| `loggedOut` | 该用户在前某个时间点由登录操作识别，但在观察事件时未登录。 |
