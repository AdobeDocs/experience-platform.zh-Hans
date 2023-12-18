---
title: 实施详细信息数据类型
description: 了解实施详细信息Experience Data Model (XDM)数据类型。
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 6%

---

# [!UICONTROL 实施详细信息] 数据类型

[!UICONTROL 实施详细信息] 是一个标准体验数据模型(XDM)数据类型，用于描述技术实施，如API或SDK。

![数据类型结构](../images/data-types/implementation-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `environment` | 字符串 | 实施的环境。 |
| `name` | 字符串 | SDK或端点的标识符。 所有SDK或端点均通过URI进行标识，包括扩展。 |
| `version` | 字符串 | API或SDK的版本。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
