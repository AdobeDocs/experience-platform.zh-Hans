---
description: 了解如何为使用Destination SDK构建的目标配置合作伙伴架构。
title: 合作伙伴架构配置
exl-id: 0548e486-206b-45c5-8d18-0d6427c177c5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 3%

---

# 合作伙伴架构配置

Experience Platform使用架构，以一致且可重用的方式描述数据结构。 当数据被摄取到Experience Platform中时，它会根据XDM架构进行构建。 有关架构组合模型的更多信息，包括设计原则和最佳实践，请参阅架构组合的[基础知识](../../../../xdm/schema/composition.md)。

使用Destination SDK构建目标时，您可以定义自己的合作伙伴架构以供目标平台使用。 这样，用户便能够将配置文件属性从Experience Platform映射到目标平台可识别的特定字段，并且所有这些字段均位于Experience Platform UI中。

在为目标配置合作伙伴架构时，您可以优化目标平台支持的字段映射，例如：

* 允许用户将`phoneNumber` XDM属性映射到目标平台支持的`phone`属性。
* 创建动态合作伙伴架构，Experience Platform可以动态调用这些架构以检索目标中所有受支持属性的列表。
* 定义目标平台所需的必填字段映射。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅[配置选项](../configuration-options.md)文档中的关系图，或参阅如何[使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)的指南。

您可以通过`/authoring/destinations`端点配置架构设置。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持的架构配置选项，并显示了客户将在Experience Platform UI中看到的内容。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;****。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 是 |

## 支持的架构配置 {#supported-schema-types}

Destination SDK支持多种架构配置：

* 静态架构是通过`profileFields`部分中的`schemaConfig`数组定义的。 在静态架构中，您定义了`profileFields`数组中应显示在Experience Platform UI中的每个目标属性。 如果需要更新架构，您必须[更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)。
* 动态架构使用名为[动态架构服务器](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers)的其他目标服务器类型来动态检索支持的目标属性，并根据您自己的API生成架构。 动态架构不使用`profileFields`数组。 如果需要更新架构，则无需[更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)。 动态架构服务器而是从API中检索更新的架构。
* 在架构配置中，您可以选择添加所需的（或预定义的）映射。 用户可以在Experience Platform UI中查看这些映射，但在设置与目标的连接时，无法修改它们。 例如，您可以强制电子邮件地址字段始终发送到目标。

`schemaConfig`部分根据所需的架构类型使用多个配置参数，如下部分所示。

## 创建静态架构 {#attributes-schema}

