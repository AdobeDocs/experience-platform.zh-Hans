---
keywords: Experience Platform；主页；热门主题；
title: (Beta) Mixpanel源连接器概述
description: 了解如何使用API或用户界面将Mixpanel连接到Adobe Experience Platform。
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (Beta) [!DNL Mixpanel]

>[!NOTE]
>
>此 [!DNL Mixpanel] 源为测试版。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源的更多信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方Analytics应用程序引入数据。 对分析提供商的支持包括 [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) 是一款产品分析工具，用于捕获有关用户如何与数字产品交互的数据。 Mixpanel允许您通过简单的交互式报表分析此产品数据，这些报表允许您只需单击几下即可查询和可视化数据。

源利用 [Mixpanel事件导出API >下载](https://developer.mixpanel.com/reference/raw-event-export) 在接收并存储事件数据时下载该数据 [!DNL Mixpanel]，以及所有事件属性(包括 `distinct_id`)和将事件发送到Experience Platform中的确切时间戳。 Mixpanel使用持有者令牌作为身份验证机制，与Mixpanel事件导出API通信。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面，以了解更多信息。

## 验证您的 [!DNL Mixpanel] 帐户

此部分概述了验证帐户身份并将您的帐户带入 [!DNL Mixpanel] 数据到Platform。

为了创建 [!DNL Mixpanel] 源连接和数据流，您必须首先拥有有效的 [!DNL Mixpanel] 帐户。 如果您没有有效的 [!DNL Mixpanel] 帐户，请参阅 [Mixpanel寄存器](https://mixpanel.com/register/) 页面创建您的帐户。

成功创建 [!DNL Mixpanel] 帐户，导航到 [!DNL Project Details] 在中选项卡 [!DNL Project Seettings] 第页，共 [!DNL Mixpanel] 用于检索项目ID和配置时区的UI。

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

接下来，导航到 [!DNL Service Accounts] 在中选项卡 [!DNL Project Settings] 中的页面 [!DNL Mixpanel] 用于检索您的服务帐户凭据的UI。

>[!TIP]
>
>对于最佳实践，请选择一个服务帐户 [不会过期](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Mixpanel服务帐户](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

最后，创建平台 [架构](../../../xdm/schema/composition.md) 必需 [!DNL Mixpanel Event Export API]. 有关架构所需的映射的更多信息，请参阅 [创建 [!DNL Mixpanel] UI中的源连接](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![创建架构](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connect [!DNL Mixpanel] 到使用API的平台

以下文档提供了有关如何连接的信息 [!DNL Mixpanel] 至使用API或用户界面的Platform：

* [创建源连接和数据流 [!DNL Mixpanel] 使用流服务API](../../tutorials/api/create/analytics/mixpanel.md)

## Connect [!DNL Mixpanel] 使用UI到Platform

* [创建 [!DNL Mixpanel] UI中的源连接](../../tutorials/ui/create/analytics/mixpanel.md)
* [在UI中为客户成功源连接创建数据流](../../tutorials/ui/dataflow/analytics.md)
