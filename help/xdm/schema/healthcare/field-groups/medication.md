---
title: 药物架构字段组
description: 了解药物架构字段组。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1f53ff8-3079-4b2f-9e73-31a773907a63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 6%

---

# [!UICONTROL 药物]架构字段组

[!UICONTROL 药物]是[[!DNL Medication] 类](../../../classes/medication.md)的标准架构字段组。 它提供捕获药物信息的单个对象类型字段`healthcareMedication`。

![字段组结构](../../../images/healthcare/field-groups/medication/medication.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| ---|  --- | --- | --- |
| [!UICONTROL 批次] | `batch` | 对象 | 包装药物的详细信息。 包含两个属性： <li>`lotNumber`：分配给批次的标识符的字符串值。</li> <li>`expirationDate`：批次到期时的DateTime值。</li> |
| [!UICONTROL 代码] | `code` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 标识此药物的代码。 |
| [!UICONTROL 定义] | `definition` | [[!UICONTROL 引用]](../data-types/reference.md) | 药物的定义。 |
| [!UICONTROL 剂量表] | `doseForm` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 描述药物的剂型，如片剂或胶囊。 |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../data-types/identifier.md)的数组 | 药物的标识符。 |
| [!UICONTROL 配料] | `ingredient` | 对象数组 | 描述药物的配料信息。 有关详细信息，请参阅下面[&#128279;](#ingredient)的部分。 |
| [!UICONTROL 营销授权持有者] | `marketingAuthorizationHolder` | [[!UICONTROL 引用]](../data-types/reference.md) | 有权营销药物的组织。 |
| 总容量 | `totalVolume` | [[!UICONTROL 数量]](../data-types/quantity.md) | 当产品代码未推断包装尺寸时，药物中提供的产品量。 |
| [!UICONTROL 状态] | `status` | 字符串 | 药物状态。 此属性的值必须等于以下已知枚举值之一。 <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> |

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.schema.json)

## `ingredient` {#ingredient}

`ingredient`作为对象数组提供。 每个对象的结构如下所述。

![成分结构](../../../images/healthcare/field-groups/medication/ingredient.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 项目] | `item` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md) | 所描述的配料。 |
| [!UICONTROL 强度可编码概念] | `strengthCodeableConcept` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 现有配料的数量，以系统定义的术语表示。 |
| [!UICONTROL 强度数量] | `strengthQuantity` | [[!UICONTROL 数量]](../data-types/quantity.md) | 存在的配料数量。 |
| [!UICONTROL 强度比] | `strengthRatio` | [[!UICONTROL 比率]](../data-types/ratio.md) | 所含成分的比例。 |
| [!UICONTROL 处于活动状态] | `isActive` | 布尔值 | 指示配料是否有效。 |
