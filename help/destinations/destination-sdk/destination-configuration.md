---
description: 此配置允许您指示目标名称、类别、描述、徽标等基本信息。 此配置中的设置还可确定Experience Platform用户如何对您的目标进行身份验证、该目标如何显示在Experience Platform用户界面中，以及可导出到您目标的身份。
title: 用于Destination SDK的流目标配置选项
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 301cef53644e813c3fd43e7f2dbaf730c9e5fc11
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 4%

---

# 流目标配置 {#destination-configuration}

## 概述 {#overview}

此配置允许您指示流目标的基本信息，如目标名称、类别、描述等。 此配置中的设置还可确定Experience Platform用户如何对您的目标进行身份验证、该目标如何显示在Experience Platform用户界面中，以及可导出到您目标的身份。

此配置还会将目标工作所需的其他配置（目标服务器和受众元数据）连接到此配置。 了解如何在 [下文](./destination-configuration.md#connecting-all-configurations).

您可以使用 `/authoring/destinations` API端点。 读取 [目标API端点操作](./destination-configuration-api.md) 有关可对端点执行的操作的完整列表。

## 流配置示例 {#example-configuration}

这是虚构流目的地Moviestar的示例配置，该目的地在地球上的四个位置有端点。 目标属于移动设备目标类别。

```json
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "schemaConfig":{
      "profileRequired":false,
      "segmentRequired":true,
      "identityRequired":true
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
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
            "oneIdentityPerGroup":false,
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
   },
   "backfillHistoricalProfileData":true
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `name` | 字符串 | 指示Experience Platform目录中目标的标题。 |
| `description` | 字符串 | 在Experience Platform目标目录中，提供目标卡的描述。 目标不超过4-5句。 |
| `status` | 字符串 | 指示目标卡的生命周期状态。 接受的值包括 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 首次配置目标时。 |

{style=&quot;table-layout:auto&quot;}

## 客户身份验证配置 {#customer-authentication-configurations}

目标配置中的此部分将生成 [配置新目标](/help/destinations/ui/connect-destination.md) Experience Platform用户界面中的页面，用户可将Experience Platform连接到他们与您的目标拥有的帐户。 根据您在 `authType` 字段中，将为用户生成Experience Platform页面，如下所示：

### 承载验证

当您配置承载身份验证类型时，用户需要输入他们从您的目标获取的承载令牌。

![具有承载身份验证的UI呈现](assets/bearer-authentication-ui.png)

### OAuth 2身份验证

用户选择 **[!UICONTROL 连接到目标]** 触发到您目标的OAuth 2身份验证流，如以下Twitter自定义受众目标示例所示。 有关将OAuth 2身份验证配置到目标端点的详细信息，请阅读专用 [Destination SDKOAuth 2身份验证页面](./oauth2-authentication.md).

![使用OAuth 2身份验证渲染UI](assets/oauth2-authentication-ui.png)

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `customerAuthenticationConfigurations` | 字符串 | 指示用于向服务器验证Experience Platform客户的配置。 请参阅 `authType` 下方的值。 |
| `authType` | 字符串 | 流目标的接受值包括：<ul><li>`BEARER`的问题。如果您的目标支持载体身份验证，请设置 `"authType":"Bearer"` 和  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` 在 [目标投放部分](./destination-configuration.md).</li><li>`OAUTH2`的问题。如果您的目标支持OAuth 2身份验证，请设置 `"authType":"OAUTH2"` 和，添加OAuth 2的必填字段，如 [Destination SDKOAuth 2身份验证页面](./oauth2-authentication.md). 此外，设置 `"authenticationRule":"CUSTOMER_AUTHENTICATION"` 在 [目标投放部分](./destination-configuration.md).</li> |

{style=&quot;table-layout:auto&quot;}

## 客户数据字段 {#customer-data-fields}

在Experience PlatformUI中连接到目标时，使用此部分要求用户填写特定于您目标的自定义字段。 配置会反映在身份验证流程中，如下所示：

![自定义字段身份验证流程](./assets/custom-field-authentication-flow.png)

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `name` | 字符串 | 为要引入的自定义字段提供名称。 |
| `type` | 字符串 | 指示您引入的自定义字段类型。 接受的值为 `string`, `object`, `integer`. |
| `title` | 字符串 | 指示字段的名称，客户在Experience Platform用户界面中可看到该字段。 |
| `description` | 字符串 | 为自定义字段提供描述。 |
| `isRequired` | 布尔型 | 指示目标设置工作流中是否需要此字段。 |
| `enum` | 字符串 | 将自定义字段呈现为下拉菜单，并列出可供用户使用的选项。 |
| `pattern` | 字符串 | 如果需要，可为自定义字段实施模式。 使用正则表达式来强制实施模式。 例如，如果您的客户ID不包含数字或下划线，请输入 `^[A-Za-z]+$` 中。 |

{style=&quot;table-layout:auto&quot;}

## UI属性 {#ui-attributes}

此部分引用上述配置中的UI元素，Adobe应在Adobe Experience Platform用户界面中将其用于您的目标。 请参阅下文：

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `documentationLink` | 字符串 | 指 [目标目录](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 你的目的地。 使用 `http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是您的目标名称。 对于名为Moviestar的目标，您将使用 `http://www.adobe.com/go/destinations-moviestar-en`. 请注意，此链接仅在Adobe设置目标处于实时状态且文档已发布后才可用。 |
| `category` | 字符串 | 是指分配给您在Adobe Experience Platform中的目标的类别。 有关更多信息，请阅读 [目标类别](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). 使用以下任一值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `connectionType` | 字符串 | `Server-to-server` 是当前唯一可用的选项。 |
| `frequency` | 字符串 | 是指目标支持的数据导出类型。 支持的值： <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 映射步骤中的架构配置 {#schema-configuration}

![启用映射步骤](./assets/enable-mapping-step.png)

在中使用参数 `schemaConfig` 以启用目标激活工作流的映射步骤。 通过使用下面描述的参数，您可以确定Experience Platform用户是否可以将配置文件属性和/或身份映射到目标方的所需架构。

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `profileFields` | 数组 | *上述示例配置中未显示。* 添加预定义 `profileFields`，则Experience Platform用户可以选择将平台属性映射到目标侧的预定义属性。 |
| `profileRequired` | 布尔型 | 使用 `true` 如上面的示例配置所示，用户应该能够在目标侧将配置文件属性从Experience Platform映射到自定义属性。 |
| `segmentRequired` | 布尔型 | 始终使用 `segmentRequired:true`. |
| `identityRequired` | 布尔型 | 使用 `true` 用户应能够将身份命名空间从Experience Platform映射到所需的架构。 |

{style=&quot;table-layout:auto&quot;}


## 身份和属性 {#identities-and-attributes}

此部分中的参数可确定目标接受的身份。 此配置还会在 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) Experience Platform用户界面的中，用户可将身份和属性从其XDM架构映射到目标中的架构。

您必须指明 [!DNL Platform] 标识客户能够导出到您的目标。 例如 [!DNL Experience Cloud ID]，经过哈希处理的电子邮件，设备ID([!DNL IDFA], [!DNL GAID])。 这些值包括 [!DNL Platform] 客户可以映射到来自您目标的身份命名空间的身份命名空间。 您还可以指示客户是否可以将自定义命名空间映射到您的目标支持的身份。

身份命名空间不需要 [!DNL Platform] 和你的目的地。
例如，客户可以映射 [!DNL Platform] [!DNL IDFA] 命名空间 [!DNL IDFA] 命名空间，或者它们可以映射相同的 [!DNL Platform] [!DNL IDFA] 命名空间 [!DNL Customer ID] 命名空间。

有关更多信息，请参阅 [身份命名空间概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans).

![在UI中渲染Target标识](./assets/target-identities-ui.png)

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `acceptsAttributes` | 布尔型 | 指示您的目标是否接受标准配置文件属性。 通常，合作伙伴文档中会突出显示这些属性。 |
| `acceptsCustomNamespaces` | 布尔型 | 指示客户是否可以在您的目标中设置自定义命名空间。 |
| `transformation` | 字符串 | *示例配置中未显示*. 例如，当 [!DNL Platform] 客户将纯电子邮件地址作为属性，且您的平台仅接受经过哈希处理的电子邮件。 在此对象中，您可以应用需要的转换（例如，将电子邮件转换为小写，然后进行哈希转换）。 有关示例，请参阅 `requiredTransformation` 在 [目标配置API引用](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | - | 用于平台接受 [标准身份命名空间](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) （例如IDFA），以便您可以限制Platform用户仅选择这些身份命名空间。 |

{style=&quot;table-layout:auto&quot;}

## 目标投放 {#destination-delivery}

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `authenticationRule` | 字符串 | 指示方式 [!DNL Platform] 客户连接到您的目标。 接受的值为 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客户通过用户名和密码、载体令牌或其他身份验证方法登录您的系统。 例如，如果您还选择了 `authType: OAUTH2` 或 `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe与目标之间存在全局身份验证系统，并且 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。 在这种情况下，必须使用 [凭据](./credentials-configuration-api.md) 配置。 </li><li>使用 `NONE` 如果向目标平台发送数据时不需要任何身份验证。 </li></ul> |
| `destinationServerId` | 字符串 | 的 `instanceId` 的 [目标服务器配置](./destination-server-api.md) 用于此目标。 |

{style=&quot;table-layout:auto&quot;}

## 区段映射配置 {#segment-mapping}

![区段映射配置部分](./assets/segment-mapping-configuration.png)

目标配置的此部分与区段元数据（如区段名称或ID）在Experience Platform与目标之间共享的方式相关。

通过 `audienceTemplateId`，此部分还会将此配置与 [受众元数据配置](./audience-metadata-management.md).

上述配置中显示的参数在 [目标端点API引用](./destination-configuration-api.md).

## 聚合策略 {#aggregation}

![配置模板中的聚合策略](./assets/aggregation-configuration.png)

利用此部分，可设置Experience Platform在将数据导出到目标时应使用的聚合策略。

聚合策略确定导出的用户档案在数据导出中的合并方式。 可用选项包括：
* 尽力汇总
* 可配置聚合（如上面的配置中所示）

阅读 [用模板](./message-format.md#using-templating) 和 [聚合关键示例](./message-format.md#template-aggregation-key) 了解如何根据您选择的聚合策略在消息转换模板中包含聚合策略。

### 尽力汇总 {#best-effort-aggregation}

>[!TIP]
>
>如果您的API端点每个API调用接受的配置文件少于100个，则使用此选项。

此选项最适用于那些希望每个请求少使用用户档案的目标，它们更愿意接收数据较少的请求，而不是数据较多的请求。

使用 `maxUsersPerRequest` 参数指定目标在请求中可接收的最大用户档案数。

### 可配置聚合 {#configurable-aggregation}

如果您希望批量处理，并且在同一调用中具有数千个用户档案，则此选项最有效。 此选项还允许您根据复杂的聚合规则聚合导出的用户档案。

此选项允许您：

* 在对目标进行API调用之前，设置要聚合的配置文件的最大时间和最大数量。
* 根据以下信息聚合映射到目标的导出用户档案：
   * 区段ID;
   * 区段状态；
   * 身份或身份组。

>[!NOTE]
>
>在对目标使用可配置的聚合选项时，请注意可用于这两个参数的最小值和最大值 `maxBatchAgeInSecs` （最低1.800和最高3.600）和 `maxNumEventsInBatch` （最小1.000，最大10.000）。

有关聚合参数的详细说明，请参阅 [目标API端点操作](./destination-configuration-api.md) 引用页面，其中描述了每个参数。

## 历史用户档案资格 {#profile-backfill}

您可以使用 `backfillHistoricalProfileData` 参数来确定是否应将历史配置文件资格导出到您的目标。

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `backfillHistoricalProfileData` | 布尔型 | 控制在将区段激活到目标时是否导出历史配置文件数据。 <br> <ul><li> `true`: [!DNL Platform] 发送在激活区段之前符合区段资格条件的历史用户配置文件。 </li><li> `false`: [!DNL Platform] 仅包括激活区段后符合区段资格的用户配置文件。 </li></ul> |

{style=&quot;table-layout:auto&quot;}

## 此配置如何连接目标的所有必需信息 {#connecting-all-configurations}

您的某些目标设置必须通过 [目标服务器](./server-and-template-configuration.md) 或 [受众元数据配置](./audience-metadata-management.md). 此处描述的目标配置通过引用以下两个其他配置来连接所有这些设置：

* 使用 `destinationServerId` 引用为目标设置的目标服务器和模板配置。
* 使用 `audienceMetadataId` 引用为您的目标设置的受众元数据配置。