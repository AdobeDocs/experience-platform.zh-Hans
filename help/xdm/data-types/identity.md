---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；身份；数据类型；数据类型；
solution: Experience Platform
title: 身份数据类型
description: 本文档概述了Identity XDM数据类型。
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 4%

---

# [!UICONTROL 身份] 数据类型

[!UICONTROL 身份] 是一种标准的XDM数据类型，用于明确区分与数字体验进行交互的人员。 身份由身份提供者建立，该提供者本身在 `namespace` 属性。 在每个 `namespace`，则标识是唯一的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `namespace` | 对象 | 包含单个字符串字段(`code`)，指示与提供的 `id` 属性。 |
| `authenticatedState` | 字符串 | 观察到的体验事件时此身份的已验证状态。 请参阅 [附录](#authenticatedState) 以了解接受的值和定义。 |
| `id` | 字符串 | 相关命名空间中消费者的标识。 |
| `primary` | 布尔型 | 指示这是否是个人的主标识。 每个人只能有一个主标识。 |
| `xid` | 字符串 | 如果存在，则此值表示跨命名空间标识符，该标识符在所有命名空间中所有命名空间范围内的标识符都是唯一的。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附录

以下部分包含有关 [!UICONTROL 身份] 数据类型。

## 已接受的authenticatedState值 {#authenticatedState}

下表概述了 `authenticatedState` 及其相关含义：

| 值 | 描述 |
| --- | --- |
| `ambiguous` | 身份验证状态不明确。 |
| `authenticated` | 用户是通过在事件观察时有效的登录或类似操作来识别的。 |
| `loggedOut` | 用户是在以前某个时间点通过登录操作识别的，但在事件观察时未登录。 |
