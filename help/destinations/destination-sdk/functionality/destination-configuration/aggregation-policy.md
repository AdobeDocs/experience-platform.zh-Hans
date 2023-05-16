---
description: 了解如何设置聚合策略以确定对目标的HTTP请求应如何分组和批量处理。
title: 聚合策略
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 2%

---


# 聚合策略

为确保在将数据导出到API端点时获得最大效率，您可以使用各种设置将导出的配置文件聚合到较大或较小的批次中，按身份和其他用例对它们进行分组。 这还允许您根据API端点的任何下游限制（速率限制、每个API调用的标识数等）来定制数据导出。

使用可配置聚合深入了解Destination SDK提供的设置，或使用尽最大努力聚合告知Destination SDK尽可能对API调用进行批处理。

构建具有Destination SDK的实时（流）目标时，您可以配置导出的用户档案在结果导出中的合并方式。 此行为由聚合策略设置决定。

要了解此组件在与Destination SDK创建的集成中的位置，请参阅 [配置选项](../configuration-options.md) 文档，或参阅有关如何 [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-destination-configuration).

您可以通过 `/authoring/destinations` 端点。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持的聚合策略设置。

阅读本文档后，请参阅 [用模板](../../functionality/destination-server/message-format.md#using-templating) 和 [聚合关键示例](../../functionality/destination-server/message-format.md#template-aggregation-key) 了解如何根据您选择的聚合策略在消息转换模板中包含聚合策略。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均为 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持本页所述功能的详细信息，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件的（批处理）集成 | 否 |

## 尽力汇总 {#best-effort-aggregation}

尽力聚合最适合那些希望每个请求的用户档案数量较少的目标，它们更愿意接收数据较少的请求数量多于数据较多的请求数量。

以下示例配置显示了尽力的聚合配置。 有关可配置聚合的示例，请参阅 [可配置聚合](#configurable-aggregation) 中。 适用于尽力聚合的参数记录在下表中。

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false
   }
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `aggregationType` | 字符串 | 指示目标应使用的聚合策略类型。 支持的聚合类型： <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | 整数 | Experience Platform可以在一个HTTP调用中聚合多个导出的配置文件。 <br><br>此值指示您的端点在单个HTTP调用中应接收的最大配置文件数。 请注意，这是一种尽力的聚合。 例如，如果您指定值100,Platform可能会在一次调用中发送任意数量小于100的用户档案。 <br><br> 如果您的服务器不接受每个请求的多个用户，请将此值设置为 `1`. |
| `bestEffortAggregation.splitUserById` | 布尔值 | 如果目标的调用应按身份进行拆分，则使用此标记。 将此标志设置为 `true` 如果服务器在每次调用中仅接受一个身份，则表示给定的身份命名空间。 |

{style="table-layout:auto"}

>[!TIP]
>
>如果您的API端点每个API调用接受的用户档案少于100个，请尽最大努力进行聚合。

## 可配置聚合 {#configurable-aggregation}

如果您希望批量处理，并且在同一调用中具有数千个配置文件，则可配置聚合最有效。 此选项还允许您根据复杂的聚合规则聚合导出的用户档案。

以下示例配置显示了可配置的聚合配置。 有关尽力聚合的示例，请参阅 [最佳工作聚合](#best-effort-aggregation) 中。 适用于可配置聚合的参数记录在下表中。

```json
"aggregation":{
   "aggregationType":"CONFIGURABLE_AGGREGATION",
   "configurableAggregation":{
      "splitUserById":true,
      "maxBatchAgeInSecs":2400,
      "maxNumEventsInBatch":5000,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `aggregationType` | 字符串 | 指示目标应使用的聚合策略类型。 支持的聚合类型： <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | 布尔值 | 如果目标的调用应按身份进行拆分，则使用此标记。 将此标志设置为 `true` 如果服务器在每次调用中仅接受一个身份，则表示给定的身份命名空间。 |
| `configurableAggregation.maxBatchAgeInSecs` | 整数 | 用于 `maxNumEventsInBatch`，此参数可确定Experience Platform应等待多长时间，直到向您的端点发送API调用。 <ul><li>最小值（秒）：1800</li><li>最大值（秒）：3600</li></ul> 例如，如果您对两个参数使用最大值，则Experience Platform将等待3600秒或直到有10000个符合条件的配置文件才进行API调用，以先发生的为准。 |
| `configurableAggregation.maxNumEventsInBatch` | 整数 | 与 `maxBatchAgeInSecs`，此参数可确定在API调用中应聚合多少个符合条件的用户档案。 <ul><li>最小值：1000</li><li>最大值：10000</li></ul> 例如，如果您对两个参数使用最大值，则Experience Platform将等待3600秒或直到有10000个符合条件的配置文件才进行API调用，以先发生的为准。 |
| `configurableAggregation.aggregationKey` | - | 允许您根据下面描述的参数聚合映射到目标的导出配置文件。 |
| `configurableAggregation.aggregationKey.includeSegmentId` | 布尔值 | 将此参数设置为 `true` 要按区段ID对导出到目标的用户档案进行分组。 |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | 布尔值 | 同时设置此参数和 `includeSegmentId` to `true`，以便按区段ID和区段状态对导出到目标的用户档案进行分组。 |
| `configurableAggregation.aggregationKey.includeIdentity` | 布尔值 | 将此参数设置为 `true` 如果要按身份命名空间对导出到目标的用户档案进行分组。 |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布尔值 | 将此参数设置为 `true` 如果您希望将导出的用户档案根据单个身份（GAID、IDFA、电话号码、电子邮件等）聚合到组中。 |
| `configurableAggregation.aggregationKey.groups` | 数组 | 如果要按身份命名空间的组对导出到目标的配置文件进行分组，请创建身份组列表。 例如，您可以使用上例中显示的配置，将包含IDFA和GAID移动标识符的用户档案合并到对目标的一次调用中，以及将电子邮件合并到另一个调用中。 |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

阅读本文后，您应该对如何为目标配置聚合策略有了更好的了解。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证配置](customer-authentication.md)
* [OAuth2身份验证](oauth2-authentication.md)
* [客户数据字段](customer-data-fields.md)
* [UI属性](ui-attributes.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [批量配置](batch-configuration.md)
* [历史用户档案资格](historical-profile-qualifications.md)