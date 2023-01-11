---
solution: Experience Platform
title: 同意字符串数据类型
description: 本文档概述了同意字符串XDM数据类型。
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# [!UICONTROL 同意字符串] 数据类型

[!UICONTROL 同意字符串] 是一种标准XDM数据类型，用于描述表示客户同意的字符串值。 它包含上下文信息，例如同意字符串的标准(例如， [IAB透明度和同意框架(TCF)2.0](../field-groups/profile/iab.md))。

![](../images/data-types/consent-string.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `consentStandard` | 字符串 | 同意字符串的标准。 这有助于确定由同意管理服务设置的同意字符串的格式。 |
| `consentStandardVersion` | 字符串 | 同意标准的版本，用于准确定义由同意管理服务设置的同意字符串的格式。 |
| `consentStringValue` | 字符串 | 由同意管理服务提供的完全同意字符串。 `consentStandard` 和 `consentStandardVersion` 帮助定义如何解析此字符串。 |
| `containsPersonalData` | 布尔型 | 如果此字段为true，则表示需要处理此同意字符串以强制执行同意。 |
| `gdprApplies` | 布尔型 | 如果此字段为true，则表示个人数据中包含同意。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
