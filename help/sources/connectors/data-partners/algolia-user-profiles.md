---
title: Algolia用户配置文件Source概述
description: 了解Adobe Experience Platform中的Algolia用户配置文件源
hide: true
hidefromtoc: true
source-git-commit: 1bde4b831f1b79de1a8292ad5f221f522e871d08
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# [!DNL Algolia User Profiles]

[[!DNL Algolia]](https://www.algolia.com/)是一个功能强大的搜索和发现API平台，使企业能够提供快速、相关且可自定义的搜索体验。 它提供了实时搜索功能，具有拼写容错、过滤、分面和AI支持的相关性调整等功能。 [!DNL Algolia]通过为网站、电子商务平台和应用程序提供高性能搜索解决方案，帮助公司提高用户参与度、转化率和总体客户体验。

[!DNL Algolia]的一些主要优势包括：

* 快速搜索，结果即时可见。
* 由AI提供支持的具有高度相关性的推荐。
* 可自定义的排名，可排定业务需求的优先级。
* 可轻松处理高流量负载的扩展性。

有关详细信息，请访问[[!DNL Algolia] 产品文档](https://resources.algolia.com/)。

## 架构

自助式源(批处理SDK)提供所有必需的功能，例如身份验证、分页或完整和部分数据拉取。 [!DNL Algolia User Profiles]源使用这些功能完成集成。

![Algolia与Experience Platform集成的架构](../../images/tutorials/create/algolia/user-profiles/algolia-aep-user-profiles-arch.png)

## 先决条件 {#prerequisites}

必须先完成以下先决步骤，然后才能将您的[!DNL Algolia]帐户连接到Experience Platform。

1. 使用[[!DNL Algolia] 仪表板](https://dashboard.algolia.com/users/sign_up)登录您的[!DNL Algolia]帐户或创建新帐户。
2. [准备索引](https://www.algolia.com/doc/guides/sending-and-managing-data/prepare-your-data/in-depth/prepare-data-in-depth/)。
3. [设置您的Facet](https://www.algolia.com/doc/guides/managing-results/refine-results/faceting/)。
4. [发送用户事件](https://www.algolia.com/doc/guides/sending-events/getting-started/)。
5. [个性化您的索引](https://www.algolia.com/doc/guides/personalization/advanced-personalization/configure/setup/indices/)。

### 在Experience Platform上配置权限

若要将您的[!DNL Algolia]帐户连接到Experience Platform，您必须同时为您的帐户启用&#x200B;**[!UICONTROL 查看源]**&#x200B;和&#x200B;**[!UICONTROL 管理源]**&#x200B;权限。 请联系您的产品管理员以获取必要的权限。 有关详细信息，请阅读[访问控制UI指南](../../../access-control/abac/ui/permissions.md)。

### IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 列入允许列表有关详细信息，请参阅[IP地址](../../ip-address-allow-list.md)页。

## 将您的[!DNL Algolia]帐户连接到Experience Platform

完成先决条件后，您可以继续下一步并[将您的 [!DNL Algolia] 帐户连接到Experience Platform](../../tutorials/ui/create/data-partners/algolia-user-profiles.md)。
