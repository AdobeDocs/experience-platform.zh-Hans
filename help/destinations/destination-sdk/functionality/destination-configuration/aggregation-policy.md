---
description: 了解如何设置聚合策略，以确定应如何对发往您目标的HTTP请求进行分组和批处理。
title: 聚合策略
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 2%

---


# 聚合策略

为了确保将数据导出到API端点时实现最高效率，您可以使用各种设置将导出的用户档案聚合为更大或更小的批次，按身份和其他用例对它们进行分组。 这还允许您根据API端点的任何下游限制（速率限制、每个API调用的身份数等）来定制数据导出。

使用可配置的聚合深入了解Destination SDK提供的设置，或使用尽力聚合告知Destination SDK尽可能多地分批API调用。

使用Destination SDK构建实时（流）目标时，您可以配置如何将导出的用户档案组合到生成的导出中。 此行为由聚合策略设置决定。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅 [配置选项](../configuration-options.md) 文档或参阅指南，了解如何 [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-destination-configuration).

您可以通过以下方式配置聚合策略设置 `/authoring/destinations` 端点。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持的聚合策略设置。

阅读本文档后，请参阅以下文档： [使用模板](../../functionality/destination-server/message-format.md#using-templating) 和 [聚合密钥示例](../../functionality/destination-server/message-format.md#template-aggregation-key) 了解如何根据所选的聚合策略在消息转换模板中包含聚合策略。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免区分大小写错误，请完全按照文档中所示使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 否 |

## 最大努力聚合 {#best-effort-aggregation}

最大努力聚合最适合以下目标：每个请求喜欢较少的配置文件，并且与具有较多数据的更少请求相比，宁愿接收具有较少数据的更多请求。

以下示例配置显示了尽力聚合配置。 有关可配置聚合的示例，请参见 [可配置聚合](#configurable-aggregation) 部分。 下表介绍了适用于最大努力聚合的参数。

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
| `aggregationType` | 字符串 | 指示目标应使用的聚合策略的类型。 支持的聚合类型： <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | 整数 | Experience Platform可以在单个HTTP调用中聚合多个导出的用户档案。 <br><br>此值指示您的端点在单个HTTP调用中应接收的最大配置文件数。 请注意，这是尽力而为的汇总。 例如，如果指定值100，Platform可能会在一次调用中发送任何数量小于100的用户档案。 <br><br> 如果您的服务器不接受每个请求多个用户，请将此值设置为 `1`. |
| `bestEffortAggregation.splitUserById` | 布尔值 | 如果对目标的调用应按身份拆分，则使用此标志。 将此标记设置为 `true` 对于给定的标识命名空间，如果您的服务器仅接受每个调用一个标识。 |

{style="table-layout:auto"}

>[!TIP]
>
>如果您的API端点在每个API调用中接受的用户档案少于100个，请使用尽最大努力聚合。

## 可配置的聚合 {#configurable-aggregation}

如果要在同一调用中批量处理数千个用户档案，那么可配置的聚合效果最好。 此选项还允许您根据复杂的聚合规则聚合导出的用户档案。

下面的示例配置显示了可配置的聚合配置。 有关最大努力汇总的示例，请参见 [尽力而为聚合](#best-effort-aggregation) 部分。 下表介绍了适用于可配置聚合的参数。

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
| `aggregationType` | 字符串 | 指示目标应使用的聚合策略的类型。 支持的聚合类型： <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | 布尔值 | 如果对目标的调用应按身份拆分，则使用此标志。 将此标记设置为 `true` 对于给定的标识命名空间，如果您的服务器仅接受每个调用一个标识。 |
| `configurableAggregation.maxBatchAgeInSecs` | 整数 | 结合使用 `maxNumEventsInBatch`，此参数可确定Experience Platform在将API调用发送到端点之前应等待的时长。 <ul><li>最小值（秒）：1800</li><li>最大值（秒）：3600</li></ul> 例如，如果为这两个参数使用最大值，则Experience Platform将等待3600秒或直到10000有符合条件的配置文件为止，然后再进行API调用（以先发生者为准）。 |
| `configurableAggregation.maxNumEventsInBatch` | 整数 | 与一起使用 `maxBatchAgeInSecs`，此参数确定应在API调用中聚合多少个符合条件的用户档案。 <ul><li>最小值：1000</li><li>最大值： 10000</li></ul> 例如，如果为这两个参数使用最大值，则Experience Platform将等待3600秒或直到10000有符合条件的配置文件为止，然后再进行API调用（以先发生者为准）。 |
| `configurableAggregation.aggregationKey` | - | 允许您根据下述参数聚合映射到目标的导出用户档案。 |
| `configurableAggregation.aggregationKey.includeSegmentId` | 布尔值 | 将此参数设置为 `true` 如果您希望按受众ID对导出到目标的用户档案进行分组。 |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | 布尔值 | 设置此参数和 `includeSegmentId` 到 `true`，适用于要按受众ID和受众状态对导出到目标的用户档案进行分组的情况。 |
| `configurableAggregation.aggregationKey.includeIdentity` | 布尔值 | 将此参数设置为 `true` 如果您希望按身份命名空间对导出到目标的用户档案进行分组。 |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布尔值 | 将此参数设置为 `true` 如果您希望将导出的用户档案根据单个身份（GAID、IDFA、电话号码、电子邮件等）聚合到组中。 |
| `configurableAggregation.aggregationKey.groups` | 数组 | 如果要按身份命名空间组对导出到目标的配置文件进行分组，请创建身份组列表。 例如，可以使用上例中显示的配置，将包含IDFA和GAID移动标识符的用户档案合并到一个对目标的调用中，并将电子邮件合并到另一个调用中。 |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解如何为目标配置聚合策略。

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
* [批次配置](batch-configuration.md)
* [历史配置文件资格](historical-profile-qualifications.md)