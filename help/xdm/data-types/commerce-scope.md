---
title: Commerce范围数据类型
description: 了解Commerce Scope Experience Data Model (XDM)数据类型。
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# [!UICONTROL Commerce作用域]数据类型

[!UICONTROL Commerce作用域]是一个标准的体验数据模型(XDM)数据类型，它定义了商业生态系统中发生事件的标识符。 它可以区分环境、网站、商店和商店视图。

![Commerce Scope数据类型的图表。](../images/data-types/commerce-scope.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL 环境ID] | `environmentID` | 字符串 | 环境ID 32位数的字母数字ID。 |
| [!UICONTROL 网站代码] | `websiteCode` | 字符串 | 环境中的唯一网站代码。 |
| [!UICONTROL 存储区代码] | `storeCode` | 字符串 | 网站中的唯一商店代码。 |
| [!UICONTROL 存储视图代码] | `storeViewCode` | 字符串 | 商店中的唯一商店视图代码。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
