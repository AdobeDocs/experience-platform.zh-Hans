---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；
solution: Experience Platform
title: 商务详细信息架构字段组
description: 了解商务详细信息架构字段组。
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# [!UICONTROL 商业详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 查看文档 [字段组名称更新](../name-updates.md) 以了解更多信息。

[!UICONTROL 商业详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)，用于描述商业数据，如产品信息（SKU、名称、数量）和标准购物车操作（订单、结账、放弃）。

![](../../images/field-groups/commerce-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | 描述产品退货、保修登记和购物车/订单流程的对象。 |
| `productListItems` | 数组 [产品列表项](../../data-types/product-list-item.md) | 代表客户选择的产品的项目列表，具有特定选项并在特定时间定价（可能与产品记录不同）。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
