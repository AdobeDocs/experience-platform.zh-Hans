---
title: 剂量数据类型
description: 了解剂量体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 56eda38b-a7f7-40da-af08-73cfe9db0c7e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 6%

---

# [!UICONTROL 剂量]数据类型

[!UICONTROL 剂量]是标准的体验数据模型(XDM)数据类型，用于描述药物服用或应该服用的方式。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![剂量数据类型结构](../../../images/healthcare/data-types/dosage/dosage.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 其他说明] | `additionalInstruction` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 对患者的补充说明或警告。 |
| 所需的 | `asNeededFor` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 描述根据需要服用药物时应该出现什么问题。 |
| [!UICONTROL 剂量和速率] | `doseAndRate` | 对象数组 | 给药量、给药量或典型给药量。 有关详细信息，请参阅下面的[部分](#dose-and-rate) |
| 每次管理[!UICONTROL 最大剂量] | `maxDosePerAdministration` | [[!UICONTROL 简单数量]](../data-types/simple-quantity.md) | 每次给药的药物上限。 |
| [!UICONTROL 每生命周期最大剂量] | `maxDosePerLifetime` | [[!UICONTROL 简单数量]](../data-types/simple-quantity.md) | 患者每生用药的上限。 |
| 每期[!UICONTROL 最大剂量] | `maxDosePerPeriod` | [[!UICONTROL 比率]](../data-types/ratio.md)的数组 | 每单位时间的药物上限。 |
| [!UICONTROL 方法] | `method` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 给药技术。 |
| [!UICONTROL 路由] | `route` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 药物应该如何进入体内。 |
| [!UICONTROL 正文站点] | `site` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 给药的身体部位。 |
| [!UICONTROL 计时] | `timing` | [[!UICONTROL 计时]](../data-types/timing.md) | 何时该用药。 |
| [!UICONTROL 根据需要] | `asNeeded` | 布尔值 | 指示是否应该根据需要服用药物。 |
| [!UICONTROL 患者说明] | `patientInstruction` | 字符串 | 患者或消费者理解的用语。 |
| [!UICONTROL 序列] | `Integer` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 剂量说明的顺序。 |
| [!UICONTROL 文本] | `text` | 字符串 | 计划文本剂量说明。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.schema.json)

## `doseAndRate` {#dose-and-rate}

`doseAndRate`作为对象数组提供。 每个对象的结构如下所述。

![剂量和速率结构](../../../images/healthcare/data-types/dosage/dose-and-rate.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 剂量数量] | `doseQuantity` | [[!UICONTROL 简单数量]](../data-types/simple-quantity.md) | 每剂药物的量。 |
| [!UICONTROL 剂量范围] | `doseRange` | [[!UICONTROL Range]](../data-types/range.md) | 每剂药物的量。 |
| [!UICONTROL 费率数量] | `rateQuantity` | [[!UICONTROL 简单数量]](../data-types/simple-quantity.md) | 每单位时间的药物量。 |
| [!UICONTROL 费率范围] | `rateRange` | [[!UICONTROL Range]](../data-types/range.md) | 每单位时间的药物量。 |
| [!UICONTROL 比率比率] | `rateRatio` | [[!UICONTROL 比率]](../data-types/ratio.md) | 每单位时间的药物量。 |
| [!UICONTROL 类型] | `type` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 指定的剂量或剂量率。 |
