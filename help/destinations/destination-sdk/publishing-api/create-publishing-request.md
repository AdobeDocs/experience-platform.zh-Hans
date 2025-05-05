---
description: 了解如何设置API调用的格式，以通过Adobe Experience Platform Destination SDK提交目标发布请求。
title: 创建目标发布请求
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# 创建目标发布请求

>[!IMPORTANT]
>
>只有在提交由其他Experience Platform客户使用的生产（公共）目标时，才需要使用此API端点。 如果您正在创建供自己使用的专用目标，则无需使用发布API正式提交目标。

>[!IMPORTANT]
>
>**API终结点**： `platform.adobe.io/data/core/activation/authoring/destinations/publish`

配置和测试目标后，可将其提交到Adobe进行审查和发布。 请阅读[在Destination SDK](../guides/submit-destination.md)中编写的目标提交以进行审核，了解作为目标提交流程的一部分而必须执行的所有其他步骤。

在以下情况下，使用发布目标API端点提交发布请求：

* 作为Destination SDK合作伙伴，您希望使您的产品化目标在所有Experience Platform组织中均可用，以供所有Experience Platform客户使用；
* 您对配置进行了&#x200B;*任何更新*。 只有在提交新的发布请求(经Experience Platform团队批准)后，配置更新才会反映在目标中。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;**&#x200B;**。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 目标发布API操作快速入门 {#get-started}

在继续之前，请查看[入门指南](../getting-started.md)以了解成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 提交目标配置以进行发布 {#create}

您可以通过向`/authoring/destinations/publish`端点发出POST请求来提交要发布的目标配置。

**API格式**

```http
POST /authoring/destinations/publish
```

+++请求

以下请求跨由有效负载中提供的参数配置的组织提交发布目标。 以下有效负载包含`/authoring/destinations/publish`终结点接受的所有参数。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `destinationId` | 字符串 | 您要提交以进行发布的目标配置的目标ID。 使用[检索目标配置](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API调用获取目标配置的目标ID。 |
| `destinationAccess` | 字符串 | 使用`ALL`让您的目标显示在所有Experience Platform客户的目录中。 |

{style="table-layout:auto"}

+++

+++响应

成功的响应会返回HTTP状态201以及目标发布请求的详细信息。

+++

## API错误处理

Destination SDK API端点遵循常规Experience Platform API错误消息原则。 请参阅Experience Platform疑难解答指南中的[API状态代码](../../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../../landing/troubleshooting.md#request-header-errors)。

## 后续步骤

阅读本文档后，您现在知道如何提交目标的发布请求。 Adobe Experience Platform团队将在五个工作日内审查您的发布请求并回复您。
