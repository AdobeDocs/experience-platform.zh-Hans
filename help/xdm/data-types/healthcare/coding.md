---
title: 编码数据类型
description: 了解编码体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 9%

---

# [!UICONTROL 正在编码]数据类型

[!UICONTROL 编码]是一种标准的体验数据模型(XDM)数据类型，它描述对术语系统定义的代码的引用。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![编码数据类型结构](../../images/data-types/healthcare/coding.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 代码] | `code` | 字符串 | 系统定义的语法中的符号。 |
| [!UICONTROL 显示区] | `display` | 字符串 | 由系统定义的表示。 |
| [!UICONTROL 系统] | `system` | 字符串 | 标识符值的命名空间，表示为URI。 |
| [!UICONTROL 由用户选择] | `userSelected` | 布尔值 | 此编码是否由用户选择的指示符。 默认值为false。 |
| [!UICONTROL 版本] | `version` | 字符串 | 系统的版本。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.schema.json)
