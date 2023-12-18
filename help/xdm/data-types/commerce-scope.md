---
title: 商务范围数据类型
description: 了解Commerce Scope Experience Data Model (XDM)数据类型。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 6%

---

# [!UICONTROL 商业范围] 数据类型

[!UICONTROL 商业范围] 是一种标准体验数据模型(XDM)数据类型，它定义事件在商业生态系统中发生的位置的标识符。 它可以区分环境、网站、商店和商店视图。

![商务范围数据类型的图表。](../images/data-types/commerce-scope.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL 环境ID] | `environmentID` | 字符串 | 环境ID 32位数的字母数字ID。 |
| [!UICONTROL 网站代码] | `websiteCode` | 字符串 | 环境中的唯一网站代码。 |
| [!UICONTROL 商店代码] | `storeCode` | 字符串 | 网站中的唯一商店代码。 |
| [!UICONTROL 存储视图代码] | `storeViewCode` | 字符串 | 商店中的唯一商店视图代码。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
