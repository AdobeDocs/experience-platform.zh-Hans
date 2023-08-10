---
title: 身份验证
description: 了解如何为Adobe Experience Platform Edge Network服务器API配置身份验证。
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 2%

---

# 身份验证 {#authentication}

## 概述

此 [!DNL Edge Network Server API] 根据事件源和API收集域，处理经过身份验证和未经身份验证的数据收集。

对于每个请求， [!DNL Server API] 验证数据流 [!DNL access type] 设置。 使用此设置，客户可以配置数据流以接受经过身份验证的数据，或同时接受经过身份验证和未经身份验证的数据。 默认情况下，接受这两种类型的数据。

有关配置数据流访问类型的详细信息，请参阅有关如何配置数据流的文档。 [创建和配置数据流](../datastreams/overview.md#create).

以下是基于数据流的行为摘要 [!DNL Access Type] 配置以及接收请求的端点。

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| 混合（默认） | 不对请求进行身份验证 | 验证请求 |
| 已验证 | 验证请求 | 验证请求 |

来自上的专用服务器的API调用 `server.adobedc.net` 应始终进行身份验证。

## 先决条件 {#prerequisites}

调用之前 [!DNL Server API]，确保您满足以下先决条件：

* 您拥有有权访问Adobe Experience Platform的组织帐户。
* 您的Experience Platform帐户具有 `developer` 和 `user` 为Adobe Experience Platform API产品配置文件启用的角色。 联系 [Admin Console](../access-control/home.md) 管理员为您的帐户启用这些角色。
* 你有Adobe ID。 如果您没有Adobe ID，请转到 [Adobe Developer控制台](https://developer.adobe.com/console) 并创建一个新帐户。

## 收集凭据 {#credentials}

要调用Platform API，您必须先完成 [身份验证教程](../landing/api-authentication.md). 完成身份验证教程将为所有Experience PlatformAPI调用中的每个所需标头提供值，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的资源可以隔离到特定的虚拟沙箱。 在对Platform API的请求中，您可以指定将执行操作的沙盒的名称和ID。 这些是可选参数。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙箱的详细信息，请参阅 [沙盒概述文档](../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* Content-Type: `application/json`

## 配置数据集写入权限 {#dataset-write-permissions}

要配置数据集写入权限，请转到 [Admin Console](https://adminconsole.adobe.com)，找到附加到API密钥的产品配置文件，并设置以下权限：

* 在 [!UICONTROL 沙盒] 部分，选择数据流沙盒。
* 在 [!UICONTROL 数据管理] 部分，选择 **[!UICONTROL 管理数据集]** 许可。

## 授权错误疑难解答 {#troubleshooting-authorization}

| 错误代码 | 错误消息 | 描述 |
| --- | --- | --- |
| `EXEG-0500-401` | 授权令牌无效 | 此错误消息会在以下任意情况下显示：  <ul><li>此 `authorization` 缺少标头值。</li><li>此 `authorization` 标头值不包括必需的 `Bearer` 令牌。</li><li>提供的授权令牌的格式无效。</li><li>数据流需要身份验证，但请求缺少所需的标头。</li></ul> |
| `EXEG-0501-401` | 用户授权令牌无效 | 此错误消息会在以下任意情况下显示： <ul><li>API调用缺少必需的 `x-user-token` 标题。</li><li>提供的用户令牌的格式无效。</li></ul> |
| `EXEG-0502-401` | 授权令牌无效 | 当提供的授权令牌具有有效格式(JWT)，但其签名无效时，会显示此错误消息。 查看 [身份验证教程](../landing/api-authentication.md) 以了解如何获取有效的JWT令牌。 |
| `EXEG-0503-401` | 授权令牌无效 | 提供的授权令牌过期时，会显示此错误消息。 浏览 [身份验证教程](../landing/api-authentication.md) 以生成新令牌。 |
| `EXEG-0504-401` | 缺少所需的产品上下文 | 此错误消息会在以下任意情况下显示：  <ul><li>开发人员帐户无权访问Adobe Experience Platform产品上下文。</li><li>公司帐户尚无权使用AdobeExperience Platform。</li></ul> |
| `EXEG-0505-401` | 缺少所需的授权令牌范围 | 此错误仅适用于服务帐户身份验证。 当调用中包含的服务授权令牌属于无权访问的服务帐户时，将显示错误消息 `acp.foundation` IMS范围。 |
| `EXEG-0506-401` | 无法访问沙盒进行写入 | 当开发人员帐户没有 `WRITE` 访问在其中定义数据流的Experience Platform沙盒。 |
