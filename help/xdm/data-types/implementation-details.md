---
title: 实施详细信息数据类型
description: 本文档概述了实施详细信息体验数据模型(XDM)数据类型。
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 6%

---

# [!UICONTROL 实施详细信息] 数据类型

[!UICONTROL 实施详细信息] 是一种标准的Experience Data Model(XDM)数据类型，用于描述技术实施，如API或SDK。

![数据类型结构](../images/data-types/implementation-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `environment` | 字符串 | 实施的环境。 |
| `name` | 字符串 | SDK或端点的标识符。 所有SDK或端点都通过URI（包括扩展）进行标识。 |
| `version` | 字符串 | API或SDK的版本。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
