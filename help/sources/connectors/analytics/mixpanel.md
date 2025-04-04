---
title: Mixpanel Source连接器概述
description: 了解如何使用API或用户界面将Mixpanel连接到Adobe Experience Platform。
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# [!DNL Mixpanel]

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方Analytics应用程序中摄取数据。 对Analytics提供商的支持包括[!DNL Mixpanel]。

[[!DNL Mixpanel]](https://www.mixpanel.com)是一种产品分析工具，它允许您捕获有关用户如何与数字产品交互的数据。 Mixpanel允许您使用简单的交互式报表分析此产品数据，通过单击几下即可查询和可视化数据。

源使用[Mixpanel Event Export API > Download](https://developer.mixpanel.com/reference/raw-event-export)来下载在[!DNL Mixpanel]中接收并存储的事件数据，以及所有事件属性（包括`distinct_id`）和将事件发送到Experience Platform的确切时间戳。 Mixpanel使用持有者令牌作为身份验证机制，与Mixpanel事件导出API通信。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

## 验证您的[!DNL Mixpanel]帐户

本节概述验证您的帐户并将您的[!DNL Mixpanel]数据提交到Experience Platform需要完成的先决步骤。

为了创建[!DNL Mixpanel]源连接和数据流，您必须首先拥有有效的[!DNL Mixpanel]帐户。 如果您没有有效的[!DNL Mixpanel]帐户，请查看[Mixpanel注册表](https://mixpanel.com/register/)页面以创建您的帐户。

成功创建[!DNL Mixpanel]帐户后，导航到[!DNL Mixpanel] UI的[!DNL Project Seettings]页面中的[!DNL Project Details]选项卡，以检索您的项目ID并配置您的时区。

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

接下来，在[!DNL Mixpanel] UI中导航到[!DNL Project Settings]页面中的[!DNL Service Accounts]选项卡，以检索您的服务帐户凭据。

>[!TIP]
>
>要获得最佳实践，请选择[未过期](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration)的服务帐户。

![Mixpanel服务帐户](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

最后，创建[!DNL Mixpanel Event Export API]所需的Experience Platform [架构](../../../xdm/schema/composition.md)。 有关架构所需的映射的详细信息，请参阅有关在UI](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources)中创建[源连接的指南 [!DNL Mixpanel] 。

![创建架构](../../images/tutorials/create/mixpanel-export-events/schema.png)

## 使用API将[!DNL Mixpanel]连接到Experience Platform

以下文档提供了有关如何使用API或用户界面将[!DNL Mixpanel]连接到Experience Platform的信息：

* [使用流服务API为 [!DNL Mixpanel] 创建源连接和数据流](../../tutorials/api/create/analytics/mixpanel.md)

## 使用UI将[!DNL Mixpanel]连接到Experience Platform

* [在UI中创建 [!DNL Mixpanel] 源连接](../../tutorials/ui/create/analytics/mixpanel.md)
* [在UI中为客户成功源连接创建数据流](../../tutorials/ui/dataflow/analytics.md)
