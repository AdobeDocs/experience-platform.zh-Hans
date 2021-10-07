---
description: 此配置允许您指示目标名称、类别、描述、徽标等基本信息。 此配置中的设置还可确定Experience Platform用户如何对您的目标进行身份验证、该目标如何显示在Experience Platform用户界面中，以及可导出到您目标的身份。
title: 目标SDK的目标配置选项
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 76a596166edcdbf141b5ce5dc01557d2a0b4caf3
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 5%

---

# 目标配置 {#destination-configuration}

## 概述 {#overview}

此配置允许您指示目标名称、类别、描述、徽标等基本信息。 此配置中的设置还可确定Experience Platform用户如何对您的目标进行身份验证、该目标如何显示在Experience Platform用户界面中，以及可导出到您目标的身份。

此配置还会将目标工作所需的其他配置（目标服务器和受众元数据）连接到此配置。 阅读如何在](./destination-configuration.md#connecting-all-configurations)下方的[部分中引用这两个配置。

您可以使用`/authoring/destinations` API端点配置本文档中描述的功能。 请阅读[目标API端点操作](./destination-configuration-api.md) ，以获取可对端点执行的操作的完整列表。

## 示例配置 {#example-configuration}

以下是虚构目标Moviestar的示例配置，该目标在全球四个位置的端点。 目标属于移动设备目标类别。 以下各节将进一步划分此配置的构建方式。

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
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
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
| `status` | 字符串 | 指示目标卡的生命周期状态。 接受的值包括 `TEST`、`PUBLISHED` 和 `DELETED`。首次配置目标时，请使用`TEST`。 |

{style=&quot;table-layout:auto&quot;}

## 客户身份验证配置 {#customer-authentication-configurations}

此部分在Experience Platform用户界面中生成帐户页面，用户可在该页面中将Experience Platform连接到他们与您的目标拥有的帐户。 根据您在`authType`字段中指示的身份验证选项，将为用户生成Experience Platform页面，如下所示：

**承载验证**

用户需要输入从您的目标获取的载体令牌。

![具有承载身份验证的UI呈现](./assets/bearer-authentication-ui.png)

**OAuth 2身份验证**

用户选择&#x200B;**[!UICONTROL 连接到目标]**&#x200B;以触发到您目标的OAuth 2身份验证流。

![使用OAuth 2身份验证渲染UI](./assets/oauth2-authentication-ui.png)


| 参数 | 类型 | 描述 |
|---------|----------|------|
| `customerAuthenticationConfigurations` | 字符串 | 指示用于向服务器验证Experience Platform客户的配置。 有关已接受的值，请参阅下面的`authType`。 |
| `authType` | 字符串 | 接受的值为`OAUTH2, BEARER`。 <br><ul><li> 如果您的目标支持OAuth 2身份验证，请选择`OAUTH2`值并添加OAuth 2的必填字段，如目标SDK OAuth 2身份验证页面中所示。 此外，您还应在[目标投放部分](./destination-configuration.md)中选择`authenticationRule=CUSTOMER_AUTHENTICATION`。 </li><li>对于承载身份验证，请选择`BEARER`并在[目标投放部分](./destination-configuration.md)中选择`authenticationRule=CUSTOMER_AUTHENTICATION`。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 客户数据字段 {#customer-data-fields}

此部分允许合作伙伴引入自定义字段。 在上面的示例配置中，`customerDataFields`要求用户在身份验证流程中选择一个端点，并在目标中指示其客户ID。 配置会反映在身份验证流程中，如下所示：

![自定义字段身份验证流程](./assets/custom-field-authentication-flow.png)

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `name` | 字符串 | 为要引入的自定义字段提供名称。 |
| `type` | 字符串 | 指示您引入的自定义字段类型。 接受的值为`string`、`object`、`integer`。 |
| `title` | 字符串 | 指示字段的名称，客户在Experience Platform用户界面中可看到该字段。 |
| `description` | 字符串 | 为自定义字段提供描述。 |
| `isRequired` | 布尔型 | 指示目标设置工作流中是否需要此字段。 |
| `enum` | 字符串 | 将自定义字段呈现为下拉菜单，并列出可供用户使用的选项。 |
| `pattern` | 字符串 | 如果需要，可为自定义字段实施模式。 使用正则表达式来强制实施模式。 例如，如果您的客户ID不包含数字或下划线，请在此字段中输入`^[A-Za-z]+$`。 |

{style=&quot;table-layout:auto&quot;}

## UI属性 {#ui-attributes}

此部分引用上述配置中的UI元素，Adobe应在Adobe Experience Platform用户界面中将其用于您的目标。 请参阅下文：

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `documentationLink` | 字符串 | 指目标的[目标目录](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog)中的文档页面。 使用`http://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中`YOURDESTINATION`是目标的名称。 对于名为Moviestar的目标，您应使用`http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | 字符串 | 是指分配给您在Adobe Experience Platform中的目标的类别。 有关更多信息，请阅读[目标类别](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html)。 使用以下任一值：`adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`。 |
| `connectionType` | 字符串 | `Server-to-server` 是当前唯一可用的选项。 |
| `frequency` | 字符串 | `Streaming` 是当前唯一可用的选项。 |

{style=&quot;table-layout:auto&quot;}

## 映射步骤中的架构配置 {#schema-configuration}

![启用映射步骤](./assets/enable-mapping-step.png)

使用`schemaConfig`中的参数启用目标激活工作流的映射步骤。 通过使用下面描述的参数，您可以确定Experience Platform用户是否可以将配置文件属性和/或身份映射到目标方的所需架构。

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `profileFields` | 数组 | *上述示例配置中未显示。* 添加预定义 `profileFields`属性时，Experience Platform用户可以选择将平台属性映射到目标侧的预定义属性。 |
| `profileRequired` | 布尔型 | 如果用户应该能够将配置文件属性从Experience Platform映射到目标侧的自定义属性，请使用`true` ，如上面的示例配置中所示。 |
| `segmentRequired` | 布尔型 | 始终使用`segmentRequired:true`。 |
| `identityRequired` | 布尔型 | 如果用户应能够将身份命名空间从Experience Platform映射到所需的架构，请使用`true`。 |

{style=&quot;table-layout:auto&quot;}

## 身份和属性 {#identities-and-attributes}

此部分中的参数可确定如何在Experience Platform用户界面的映射步骤中填充目标标识和属性，用户可在该步骤中将其XDM架构映射到您目标中的架构。

您必须指示哪些[!DNL Platform]标识客户能够导出到您的目标。 一些示例包括[!DNL Experience Cloud ID]、经过哈希处理的电子邮件、设备ID([!DNL IDFA]、[!DNL GAID])。 这些值是[!DNL Platform]身份命名空间，客户可以将其映射到来自您目标的身份命名空间。

身份命名空间不要求[!DNL Platform]与目标之间进行一对一的通信。
例如，客户可以将[!DNL Platform] [!DNL IDFA]命名空间映射到您目标中的[!DNL IDFA]命名空间，或者，他们可以将相同的[!DNL Platform] [!DNL IDFA]命名空间映射到您目标中的[!DNL Customer ID]命名空间。

有关更多信息，请参阅[身份命名空间概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans)。

![在UI中渲染Target标识](./assets/target-identities-ui.png)

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `acceptsAttributes` | 布尔型 | 指示您的目标是否接受标准配置文件属性。 通常，合作伙伴文档中会突出显示这些属性。 |
| `acceptsCustomNamespaces` | 布尔型 | 指示客户是否可以在您的目标中设置自定义命名空间。 |
| `allowedAttributesTransformation` | 字符串 | *示例配置中未显示*。例如，当[!DNL Platform]客户将纯电子邮件地址作为属性，且您的平台仅接受经过哈希处理的电子邮件时，便会使用。 在此对象中，您可以应用需要的转换（例如，将电子邮件转换为小写，然后进行哈希转换）。 有关示例，请参阅[目标配置API引用](./destination-configuration-api.md#update)中的`requiredTransformation`。 |
| `acceptedGlobalNamespaces` | - | 用于平台接受[标准身份命名空间](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces)（例如IDFA）时的情况，因此您可以限制Platform用户仅选择这些身份命名空间。 |

{style=&quot;table-layout:auto&quot;}

## 目标投放 {#destination-delivery}

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `authenticationRule` | 字符串 | 指示[!DNL Platform]客户如何连接到您的目标。 接受的值为`CUSTOMER_AUTHENTICATION`、`PLATFORM_AUTHENTICATION`、`NONE`。 <br> <ul><li>如果Platform客户通过用户名和密码、载体令牌或其他身份验证方法登录您的系统，请使用`CUSTOMER_AUTHENTICATION`。 例如，如果您还在`customerAuthenticationConfigurations`中选择了`authType: OAUTH2`或`authType:BEARER`，则可以选择此选项。 </li><li> 如果Adobe与目标之间存在全局身份验证系统，且[!DNL Platform]客户不需要提供任何身份验证凭据即可连接到您的目标，则使用`PLATFORM_AUTHENTICATION`。 在这种情况下，必须使用[Credentials](./credentials-configuration.md)配置创建凭据对象。 </li><li>如果向目标平台发送数据不需要任何身份验证，则使用`NONE`。 </li></ul> |
| `destinationServerId` | 字符串 | 用于此目标的[目标服务器配置](./destination-server-api.md)的`instanceId`。 |
| `backfillHistoricalProfileData` | 布尔型 | 控制在将区段激活到目标时是否导出历史配置文件数据。<br> <ul><li> `true`: [!DNL Platform] 发送在激活区段之前符合区段资格条件的历史用户配置文件。 </li><li> `false`: [!DNL Platform] 仅包括激活区段后符合区段资格的用户配置文件。 </li></ul> |

{style=&quot;table-layout:auto&quot;}

## 区段映射配置 {#segment-mapping}

![区段映射配置部分](./assets/segment-mapping-configuration.png)

目标配置的此部分与区段元数据（如区段名称或ID）在Experience Platform与目标之间共享的方式相关。

通过`audienceTemplateId`，此部分还将此配置与[受众元数据配置](./audience-metadata-management.md)绑定在一起。

上述配置中显示的参数在[目标端点API引用](./destination-configuration-api.md)中进行了描述。

## 此配置如何连接目标的所有必需信息 {#connecting-all-configurations}

可以通过目标服务器或受众元数据端点配置目标的某些设置。 目标配置端点通过引用以下配置来连接所有这些设置：

* 使用`destinationServerId`引用为目标设置的目标服务器和模板配置。
* 使用`audienceMetadataId`引用为目标设置的受众元数据配置。


## 聚合策略 {#aggregation}

![配置模板中的聚合策略](./assets/aggregation-configuration.png)

利用此部分，可设置Experience Platform在将数据导出到目标时应使用的聚合策略。

聚合策略确定导出的用户档案在数据导出中的合并方式。 可用选项包括：
* 尽力汇总
* 可配置聚合（如上面的配置中所示）

请阅读[中关于使用模板](./message-format.md#using-templating)和[聚合键示例](./message-format.md#template-aggregation-key)的章节，以了解如何根据您选择的聚合策略将聚合策略包含在消息转换模板中。

### 尽力汇总 {#best-effort-aggregation}

>[!TIP]
>
>如果您的API端点每个API调用接受的配置文件少于100个，则使用此选项。

此选项最适用于那些希望每个请求少使用用户档案的目标，它们更愿意接收数据较少的请求，而不是数据较多的请求。

使用`maxUsersPerRequest`参数指定目标在请求中可接收的配置文件的最大数量。

### 可配置聚合 {#configurable-aggregation}

如果您希望批量处理，并且在同一调用中具有数千个用户档案，则此选项最有效。 此选项还允许您根据复杂的聚合规则聚合导出的用户档案。

此选项允许您：
* 在对目标进行API调用之前，设置要聚合的用户档案的最大时间和数量。
* 根据以下信息聚合映射到目标的导出用户档案：
   * 区段ID
   * 区段状态
   * 身份或身份组

有关聚合参数的详细说明，请参阅[目标API端点操作](./destination-configuration-api.md)参考页，其中描述了每个参数。

## 历史用户档案资格

您可以使用目标配置中的`backfillHistoricalProfileData`参数来确定是否应将历史配置文件资格导出到您的目标。

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `backfillHistoricalProfileData` | 布尔型 | 控制在将区段激活到目标时是否导出历史配置文件数据。<br> <ul><li> `true`: [!DNL Platform] 发送在激活区段之前符合区段资格条件的历史用户配置文件。 </li><li> `false`: [!DNL Platform] 仅包括激活区段后符合区段资格的用户配置文件。 </li></ul> |