---
description: 了解如何设置API调用的格式，以通过Adobe Experience Platform Destination SDK提交目标发布请求。
title: 创建目标发布请求
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---


# 创建目标发布请求

>[!IMPORTANT]
>
>只有在提交要由其他Experience Platform客户使用的生产（公共）目标时，才需要使用此API端点。 如果要创建供自己使用的专用目标，则无需使用发布API正式提交目标。

>[!IMPORTANT]
>
>**API端点**： `platform.adobe.io/data/core/activation/authoring/destinations/publish`

配置并测试目标后，可将其提交到Adobe进行审查和发布。 读取 [提交供审核在Destination SDK中创作的目标](../guides/submit-destination.md) 对于所有其他步骤，您必须在目标提交流程中执行。

在以下情况下，使用发布目标API端点提交发布请求：

* 作为Destination SDK合作伙伴，您希望使您的产品化目标在所有Experience Platform组织中都可供所有Experience Platform客户使用；
* 您制作 *任何更新* 到您的配置。 只有在提交新发布请求(经Experience Platform团队批准)后，配置更新才会反映在目标中。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免区分大小写错误，请完全按照文档中所示使用参数名称和值。

## 目标发布API操作快速入门 {#get-started}

在继续之前，请查看 [快速入门指南](../getting-started.md) 要成功调用API需要了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 提交目标配置以进行发布 {#create}

您可以通过向以下网站发出POST请求，提交要发布的目标配置 `/authoring/destinations/publish` 端点。

**API格式**

```http
POST /authoring/destinations/publish
```

+++请求

以下请求在由有效负载中提供的参数配置的组织间提交发布目标。 以下有效负载包含由接受的所有参数 `/authoring/destinations/publish` 端点。

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
| `destinationId` | 字符串 | 您要提交以进行发布的目标配置的目标ID。 使用获取目标配置的目标ID [检索目标配置](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API调用。 |
| `destinationAccess` | 字符串 | 使用 `ALL` ，以便您的目标显示在所有Experience Platform客户的目录中。 |

{style="table-layout:auto"}

+++响应

成功的响应会返回HTTP状态201以及目标发布请求的详细信息。

## API错误处理

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中的。

## 后续步骤

阅读本文档后，您现在知道如何提交目标的发布请求。 Adobe Experience Platform团队将在五个工作日内审核您的发布请求并回复您。