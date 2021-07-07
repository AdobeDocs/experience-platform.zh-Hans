---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;
solution: Experience Platform
title: 商务详细信息架构字段组
topic-legacy: overview
description: 本文档概述了“商务详细信息”架构字段组。
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL 商务详] 细信息架构字段组

>[!NOTE]
>
>The names of several schema field groups have changed. 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL 商务] 详细信息是类的标准架构字段 [[!DNL XDM ExperienceEvent] 组](../../classes/experienceevent.md)，用于描述商务数据，如产品信息（SKU、名称、数量）和标准购物车操作（订单、结账、放弃）。

![](../../images/field-groups/commerce-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `commerce` | [商务](../../data-types/commerce.md) | 描述产品退货、保修注册和购物车/订购流程的对象。 |
| `productListItems` | [产品列表项](../../data-types/product-list-item.md)的数组 | 代表客户选择的产品的项目列表，在特定时间点（可能与产品记录不同）提供特定选项和定价。 |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
