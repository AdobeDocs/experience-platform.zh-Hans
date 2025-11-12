---
title: PathFactory Source概述
description: 了解如何使用API或用户界面将PathFactory连接到Adobe Experience Platform。
last-substantial-update: 2024-04-30T00:00:00Z
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 3%

---

# [!DNL PathFactory]

[[!DNL PathFactory]](https://www.pathfactory.com/)提供了一个基于云的平台，可帮助企业管理内容历程并通过智能内容见解促进参与。 本指南详细介绍如何利用PathFactory的连接器将数据从PathFactory集成到Experience Platform中，以实现最佳数据摄取。

您可以使用三个主要源从[[!DNL PathFactory]](https://www.pathfactory.com/)中摄取数据：

* **[!DNL Visitors]**：将客户和联系人数据作为记录摄取，以便更好地了解您的受众。
* **[!DNL Sessions]**：跟踪您的平台上各个用户会话活动的时间序列事件。
* **[!DNL Page Views]**：时间序列事件，用于深入分析正在查看的页面，帮助您分析内容性能。

请阅读下面的文档，了解有关如何设置[!DNL PathFactory]源帐户的信息。

## IP地址允许列表 {#ip-allow-list}

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[将IP地址列入允许列表到Experience Platform](../../ip-address-allow-list.md)的指南。

## 先决条件 {#prerequisites}

开始将[[!DNL PathFactory]](https://www.pathfactory.com/)连接器与Experience Platform集成之前，请确保满足以下先决条件：

* **一个[PathFactory帐户]**。
   * 如果您还没有有效的帐户，请联系[[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml)。
* **任何**&#x200B;产品的活动订阅[!DNL PathFactory]。
* **用户名、密码和域**。
   * 需要这些凭据才能访问您的[!DNL PathFactory]帐户及其数据。
* **访问令牌**&#x200B;和&#x200B;**API端点**。
   * 这些是连接[!DNL PathFactory] API所必需的。

### 如何获取凭据和访问令牌 {#gather-credentials}

要将[!DNL PathFactory]连接到Experience Platform，您必须提供以下凭据：

| 凭据 | 描述 | 终结点 |
| --- | --- | --- |
| 用户名 | 您的[!DNL PathFactory]帐户用户名。 | 不适用 |
| 密码 | 您的[!DNL PathFactory]帐户密码。 | 不适用 |
| 域 | 与您的[!DNL PathFactory]帐户关联的域。 | 不适用 |
| 访问令牌 | 用于API身份验证的唯一令牌。 | 不适用 |
| 访客端点 | 访客数据的API端点。 | `/api/public/v3/data_lake_apis/visitors.json` |
| 会话端点 | 会话数据的API端点。 | `/api/public/v3/data_lake_apis/sessions.json` |
| 页面查看端点 | 页面查看数据的API端点。 | `/api/public/v3/data_lake_apis/page_views.json` |

有关如何获取用户名、密码、域和访问令牌的详细说明，请访问[[!DNL PathFactory] 支持中心](https://support.pathfactory.com/categories/adobe/)。 此资源提供有关检索和管理凭据的全面指南。

### 在Experience Platform上配置权限

您必须同时为您的帐户启用&#x200B;**[!UICONTROL View Sources]**&#x200B;和&#x200B;**[!UICONTROL Manage Sources]**&#x200B;权限，才能将您的[!DNL PathFactory]帐户连接到Experience Platform。 请联系您的产品管理员以获取必要的权限。 有关详细信息，请阅读[访问控制UI指南](../../../access-control/ui/overview.md)。

## 将[!DNL PathFactory]连接到Experience Platform {#pathfactory-connect}

以下文档提供了有关如何使用API或用户界面将[!DNL PathFactory]连接到Experience Platform的信息：

* [创建源连接和数据流以使用API将 [!DNL PathFactory] 数据引入Experience Platform](../../tutorials/api/create/marketing-automation/pathfactory.md)。
* 使用UI [将您的 [!DNL PathFactory] 帐户连接到Experience Platform](../../tutorials/ui/create/marketing-automation/pathfactory.md)。
* [使用UI](../../tutorials/ui/dataflow/marketing-automation.md)为源连接创建数据流。
