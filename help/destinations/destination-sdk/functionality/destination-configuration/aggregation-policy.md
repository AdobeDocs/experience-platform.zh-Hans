---
description: 了解如何设置聚合策略，以确定应如何对发往您目标的HTTP请求进行分组和批处理。
title: 聚合策略
exl-id: 2dfa8815-2d69-4a22-8938-8ea41be8b9c5
source-git-commit: 92d7abcbd642cea4e0fa041d2926ba8868f506e5
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 2%

---

# 聚合策略

为了确保将数据导出到API端点时实现最高效率，您可以使用各种设置将导出的用户档案聚合为更大或更小的批次，按身份和其他用例对其进行分组。 这还允许您根据API端点的任何下游限制（速率限制、每个API调用的身份数等）定制数据导出。

使用可配置的聚合深入了解Destination SDK提供的设置，或使用尽力聚合告知Destination SDK尽可能多地批处理API调用。

使用Destination SDK构建实时（流）目标时，您可以配置如何将导出的用户档案组合在生成的导出中。 此行为由聚合策略设置决定。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅[配置选项](../configuration-options.md)文档中的关系图，或参阅如何[使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-destination-configuration)的指南。

您可以通过`/authoring/destinations`端点配置聚合策略设置。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持的聚合策略设置。

阅读本文档后，请参阅有关[使用模板](../../functionality/destination-server/message-format.md#using-templating)和[聚合密钥示例](../../functionality/destination-server/message-format.md#template-aggregation-key)的文档，了解如何根据所选的聚合策略将聚合策略包含在消息转换模板中。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;****。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 否 |

## 最大努力聚合 {#best-effort-aggregation}

最大努力聚合最适合以下目标：每个请求喜欢较少的配置文件，并且与具有较多数据的更少请求相比，宁愿接收具有较少数据的更多请求。

以下示例配置显示了最大努力聚合配置。 有关可配置聚合的示例，请参阅[可配置聚合](#configurable-aggregation)部分。 下表介绍了适用于最大努力聚合的参数。

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false,
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
| `bestEffortAggregation.maxUsersPerRequest` | 整数 | Experience Platform可以在单个HTTP调用中聚合多个导出的用户档案。 <br><br>此值指示您的终结点在一个HTTP调用中应接收的最大配置文件数。 请注意，这是最大努力汇总。 例如，如果指定值100，Experience Platform在调用中可能会发送任何数量小于100的用户档案。 <br><br>如果您的服务器不接受每个请求多个用户，请将此值设置为`1`。 |
| `bestEffortAggregation.splitUserById` | 布尔值 | 如果对目标的调用应按身份拆分，则使用此标志。 如果您的服务器在每次调用中只接受一个给定身份命名空间中的身份，请将此标志设置为`true`。 |
| `bestEffortAggregation.aggregationKey` | 对象 | *可选*。 允许您根据下述参数聚合映射到目标的导出用户档案。 如果不需要聚合，则可以忽略此参数或将其设置为`null`。 提供后，它在可配置的聚合中的功能与聚合密钥相同。 |
| `bestEffortAggregation.aggregationKey.includeSegmentId` | 布尔值 | 如果要按受众ID对导出到目标的配置文件进行分组，请将此参数设置为`true`。 |
| `bestEffortAggregation.aggregationKey.includeSegmentStatus` | 布尔值 | 如果要按受众ID和受众状态对导出到目标的配置文件进行分组，请将此参数和`includeSegmentId`设置为`true`。 |
| `bestEffortAggregation.aggregationKey.includeIdentity` | 布尔值 | 如果要按身份命名空间对导出到目标的配置文件进行分组，请将此参数设置为`true`。 |
| `bestEffortAggregation.aggregationKey.oneIdentityPerGroup` | 布尔值 | 如果您希望导出的用户档案根据单个身份（GAID、IDFA、电话号码、电子邮件等）聚合到组中，请将此参数设置为`true`。 如果要使用`false`参数定义自定义身份命名空间分组，则设置为`groups`。 |
| `bestEffortAggregation.aggregationKey.groups` | 数组 | 当`oneIdentityPerGroup`设置为`false`时，使用此参数。 如果要按身份命名空间组对导出到目标的配置文件进行分组，请创建身份组列表。 例如，可以使用上例中显示的配置，将包含IDFA和GAID移动标识符的用户档案合并到一个对目标的调用中，并将电子邮件合并到另一个调用中。 |

{style="table-layout:auto"}

>[!TIP]
>
>如果您的API端点在每个API调用中接受少于100个配置文件，请使用最大努力聚合。

## 可配置的聚合 {#configurable-aggregation}

如果更愿意以大批量方式进行，且在同一调用中使用数千个配置文件，则可配置的聚合效果最佳。 此选项还允许您根据复杂的聚合规则聚合导出的用户档案。

下面的示例配置显示了可配置的聚合配置。 有关最大努力聚合的示例，请参阅[最大努力聚合](#best-effort-aggregation)部分。 下表介绍了适用于可配置聚合的参数。

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
| `configurableAggregation.splitUserById` | 布尔值 | 如果对目标的调用应按身份拆分，则使用此标志。 如果您的服务器在每次调用中只接受一个给定身份命名空间中的身份，请将此标志设置为`true`。 |
| `configurableAggregation.maxBatchAgeInSecs` | 整数 | 此参数与`maxNumEventsInBatch`一起使用时，可决定Experience Platform向端点发送API调用之前应等待的时间。 <ul><li>最小值（秒）：301</li><li>最大值（秒）：3,600</li></ul> 例如，如果为这两个参数使用最大值，Experience Platform将等待3,600秒或直到10000有符合条件的配置文件为止，然后再进行API调用（以先发生者为准）。 |
| `configurableAggregation.maxNumEventsInBatch` | 整数 | 此参数与`maxBatchAgeInSecs`结合使用，可确定在API调用中应聚合多少个符合条件的配置文件。 <ul><li>最小值：1,000</li><li>最大值：10,000</li></ul> 例如，如果为这两个参数使用最大值，Experience Platform将等待3,600秒或直到具有10,000个符合条件的配置文件，然后再进行API调用（以先发生者为准）。 |
| `configurableAggregation.aggregationKey` | - | 允许您根据下述参数聚合映射到目标的导出用户档案。 |
| `configurableAggregation.aggregationKey.includeSegmentId` | 布尔值 | 如果要按受众ID对导出到目标的配置文件进行分组，请将此参数设置为`true`。 |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | 布尔值 | 如果要按受众ID和受众状态对导出到目标的配置文件进行分组，请将此参数和`includeSegmentId`设置为`true`。 |
| `configurableAggregation.aggregationKey.includeIdentity` | 布尔值 | 如果要按身份命名空间对导出到目标的配置文件进行分组，请将此参数设置为`true`。 |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布尔值 | 如果您希望导出的用户档案根据单个身份（GAID、IDFA、电话号码、电子邮件等）聚合到组中，请将此参数设置为`true`。 如果要使用`false`参数定义自定义身份命名空间分组，则设置为`groups`。 |
| `configurableAggregation.aggregationKey.groups` | 数组 | 当`oneIdentityPerGroup`设置为`false`时，使用此参数。 如果要按身份命名空间组对导出到目标的配置文件进行分组，请创建身份组列表。 例如，可以使用上例中显示的配置，将包含IDFA和GAID移动标识符的用户档案合并到一个对目标的调用中，并将电子邮件合并到另一个调用中。 |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解如何为目标配置聚合策略。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证配置](customer-authentication.md)
* [OAuth2授权](oauth2-authorization.md)
* [客户数据字段](customer-data-fields.md)
* [UI属性](ui-attributes.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [批次配置](batch-configuration.md)
* [历史配置文件资格](historical-profile-qualifications.md)
