---
title: Didomi Source概述
description: 了解如何使用用户界面将Didomi连接到Adobe Experience Platform。
last-substantial-update: 2025-07-29T00:00:00Z
badge: Beta 版
exl-id: c59bcfb8-e831-4a13-8b0e-4c6d538f1059
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# [!DNL Didomi]

>[!AVAILABILITY]
>
>[!DNL Didomi]源为测试版。 有关使用测试版标记源的更多信息，请阅读源概述中的[条款和条件](../../home.md#terms-and-conditions)。

[!DNL Didomi]是一个同意和偏好设置管理平台，可帮助组织跨网站、应用程序和内部工具收集、管理和强制执行有关个人数据的用户选择。

Adobe Experience Platform支持通过源连接器系统从各种外部系统中摄取数据，包括云存储、数据库和应用程序（如[!DNL Didomi]）。 使用源对外部系统进行身份验证，管理流入Experience Platform的数据，并确保以一致和结构化的方式摄取您的客户数据。

使用[!DNL Didomi]源将来自[!DNL Didomi]同意和偏好管理平台的实时用户同意和偏好设置数据流式传输到Experience Platform中。 通过[!DNL Didomi]源，您可以在Experience Platform中集中并处理同意数据，从而保持客户配置文件和下游工作流符合要求并处于最新状态。

![Didomi数据处理体系结构。](../../images/tutorials/create/didomi/flux.jpeg)

## 先决条件

完成下面列出的先决条件步骤以成功将您的[!DNL Didomi]帐户连接到Experience Platform。

### IP地址允许列表

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[将IP地址列入允许列表到Experience Platform](../../ip-address-allow-list.md)的指南。

### 在Experience Platform上配置权限

您必须同时为您的帐户启用&#x200B;**[!UICONTROL View Sources]**&#x200B;和&#x200B;**[!UICONTROL Manage Sources]**&#x200B;权限，才能将您的[!DNL Didomi]帐户连接到Experience Platform。 请联系您的产品管理员以获取必要的权限。 有关详细信息，请阅读[访问控制UI指南](../../../access-control/ui/overview.md)。

### 收集Adobe API凭据

要安全地将[!DNL Didomi]连接到Experience Platform，您必须使用Adobe API凭据进行身份验证。 这些凭据对于设置webhook和配置数据摄取至关重要。

有关如何成功调用Experience Platform API的信息，请阅读[Experience Platform API快速入门](../../../landing/api-authentication.md)指南。

### 创建Experience Platform架构

>[!TIP]
>
>如果您已经拥有现有的XDM架构，则可以跳过此步骤。

**Experience Data Model (XDM)架构**&#x200B;定义了您将从[!DNL Didomi]发送到Experience Platform的数据的结构（例如，用户ID、同意目的）。

要创建架构，请在Experience Platform UI的左侧导航中选择[!UICONTROL Schemas]，然后选择&#x200B;**[!UICONTROL Create schema]**。 接下来，选择&#x200B;**[!UICONTROL Standard]**&#x200B;作为架构类型，然后选择&#x200B;**[!UICONTROL Manual]**&#x200B;以手动创建字段。 为您的架构选择基类并提供架构的名称。

创建后，通过添加任何必填字段来更新架构。 确保至少一个字段是[!UICONTROL Identity]字段，以通知Experience Platform您的主要标识值。 最后，确保启用[!UICONTROL Profile]切换功能，以便成功存储您的数据。

![create-schema](../../images/tutorials/create/didomi/create-schema.png)

有关详细信息，请参阅[在UI中创建架构](../../../xdm/tutorials/create-schema-ui.md)指南。

### 创建数据集

>[!TIP]
>
>如果您已经拥有现有数据集，则可以跳过此步骤。

Experience Platform中的&#x200B;**数据集**&#x200B;用于根据您定义的架构存储传入数据。

要创建数据集，请在Experience Platform UI的左侧导航中选择[!UICONTROL Datasets]，然后选择&#x200B;**[!UICONTROL Create dataset]**。 接下来，选择&#x200B;**[!UICONTROL Create dataset from schema]**，然后选择要与新数据集关联的架构。

![创建数据集](../../images/tutorials/create/didomi/create-dataset.png)

## 在[!DNL Didomi]控制台上配置HTTP Webhook

[!DNL Webhooks]允许您订阅用户与其同意首选项交互时在[!DNL Didomi]平台上触发的事件。 当发生相关事件时 — 例如，当用户给予或撤销同意时 — [!DNL Didomi]向配置的[!DNL webhook]端点发送包含JSON有效负载的实时HTTP POST请求。

![didomi-console](../../images/tutorials/create/didomi/didomi-console.png)

要确保与Experience Platform兼容，您的webhook必须满足以下要求。

| 字段 | 描述 | 示例 |
| --- | --- | --- | 
| 客户端密码 | 与您的Adobe API凭据关联的密钥。 | `d8f3b2e1-4c9a-4a7f-9b2e-8f1c3d2a1b6e` |
| API密钥 | 用于对Adobe服务的请求进行身份验证的公共API密钥。 |  |
| 授权类型 | 应用程序从授权服务器获取访问令牌的方法。 将此值设置为`client_credentials`。 | `client_credentials` |
| 范围 | 授权范围定义应用程序向API提供程序请求的特定权限或访问级别。 | `openid,AdobeID,read_organizations,additional_info.projectedProductContext,session` |
| 身份验证标头 | Adobe令牌请求所需的其他标头。 | `{"Content-type": "application/x-www-form-urlencoded"}` |
| 令牌URL | 您的Adobe令牌端点。 | `https://ims-na1.adobelogin.com/ims/token/v3` |
| 端点 URL | 最终Adobe连接器URL（在设置结束时提供）。 | `https://dcs.adobedc.net/collection/your-adobe-endpoint-id` |

{style="table-layout:auto"}

接下来，为您的[!DNL webhook]配置以下选项。

| 字段 | 描述 | 值 |
| ---| --- | --- | 
| 请求标头 | [!DNL webhook]的自定义标头。 确保包括`x-adobe-flow-id`。 您可以在创建[数据流](../../tutorials/ui/create/consent-and-preferences/didomi.md#retrieve-the-streaming-endpoint-url)后检索此值。 | `{"Content-Type": "application/json", "Cache-Control": "no-cache", "x-adobe-flow-id": "{DATAFLOW_ID}"}` |
| Flatten | 必须检查此属性，因为它确保[!DNL webhook]数据作为平面对象发送。 | 已启用 |
| 事件类型 | 选择应触发[!DNL Didomi]的特定`event.*`事件组（`user.*`或[!DNL webhook]）。 使用`event.*`跟踪同意或首选项更改，并使用`user.*`跟踪用户配置文件更新。 需要选择此项以确保仅向Adobe发送兼容的事件。 Adobe仅支持每个数据流一个架构，因此选择这两种事件类型可能会导致摄取错误。 | 支持的事件类型列表包括： <ul><li>`Event.created`</li><li>`Event.updated`</li><li>`Event.deleted`</li><li>`User.created`</li><li>`User.updated`</li><li>`User.deleted`</li></ul> |

### 下载示例有效负载文件 {#download-the-sample-payload-file}

根据您选择的事件组，直接从&#x200B;**控制台下载相应的**&#x200B;示例有效负载文件[!DNL Didomi]。 此文件代表数据的结构，将在Adobe的架构和映射步骤中使用。

| **事件组** | **要下载的样本文件** | **筛选选项** |
| --- | ---| --- |
| `event.*` | 下载`event.created`的示例 | 仅筛选`event.*`事件 |
| `user.*` | 下载`user.created`的示例 | 仅筛选`user.*`事件 |

## 将您的[!DNL Didomi]帐户连接到Experience Platform

阅读有关[连接 [!DNL Didomi] 到Experience Platform](../../tutorials/ui/create/consent-and-preferences/didomi.md)的指南，了解如何创建源连接并将[!DNL Didomi]中的同意和偏好设置数据摄取到Experience Platform。