要创建具有配置文件属性的静态架构，请在`profileFields`数组中定义目标属性，如下所示。

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
      "identityRequired":true,
      "segmentNamespaceAllowList": ["someNamespace"],
      "segmentNamespaceDenyList": ["someOtherNamespace"]

}
```

| 参数 | 类型 | 必需/可选 | 描述 |
|---------|----------|------|---|
| `profileFields` | 数组 | 可选 | 定义目标平台接受的目标属性数组，客户可以将其配置文件属性映射到这些目标属性。 使用`profileFields`数组时，可以完全省略`useCustomerSchemaForAttributeMapping`参数。 |
| `useCustomerSchemaForAttributeMapping` | 布尔值 | 可选 | 启用或禁用从客户架构到您在`profileFields`数组中定义的属性的映射。 <ul><li>如果设置为`true`，则用户仅在映射字段中看到源列。 `profileFields`不适用于这种情况。</li><li>如果设置为`false`，则用户可以将源属性从其架构映射到您在`profileFields`数组中定义的属性。</li></ul> 默认值为 `false`。 |
| `profileRequired` | 布尔值 | 可选 | 如果用户应能够将Experience Platform中的配置文件属性映射到目标平台上的自定义属性，则使用`true`。 |
| `segmentRequired` | 布尔值 | 必需 | Destination SDK需要此参数，应始终将其设置为`true`。 |
| `identityRequired` | 布尔值 | 必需 | 如果用户应该能够将Experience Platform中的`true`标识类型[映射到您在](identity-namespace-configuration.md)数组中定义的属性，则设置为`profileFields`。 |
| `segmentNamespaceAllowList` | 数组 | 可选 | 允许用户仅将受众从数组中定义的受众命名空间映射到目标。 <br><br>在大多数情况下不建议使用此参数。 请改用`"segmentNamespaceDenyList":[]`以允许将所有类型的受众导出到您的目标。 <br><br>如果您的配置中同时缺少`segmentNamespaceAllowList`和`segmentNamespaceDenyList`，则用户将只能导出源自[分段服务](../../../../segmentation/home.md)的受众。 <br><br>`segmentNamespaceAllowList`和`segmentNamespaceDenyList`互斥。 |
| `segmentNamespaceDenyList` | 数组 | 可选 | 限制用户将受众从数组中定义的受众命名空间映射到目标。 <br><br>Adobe建议通过设置`"segmentNamespaceDenyList":[]`允许导出所有受众，而不考虑其来源。 <br><br>**重要信息：**&#x200B;如果您未在`segmentNamespaceDenyList`中指定`schemaConfig`并且未使用`segmentNamespaceAllowList`，则系统会自动将`segmentNamespaceDenyList`设置为`[]`。 这样可以防止将来丢失自定义受众。 为安全起见，Adobe建议在您的配置中明确设置`"segmentNamespaceDenyList":[]`。 <br><br>`segmentNamespaceAllowList`和`segmentNamespaceDenyList`互斥。 |

{style="table-layout:auto"}

生成的UI体验如下图所示。

当用户选择目标映射时，他们可以看到`profileFields`数组中定义的字段。

![显示目标属性屏幕的UI图像。](../../assets/functionality/destination-configuration/select-attributes.png)

选择属性后，他们可以在目标字段列中看到这些属性。

![UI图像显示具有属性的静态目标架构](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## 创建动态架构 {#dynamic-schema-configuration}

Destination SDK支持创建动态合作伙伴架构。 与静态架构相反，动态架构不使用`profileFields`数组。 动态架构会改用动态架构服务器，该服务器会连接到您自己的API，并在其中检索架构配置。

>[!IMPORTANT]
>
>在创建动态架构之前，必须[创建动态架构服务器](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers)。

在动态架构配置中，`profileFields`数组已由`dynamicSchemaConfig`部分替换，如下所示。

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

| 参数 | 类型 | 必需/可选 | 描述 |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | 字符串 | 必需 | 指示[!DNL Experience Platform]客户如何连接到您的目标。 接受的值为`CUSTOMER_AUTHENTICATION`、`PLATFORM_AUTHENTICATION`、`NONE`。<br> <ul><li>如果Experience Platform客户通过`CUSTOMER_AUTHENTICATION`此处[描述的任何身份验证方法登录您的系统，请使用](customer-authentication.md)。 </li><li> 如果Adobe与您的目标之间存在全局身份验证系统，并且`PLATFORM_AUTHENTICATION`客户不需要提供任何身份验证凭据即可连接到您的目标，则使用[!DNL Experience Platform]。 在这种情况下，您必须使用凭据API [创建凭据对象](../../credentials-api/create-credential-configuration.md)，并在`authenticationId`目标投放[配置的](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication)参数中传递凭据对象的ID。 </li><li>如果不需要身份验证即可将数据发送到目标平台，请使用`NONE`。 </li></ul> |
| `dynamicEnum.destinationServerId` | 字符串 | 必需 | 动态架构服务器的`instanceId`。 此目标服务器包括Experience Platform将调用以检索动态架构的API端点。 |
| `dynamicEnum.value` | 字符串 | 必需 | 动态架构的名称，如动态架构服务器配置中所定义。 |
| `dynamicEnum.responseFormat` | 字符串 | 必需 | 定义动态架构时，始终设置为`SCHEMA`。 |
| `profileRequired` | 布尔值 | 可选 | 如果用户应能够将Experience Platform中的配置文件属性映射到目标平台上的自定义属性，则使用`true`。 |
| `segmentRequired` | 布尔值 | 必需 | Destination SDK需要此参数，应始终将其设置为`true`。 |
| `identityRequired` | 布尔值 | 必需 | 如果用户应该能够将Experience Platform中的`true`标识类型[映射到您在](identity-namespace-configuration.md)数组中定义的属性，则设置为`profileFields`。 |

{style="table-layout:auto"}

## 必需的映射 {#required-mappings}

在架构配置中，除了静态或动态架构外，您还可以选择添加所需的（或预定义的）映射。 用户可以在Experience Platform UI中查看这些映射，但在设置与目标的连接时，无法修改它们。

例如，您可以强制电子邮件地址字段始终发送到目标。

>[!NOTE]
>
>当前支持以下必需的映射组合：
>
>* 您可以配置必填源字段和必填目标字段。 在这种情况下，用户无法编辑或选择这两个字段中的任何一个，并且只能查看所选内容。
>* 您只能配置必需的目标字段。 在这种情况下，允许用户选择要映射到目标的源字段。
>
> 仅配置必需源字段当前是&#x200B;*不支持*。

请参阅下面的两个架构配置示例，其中包含所需的映射，以及在[将数据激活到批处理目标工作流](../../../ui/activate-batch-profile-destinations.md)的映射步骤中这些配置的外观。


>[!BEGINTABS]

>[!TAB 必需的源和目标映射]

以下示例显示了所需的源映射和目标映射。 当源字段和目标字段均指定为必需映射时，用户无法选择或编辑这两个字段中的任何一个，并且只能查看预定义的选择。

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

| 参数 | 类型 | 必需/可选 | 描述 |
|---|---|---|---|
| `requiredMappingsOnly` | 布尔值 | 可选 | 当此项设置为true时，除了您在`requiredMappings`数组中定义的必需映射之外，用户无法映射激活流中的其他属性和身份。 |
| `requiredMappings.sourceType` | 字符串 | 必需 | 指示`source`字段的类型。 支持的值： <ul><li>`text/x.schema-path`：当`source`字段是XDM架构中的配置文件属性时使用此值。</li><li>`text/x.aep-xl`：当您的`source`字段由正则表达式定义时，使用此值。 示例：`iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`：当您的`source`字段由宏模板定义时，使用此值。 当前，唯一支持的宏模板是`metadata.segment.alias`。</li></ul> |
| `requiredMappings.source` | 字符串 | 必需 | 指示源字段的值。 支持的值类型： <ul><li>XDM配置文件属性。 示例： `personalEmail.address`。 当源属性是XDM配置文件属性时，将`sourceType`参数设置为`text/x.schema-path`。</li><li>正则表达式。 示例： `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`。 当源属性为正则表达式时，将`sourceType`参数设置为`text/x.aep-xl`。</li><li>宏模板。 示例： `metadata.segment.alias`。 当源属性是宏模板时，将`sourceType`参数设置为`text/plain`。 当前，唯一支持的宏模板是`metadata.segment.alias`。</li></ul> |
| `requiredMappings.destination` | 字符串 | 必需 | 指示目标字段的值。 当源字段和目标字段均指定为必需映射时，用户无法选择或编辑这两个字段中的任何一个，并且只能查看所选内容。 |

{style="table-layout:auto"}

因此，Experience Platform UI中的&#x200B;**[!UICONTROL Source field]**&#x200B;和&#x200B;**[!UICONTROL Target field]**&#x200B;部分均呈灰显状态。

![UI激活流程中所需映射的图像。](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB 必需的目标映射]

以下示例显示了所需的目标映射。 如果仅将目标字段指定为必填字段，则用户可以选择要映射到它的源字段。

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

| 参数 | 类型 | 必需/可选 | 描述 |
|---|---|---|---|
| `requiredMappingsOnly` | 布尔值 | 可选 | 当此项设置为true时，除了您在`requiredMappings`数组中定义的必需映射之外，用户无法映射激活流中的其他属性和身份。 |
| `requiredMappings.destination` | 字符串 | 必需 | 指示目标字段的值。 当仅指定目标字段时，用户可以选择要映射到目标的源字段。 |
| `mandatoryRequired` | 布尔值 | 可选 | 指示映射是否应标记为[必需属性](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes)。 |
| `primaryKeyRequired` | 布尔值 | 可选 | 指示映射是否应标记为[重复数据删除键](../../../ui/activate-batch-profile-destinations.md#deduplication-keys)。 |

{style="table-layout:auto"}

因此，Experience Platform UI中的&#x200B;**[!UICONTROL Target field]**&#x200B;部分呈灰显状态，而&#x200B;**[!UICONTROL Source field]**&#x200B;部分处于活动状态，用户可以与其进行交互。 **[!UICONTROL Mandatory key]**&#x200B;和&#x200B;**[!UICONTROL Deduplication key]**&#x200B;选项处于活动状态，用户无法更改它们。

![UI激活流程中所需映射的图像。](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## 配置对外部受众的支持 {#external-audiences}

要将您的目标配置为支持激活[外部生成的受众](../../../../segmentation/ui/audience-portal.md#import-audience)，请在`schemaConfig`部分中包含以下代码片段。

```json
"schemaConfig": {
  "segmentNamespaceDenyList": [],
  ...
}
```

请参阅本页上面[表](#attributes-schema)中的属性说明，了解有关`segmentNamespaceDenyList`功能的更多信息。

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解Destination SDK支持哪些架构类型，以及如何配置架构。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证](customer-authentication.md)
* [OAuth2授权](oauth2-authorization.md)
* [UI属性](ui-attributes.md)
* [客户数据字段](customer-data-fields.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [目标投放](destination-delivery.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次配置](batch-configuration.md)
* [历史配置文件资格](historical-profile-qualifications.md)
