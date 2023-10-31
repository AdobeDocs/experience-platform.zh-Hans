---
description: 了解使用Destination SDK构建的目标支持的历史配置文件资格。
title: 历史配置文件资格
exl-id: 8880cff9-865b-4d45-a24d-a78e77419670
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---

# 历史配置文件资格

默认情况下，通过Destination SDK创建的所有目标都支持历史配置文件资格。 这意味着当用户首次设置到目标的激活数据流时，第一次导出包含曾经符合该区段资格的受众所有成员。

此行为由 `"backfillHistoricalProfileData":true` 目标配置中的参数。

>[!IMPORTANT]
>
>对于通过Destination SDK创建的所有目标，都会启用历史配置文件资格， `backfillHistoricalProfileData` 参数不能由用户配置。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 是 |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when audiences are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the audience before the audience is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the audience after the audience is activated. </li></ul> |

{style="table-layout:auto"} -->


## 后续步骤 {#next-steps}

阅读本文后，您应该知道，在首次将受众导出到目标时，Experience Platform会自动导出符合激活受众条件的所有用户档案的历史群体。 此选项无法在Destination SDK或Experience PlatformUI中进行配置。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证](customer-authentication.md)
* [OAuth2身份验证](oauth2-authentication.md)
* [客户数据字段](customer-data-fields.md)
* [UI属性](ui-attributes.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次配置](batch-configuration.md)
