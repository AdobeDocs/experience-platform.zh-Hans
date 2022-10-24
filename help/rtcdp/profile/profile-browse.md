---
keywords: 查看配置文件rtcdp;rtcdp配置文件视图；rtcdp配置文件
title: 浏览Real-time Customer Data Platform中的用户档案
description: Adobe Real-time Customer Data Platform允许您使用Adobe Experience Platform用户界面浏览实时客户资料数据。
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# 浏览Real-time Customer Data Platform中的用户档案

实时客户资料可整合来自多个渠道的数据（包括在线、离线、CRM和第三方数据），从而创建每个客户的整体视图。 由于单个用户档案是根据从各种来源引入系统的数据进行汇总的，因此每个用户档案都会成为客户与您的品牌进行每次交互的可操作且加盖时间戳的帐户。

在Adobe Experience Platform用户界面中，您可以查看这些只读配置文件，并查看有关每个客户的重要信息，包括其偏好、过去事件、交互以及个人所属的区段。

Adobe Real-time Customer Data Platform构建于Adobe Experience Platform之上，因此能够利用Experience PlatformUI中的用户档案查看功能。 有关在Platform用户界面中查看客户配置文件的详细指南，请参阅 [Real-time Customer Profile用户指南](../../profile/ui/user-guide.md).

## Real-Time CDP B2B Edition的配置文件增强功能

除了Adobe Experience Platform、Real-Time CDP、B2B Edition支持的配置文件浏览功能外，用户还可以在 [!UICONTROL 属性] 和 [!UICONTROL 事件] 选项卡。 B2B数据还可用于执行分段，这些区段显示在客户的 [!UICONTROL 区段成员资格] 选项卡上的任意位置。

Real-Time CDP, B2B Edition还允许您浏览 [!UICONTROL 帐户], [!UICONTROL 机会]和 [!UICONTROL 源记录] 来自与单个客户关联的企业来源。

要探索这些增强功能，请首先执行 [Real-time Customer Profile用户指南](../../profile/ui/user-guide.md) 按合并策略或身份命名空间浏览配置文件。

![](images/b2b-browse-profile.png)

用户档案详细信息包括 [!UICONTROL 帐户], [!UICONTROL 机会]和 [!UICONTROL 源记录] 选项卡，以及客户配置文件中提供的标准信息，B2B事件和属性也增强了这些信息。

![](images/b2b-profile-detail.png)

### “帐户”选项卡

选择 **[!UICONTROL 帐户]** 查看与用户档案相关的帐户列表。 此列表包括帐户配置文件中的基本信息（如帐户的名称、网站和行业），以及指向帐户配置文件的链接。

有关查看和浏览帐户用户档案的更多信息，请首先阅读 [帐户配置文件概述](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### “机会”选项卡

的 **[!UICONTROL 机会]** 选项卡提供与帐户相关的未结和已结业务机会的详细信息。 这些机会可能会从多个来源摄取到Experience Platform中，但Real-Time CDP B2B Edition使营销人员能够轻松地在一个位置一起查看所有这些机会。

每个机会都包括诸如机会名称、其数量、阶段，以及该机会是否是打开、关闭、赢得还是丢失的信息。

![](images/b2b-profile-opportunities.png)

### “源记录”选项卡

的 **[!UICONTROL 源记录]** 选项卡，您可以轻松查看来自企业源的对单个客户配置文件做出贡献的多个源记录。 除 [!UICONTROL 人员来源键] 和电子邮件地址，每个源记录还提供记录类型（例如，“联系人”或“潜在客户”记录）以及源。

![](images/b2b-profile-source-records.png)
