---
description: 了解如何为通过Destination SDK构建的目标配置合作伙伴模式。
title: 合作伙伴架构配置
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 5%

---


# 合作伙伴架构配置

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。将数据摄取到平台后，其结构将按照XDM架构进行。 有关架构组合模型（包括设计原则和最佳实践）的更多信息，请参阅 [架构组合基础知识](../../../../xdm/schema/composition.md).

使用Destination SDK构建目标时，您可以定义自己的合作伙伴架构以供目标平台使用。 这允许用户将Platform中的配置文件属性映射到目标平台可识别的特定字段，所有这些字段都可在Platform UI中完成。

在为目标配置合作伙伴架构时，您可以优化目标平台支持的字段映射，例如：

* 允许用户映射 `phoneNumber` XDM属性 `phone` 目标平台支持的属性。
* 创建动态合作伙伴架构，Experience Platform可以动态调用以检索目标中所有受支持属性的列表。
* 定义目标平台所需的必填字段映射。

要了解此组件在与Destination SDK创建的集成中的位置，请参阅 [配置选项](../configuration-options.md) 文档，或参阅有关如何 [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以通过 `/authoring/destinations` 端点。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持的架构配置选项，并显示了客户将在平台UI中看到的内容。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均为 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持本页所述功能的详细信息，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件的（批处理）集成 | 是 |

## 支持的架构配置 {#supported-schema-types}

Destination SDK支持多个架构配置：

* 静态架构通过 `profileFields` 数组 `schemaConfig` 中。 在静态架构中，您可以定义应显示在Experience PlatformUI中的每个目标属性 `profileFields` 数组。 如果需要更新架构，则必须 [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md).
* 动态架构使用其他目标服务器类型，称为 [动态模式服务器](../../authoring-api/destination-server/create-destination-server.md)，以根据您自己的API动态生成模式。 动态架构不使用 `profileFields` 数组。 如果需要更新架构，则无需 [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md). 动态架构服务器而是会从您的API中检索更新的架构。
* 在架构配置中，您可以选择添加必需（或预定义）映射。 这些映射是用户能够在Platform UI中查看的映射，但是在设置与目标的连接时，用户无法对其进行修改。 例如，您可以强制将电子邮件地址字段始终发送到目标。

的 `schemaConfig` 部分会根据您需要的架构类型使用多个配置参数，如以下部分所示。

## 创建静态架构 {#attributes-schema}

要使用配置文件属性创建静态架构，请在 `profileFields` 数组，如下所示。

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
}
```

| 参数 | 类型 | 必填/可选 | 描述 |
|---------|----------|------|---|
| `profileFields` | 数组 | 可选 | 定义目标平台接受的目标属性数组，客户可以将其配置文件属性映射到该数组。 使用 `profileFields` 数组，则可以忽略 `useCustomerSchemaForAttributeMapping` 参数。 |
| `useCustomerSchemaForAttributeMapping` | 布尔值 | 可选 | 启用或禁用将属性从客户架构映射到您在 `profileFields` 数组。 <ul><li>如果设置为 `true`，则用户只会在映射字段中看到源列。 `profileFields` 不适用于此情况。</li><li>如果设置为 `false`，则用户可以将源属性从其架构映射到您在 `profileFields` 数组。</li></ul> 默认值为 `false`。 |
| `profileRequired` | 布尔值 | 可选 | 使用 `true` 如果用户应能够将目标平台上的配置文件属性从Experience Platform映射到自定义属性。 |
| `segmentRequired` | 布尔值 | 必需 | 此参数是Destination SDK的必需参数，应始终设置为 `true`. |
| `identityRequired` | 布尔值 | 必需 | 设置为 `true` 如果用户应该能够 [身份类型](identity-namespace-configuration.md) 从Experience Platform到您在 `profileFields` 数组。 |

{style="table-layout:auto"}

生成的UI体验如下图所示。

当用户选择目标映射时，他们可以看到 `profileFields` 数组。

![显示目标属性屏幕的UI图像。](../../assets/functionality/destination-configuration/select-attributes.png)

选择属性后，他们可以在目标字段列中看到这些属性。

![显示具有属性的静态Target架构的UI图像](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## 创建动态架构 {#dynamic-schema-configuration}

Destination SDK支持创建动态合作伙伴模式。 与静态架构不同，动态架构不使用 `profileFields` 数组。 动态模式而是使用动态模式服务器，该服务器会连接到您自己的API，从中检索模式配置。

>[!IMPORTANT]
>
>在创建动态架构之前，您必须 [创建动态模式服务器](../../authoring-api/destination-server/create-destination-server.md).

在动态模式配置中， `profileFields` 阵列被替换为 `dynamicSchemaConfig` 中，如下所示。

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| 参数 | 类型 | 必填/可选 | 描述 |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | 字符串 | 必需 | 指示方式 [!DNL Platform] 客户连接到您的目标。 接受的值为 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客户通过描述的任何身份验证方法登录您的系统 [此处](customer-authentication.md). </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe与目标之间存在全局身份验证系统，并且 [!DNL Platform] 客户无需提供任何身份验证凭据即可连接到您的目标。 在这种情况下，您必须 [创建凭据对象](../../credentials-api/create-credential-configuration.md) 使用凭据API。 </li><li>使用 `NONE` 如果向目标平台发送数据时不需要任何身份验证。 </li></ul> |
| `dynamicEnum.destinationServerId` | 字符串 | 必需 | 的 `instanceId` 动态模式服务器的URL。 此目标服务器包括Experience Platform将调用以检索动态架构的API端点。 |
| `dynamicEnum.value` | 字符串 | 必需 | 动态架构的名称，在动态架构服务器配置中定义。 |
| `dynamicEnum.responseFormat` | 字符串 | 必需 | 始终设置为 `SCHEMA` 定义动态架构时。 |
| `profileRequired` | 布尔值 | 可选 | 使用 `true` 如果用户应能够将目标平台上的配置文件属性从Experience Platform映射到自定义属性。 |
| `segmentRequired` | 布尔值 | 必需 | 此参数是Destination SDK的必需参数，应始终设置为 `true`. |
| `identityRequired` | 布尔值 | 必需 | 设置为 `true` 如果用户应该能够 [身份类型](identity-namespace-configuration.md) 从Experience Platform到您在 `profileFields` 数组。 |

{style="table-layout:auto"}

## 必需映射 {#required-mappings}

在架构配置中，除了静态或动态架构之外，您还可以选择添加所需（或预定义）映射。 这些映射是用户能够在Platform UI中查看的映射，但是在设置与目标的连接时，用户无法对其进行修改。

例如，您可以强制将电子邮件地址字段始终发送到目标。

>[!NOTE]
>
>当前支持以下所需映射组合：
>* 您可以配置必填的源字段和必填的目标字段。 在这种情况下，用户无法编辑或选择这两个字段中的任意一个，并且只能查看选择。
>* 您只能配置必需的目标字段。 在这种情况下，将允许用户选择要映射到目标的源字段。
>
> 当前仅配置必需源字段 *not* 受支持。

请参阅下面两个具有所需映射的架构配置示例，以及这些示例在的映射步骤中的显示情况 [将数据激活到批处理目标工作流](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB 所需的源和目标映射]

以下示例显示了所需的源映射和目标映射。 当源字段和目标字段均指定为必需映射时，用户将无法选择或编辑这两个字段中的任意字段，并且只能查看预定义的选择。

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| 参数 | 类型 | 必填/可选 | 描述 |
|---|---|---|---|
| `requiredMappingsOnly` | 布尔值 | 可选 | 如果将此值设置为true，则除了您在 `requiredMappings` 数组。 |
| `requiredMappings.sourceType` | 字符串 | 必需 | 指示 `source` 字段。 支持的值： <ul><li>`text/x.schema-path`:当 `source` 字段是XDM架构中的配置文件属性。</li><li>`text/x.aep-xl`:在 `source` 字段由正则表达式定义。 示例：`iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`:在 `source` 字段。 目前，唯一支持的宏模板是 `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | 字符串 | 必需 | 指示源字段的值。 支持的值类型： <ul><li>XDM配置文件属性。 示例: `personalEmail.address`. 如果源属性是XDM配置文件属性，请将 `sourceType` 参数 `text/x.schema-path`.</li><li>正则表达式. 示例: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. 如果源属性是正则表达式，请将 `sourceType` 参数 `text/x.aep-xl`.</li><li>宏模板。 示例:`metadata.segment.alias`. 如果源属性是宏模板，请将 `sourceType` 参数 `text/plain`. 目前，唯一支持的宏模板是 `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | 字符串 | 必需 | 指示目标字段的值。 如果源字段和目标字段均指定为必需映射，则用户将无法选择或编辑这两个字段中的任意字段，并且只能查看选择。 |

{style="table-layout:auto"}

因此， **[!UICONTROL 源字段]** 和 **[!UICONTROL 目标字段]** Platform UI中的部分呈灰显状态。

![UI激活流程中所需映射的图像。](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB 必需的目标映射]

以下示例显示了所需的目标映射。 如果仅将目标字段指定为必需字段，则用户可以选择要映射到该字段的源字段。

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| 参数 | 类型 | 必填/可选 | 描述 |
|---|---|---|---|
| `requiredMappingsOnly` | 布尔值 | 可选 | 如果将此值设置为true，则除了您在 `requiredMappings` 数组。 |
| `requiredMappings.destination` | 字符串 | 必需 | 指示目标字段的值。 仅指定目标字段时，用户可以选择要映射到目标的源字段。 |
| `mandatoryRequired` | 布尔值 | 可选 | 指示是否应将映射标记为 [强制属性](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | 布尔值 | 可选 | 指示是否应将映射标记为 [重复数据删除键](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

因此， **[!UICONTROL 目标字段]** 部分显示为灰显，而 **[!UICONTROL 源字段]** 区域处于活动状态，且用户可以与之进行交互。 的 **[!UICONTROL 必填项]** 和 **[!UICONTROL 重复数据删除键]** 选项处于活动状态，用户无法更改它们。

![UI激活流程中所需映射的图像。](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## 后续步骤 {#next-steps}

阅读本文后，您应该对Destination SDK支持的架构类型以及如何配置架构有了更深入的了解。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证](customer-authentication.md)
* [OAuth2身份验证](oauth2-authentication.md)
* [UI属性](ui-attributes.md)
* [客户数据字段](customer-data-fields.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批量配置](batch-configuration.md)
* [历史用户档案资格](historical-profile-qualifications.md)