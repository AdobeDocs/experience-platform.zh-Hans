---
description: 本页举例说明了用于通过Adobe Experience Platform Destination SDK检索凭据配置的API调用。
title: 检索凭据配置
exl-id: cec55073-6e2f-4412-a9dd-1aeb445279c0
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 检索凭据配置

>[!IMPORTANT]
>
>**API终结点**： `platform.adobe.io/data/core/activation/authoring/credentials`

此页面举例说明了API请求和有效负荷，您可以使用`/authoring/credentials` API端点检索凭据配置。

## 何时使用`/credentials` API端点 {#when-to-use}

>[!IMPORTANT]
>
>在大多数情况下，您&#x200B;***不***&#x200B;需要使用`/credentials` API终结点。 您可以改为通过`customerAuthenticationConfigurations`端点的`/destinations`参数配置目标的身份验证信息。
> 
>有关支持的身份验证类型的详细信息，请阅读[客户身份验证配置](../functionality/destination-configuration/customer-authentication.md)。

仅当在Adobe与目标平台之间存在全局身份验证系统，并且[!DNL Experience Platform]客户不需要提供任何身份验证凭据即可连接到目标时，才使用此API端点创建凭据配置。 在这种情况下，您必须使用`/credentials` API端点创建凭据配置。

使用全局身份验证系统时，在`"authenticationRule":"PLATFORM_AUTHENTICATION"`创建新的目标配置[时，必须在](../functionality/destination-configuration/destination-delivery.md)目标投放[配置中设置](../authoring-api/destination-configuration/create-destination-configuration.md)。 然后，您必须创建[凭据配置](../credentials-api/create-credential-configuration.md)，并在`authenticationId`目标投放[配置中的](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication)参数中传递凭据对象的ID。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;**&#x200B;**。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 凭据API操作快速入门 {#get-started}

在继续之前，请查看[入门指南](../getting-started.md)以了解成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 检索凭据配置 {#retrieve}

您可以通过向[端点发出](create-credential-configuration.md)请求来检索`GET`现有`/authoring/credentials`凭据配置。

**API格式**

使用以下API格式检索帐户的所有凭据配置。

```http
GET /authoring/credentials
```

使用以下API格式检索由`{INSTANCE_ID}`参数定义的特定凭据配置。

```http
GET /authoring/credentials/{INSTANCE_ID}
```

以下两个请求检索您的IMS组织的所有凭据配置，或特定的凭据配置，具体取决于您在请求中是否传递`INSTANCE_ID`参数。

选择下面的每个选项卡以查看相应的有效负载。

>[!BEGINTABS]

>[!TAB 检索所有凭据配置]

+++请求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++响应

成功的响应返回HTTP状态200，其中包含您有权访问的凭据配置列表，该列表基于您使用的[!DNL IMS Org ID]和沙盒名称。 一个`instanceId`对应于一个凭据配置。

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB 检索特定的凭据配置]

+++请求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要检索的凭据配置的ID。 |

+++

+++响应

成功的响应返回HTTP状态200，其中包含与请求中提供的`instanceId`对应的凭据配置详细信息。

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## API错误处理 {#error-handling}

Destination SDK API端点遵循常规Experience Platform API错误消息原则。 请参阅Experience Platform疑难解答指南中的[API状态代码](../../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../../landing/troubleshooting.md#request-header-errors)。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何使用`/authoring/credentials` API端点检索有关凭据配置的详细信息。 阅读[如何使用Destination SDK配置您的目标](../guides/configure-destination-instructions.md)，以了解此步骤在配置目标的过程中所处的位置。
