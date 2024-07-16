---
description: 本页举例说明了用于删除凭据配置Adobe Experience Platform Destination SDK的API调用。
title: 删除凭据配置
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---

# 删除凭据配置

>[!IMPORTANT]
>
>**API终结点**： `platform.adobe.io/data/core/activation/authoring/credentials`

此页面举例说明了API请求和有效负荷，您可以使用`/authoring/credentials` API端点删除凭据配置。

## 何时使用`/credentials` API端点 {#when-to-use}

>[!IMPORTANT]
>
>在大多数情况下，您&#x200B;***不***&#x200B;需要使用`/credentials` API终结点。 您可以改为通过`/destinations`端点的`customerAuthenticationConfigurations`参数配置目标的身份验证信息。
> 
>有关支持的身份验证类型的详细信息，请阅读[客户身份验证配置](../functionality/destination-configuration/customer-authentication.md)。

只有在Adobe和目标平台之间存在全局身份验证系统，并且[!DNL Platform]客户不需要提供任何身份验证凭据即可连接到目标时，才使用此API端点创建凭据配置。 在这种情况下，您必须使用`/credentials` API端点创建凭据配置。

使用全局身份验证系统时，在[创建新的目标配置](../authoring-api/destination-configuration/create-destination-configuration.md)时，必须在[目标投放](../functionality/destination-configuration/destination-delivery.md)配置中设置`"authenticationRule":"PLATFORM_AUTHENTICATION"`。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;****。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 凭据API操作快速入门 {#get-started}

在继续之前，请查看[入门指南](../getting-started.md)以了解成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 删除凭据配置 {#delete}

您可以删除[现有](create-credential-configuration.md)凭据配置，方法是使用要删除的凭据配置的`{INSTANCE_ID}`向`/authoring/credentials`端点发出`DELETE`请求。

要获取现有目标配置及其对应的`{INSTANCE_ID}`，请参阅有关[检索凭据配置](retrieve-credential-configuration.md)的文章。

**API格式**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 要删除的凭据配置的`ID`。 |

以下请求删除由`{INSTANCE_ID}`参数定义的凭据配置。

+++请求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++响应

成功的响应返回HTTP状态200以及空的HTTP响应。

+++

## API错误处理 {#error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅平台疑难解答指南中的[API状态代码](../../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../../landing/troubleshooting.md#request-header-errors)。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何使用`/authoring/credentials` API端点删除凭据配置。 阅读[如何使用Destination SDK配置目标](../guides/configure-destination-instructions.md)，以了解此步骤在配置目标的过程中所处的位置。
