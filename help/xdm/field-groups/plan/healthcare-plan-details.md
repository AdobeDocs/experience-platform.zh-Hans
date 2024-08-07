---
title: 医疗保健计划详细信息架构字段组
description: 了解医疗保健计划详细信息架构字段组。
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---

# [!UICONTROL 医疗保健计划详细信息]架构字段组

[!UICONTROL 医疗保健计划详细信息]是[[!UICONTROL 计划]类](../../classes/plan.md)的标准架构字段组。 它提供单个对象类型字段`healthcarePlanDetails`，该字段捕获与医疗计划相关的属性。

![](../../images/field-groups/plan/healthcare-plan-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `networkDetails` | 对象数组 | 列出受益人可能寻求治疗的保险公司定义的医疗提供商网络的详细信息，并将按“网络内”费率承保。 每个对象都包含以下属性： <ul><li>`networkID`： （字符串）网络的保险公司特定ID。</li><li>`networkName`： （字符串）网络的特定于保险商的名称。</li></ul> |
| `affiliations` | 字符串数组 | 与计划关联的商业实体列表。 |
| `coverageType` | 字符串 | 计划保险范围类型。 接受的值包括：<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | 布尔值 | 指示计划是否处于活动状态。 |
| `lastVerificationDate` | 日期时间 | 上次验证计划的日期。 |
| `payerID` | 字符串 | 付款人（即计划的保险提供商）的唯一标识符。 |
| `planLevel` | 字符串 | 指示计划级别。 接受的值包括：<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | 字符串 | 指示规划类型。 接受的值包括：<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | 字符串 | 计划的所有者的类型。 示例包括个人、组、组织等。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅[公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json)。
