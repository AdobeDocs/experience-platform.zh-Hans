---
description: 了解如何为使用Destination SDK构建的目标配置目标交付设置，以指示导出数据的去向以及在数据登陆位置使用什么身份验证规则。
title: 目标投放
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 2%

---

# 目标投放

为了更好地控制导出到目标的数据的登陆位置，Destination SDK允许您指定目标投放设置。

目标投放部分指示导出数据的去向，以及在数据登陆位置使用的身份验证规则。

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅[配置选项](../configuration-options.md)文档中的关系图或查看以下目标配置概述页面：

* [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

您可以通过`/authoring/destinations`端点配置目标投放设置。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目标配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介绍了可用于目标的所有受支持目标传送选项。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;**&#x200B;**。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 是 |

## 支持的参数 {#supported-parameters}

配置目标投放设置时，您可以使用下表所述的参数定义导出数据的发送位置。

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `authenticationRule` | 字符串 | 指示[!DNL Experience Platform]应如何连接到您的目标。 支持的值：<ul><li>`CUSTOMER_AUTHENTICATION`：如果Experience Platform客户通过[此处](customer-authentication.md)描述的任何身份验证方法登录到您的系统，请使用此选项。</li><li>`PLATFORM_AUTHENTICATION`：如果Adobe与您的目标之间存在全局身份验证系统，并且[!DNL Experience Platform]客户不需要提供任何身份验证凭据即可连接到您的目标，请使用此选项。 在这种情况下，您必须使用[凭据API](../../credentials-api/create-credential-configuration.md)配置创建凭据对象。 </li><li>`NONE`：如果不需要身份验证即可将数据发送到目标平台，请使用此选项。 </li></ul> |
| `destinationServerId` | 字符串 | 要将数据导出到的[目标服务器](../../authoring-api/destination-server/create-destination-server.md)的`instanceId`。 |
| `deliveryMatchers.type` | 字符串 | <ul><li>为基于文件的目标配置目标投放时，请始终将此项设置为`SOURCE`。</li><li>在为流目标配置目标传递时，`deliveryMatchers`部分不是必需的。</li></ul> |
| `deliveryMatchers.value` | 字符串 | <ul><li>为基于文件的目标配置目标投放时，请始终将此项设置为`batch`。</li><li>在为流目标配置目标传递时，`deliveryMatchers`部分不是必需的。</li></ul> |

{style="table-layout:auto"}

## 流目的地的目标投放设置 {#destination-delivery-streaming}

以下示例显示了应如何为流目标配置目标投放设置。 请注意，流式目标不需要`deliveryMatchers`部分。

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## 基于文件的目标的目标投放设置 {#destination-delivery-file-based}

以下示例显示了应如何为基于文件的目标配置目标投放设置。 请注意，基于文件的目标需要`deliveryMatchers`部分。

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解如何针对流目标和基于文件的目标配置目标应导出数据的位置。

要了解有关其他目标组件的更多信息，请参阅以下文章：

* [客户身份验证](customer-authentication.md)
* [OAuth2授权](oauth2-authorization.md)
* [UI属性](ui-attributes.md)
* [客户数据字段](customer-data-fields.md)
* [架构配置](schema-configuration.md)
* [身份命名空间配置](identity-namespace-configuration.md)
* [支持的映射配置](supported-mapping-configurations.md)
* [受众元数据配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次配置](batch-configuration.md)
* [历史配置文件资格](historical-profile-qualifications.md)
