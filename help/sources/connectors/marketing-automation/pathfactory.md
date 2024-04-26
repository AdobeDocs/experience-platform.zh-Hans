---
title: PathFactory源概述
description: 了解如何使用API或用户界面将PathFactory连接到Adobe Experience Platform。
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta 版
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---

# [!DNL PathFactory]

>[!NOTE]
>
>此 [!DNL PathFactory] 源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

[[!DNL PathFactory]](https://www.pathfactory.com/) 提供了一个基于云的平台，可帮助企业管理内容历程并通过智能内容见解推动参与。 本指南详细介绍如何利用PathFactory的连接器将来自PathFactory的数据集成到Experience Platform中，以实现最佳数据摄取。

您可以从以下位置摄取数据 [[!DNL PathFactory]](https://www.pathfactory.com/) 使用三个主要源：

* **[!DNL Visitors]**：将客户和联系人数据作为记录摄取，以更好地了解您的受众。
* **[!DNL Sessions]**：跟踪您的平台上各个用户会话活动的时间系列事件。
* **[!DNL Page Views]**：提供有关查看了哪些页面的洞察信息并帮助您分析内容性能的时间系列事件。

请阅读下面的文档，了解如何设置 [!DNL PathFactory] 源帐户。

## IP地址允许列表 {#ip-allow-list}

在使用源连接器之前，可能需要将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

## 先决条件 {#prerequisites}

开始集成之前 [[!DNL PathFactory]](https://www.pathfactory.com/) 连接器的Experience Platform，请确保您满足以下先决条件：

* **A [PathFactory帐户]**.
   * 联系人 [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) 如果您还没有有效的帐户。
* **有效的订阅** 到任意 [!DNL PathFactory] 产品。
* **用户名、密码和域**.
   * 需要这些凭据才能访问您的 [!DNL PathFactory] 帐户及其数据。
* **访问令牌** 和 **API端点**.
   * 这些是连接所必需的 [!DNL PathFactory] API。

### 如何获取凭据和访问令牌 {#gather-credentials}

连接 [!DNL PathFactory] 要Experience Platform，必须提供以下凭据：

| 凭据 | 描述 | 端点 |
| --- | --- | --- |
| 用户名 | 您的 [!DNL PathFactory] 帐户用户名。 | 不适用 |
| 密码 | 您的 [!DNL PathFactory] 帐户密码。 | 不适用 |
| 域 | 与您的关联的域 [!DNL PathFactory] 帐户。 | 不适用 |
| 访问令牌 | 用于API身份验证的唯一令牌。 | 不适用 |
| 访客端点 | 访客数据的API端点。 | `/api/public/v3/data_lake_apis/visitors.json` |
| 会话端点 | 会话数据的API端点。 | `/api/public/v3/data_lake_apis/sessions.json` |
| 页面查看端点 | 页面查看数据的API端点。 | `/api/public/v3/data_lake_apis/page_views.json` |

有关如何获取用户名、密码、域和访问令牌的详细说明，请访问 [[!DNL PathFactory] 支持中心](https://support.pathfactory.com/categories/adobe/). 此资源提供有关检索和管理凭据的全面指南。

### 配置Experience Platform权限

您必须同时拥有两者 **[!UICONTROL 查看源]** 和 **[!UICONTROL 管理源]** 为您的帐户启用的权限以连接 [!DNL PathFactory] 帐户到Experience Platform。 请联系您的产品管理员以获取必要的权限。 欲知更多信息，请参阅 [访问控制UI指南](../../../access-control/ui/overview.md).

## 连接 [!DNL PathFactory] 目标平台 {#pathfactory-connect}

以下文档提供了有关如何连接的信息 [!DNL PathFactory] 使用API或用户界面连接到Platform：

* [创建源连接和数据流以引入 [!DNL PathFactory] 使用API将数据发送到平台](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [连接您的 [!DNL PathFactory] 要使用UIExperience Platform的帐户](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [使用用户界面为源连接创建数据流](../../tutorials/ui/dataflow/marketing-automation.md).
