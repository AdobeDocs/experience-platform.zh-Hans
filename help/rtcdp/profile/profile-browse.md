---
keywords: 查看配置文件rtcdp；rtcdp配置文件视图；rtcdp配置文件
title: 在Real-time Customer Data Platform中浏览配置文件
description: Adobe Real-time Customer Data Platform允许您使用Adobe Experience Platform用户界面浏览实时客户配置文件数据。
feature: Get Started, Profiles
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: ea785ffa1dfa0f7c684fe536796a4b7409882159
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# 在Real-time Customer Data Platform中浏览配置文件

Real-time Customer Profile可以为每位客户创建整体视图，结合来自多个渠道（包括在线、离线、CRM和第三方数据）的数据。 由于个人资料是根据从各种来源引入系统的数据进行聚合的，因此每个个人资料都成为一个可操作、且带有时间戳的帐户，说明了您的客户与您的品牌每次互动。

在Adobe Experience Platform用户界面中，您可以查看这些只读用户档案，并查看有关每个客户的重要信息，包括他们的偏好设置、过去的事件、交互和个人所属的受众。

Adobe Real-time Customer Data Platform基于Adobe Experience Platform构建，因此能够利用Experience PlatformUI中的用户档案查看功能。 有关在Platform用户界面中查看客户配置文件的详细指南，请参阅[实时客户配置文件用户指南](../../profile/ui/user-guide.md)。

## Real-Time CDP B2B版本的配置文件增强功能

除了Adobe Experience Platform支持的配置文件浏览功能外，Real-Time CDP和B2B版本的用户还可以分别在[!UICONTROL 属性]和[!UICONTROL 事件]选项卡上访问客户配置文件中的B2B属性和事件。 B2B数据还可用于执行分段，这些受众与非B2B受众一起显示在客户的[!UICONTROL 受众成员资格]选项卡下。

Real-Time CDP， B2B版本还允许您跨与单个客户关联的企业源浏览[!UICONTROL 帐户]、[!UICONTROL 机会]和[!UICONTROL Source记录]。

要探究这些增强功能，请按照[实时客户配置文件用户指南](../../profile/ui/user-guide.md)中概述的步骤开始，按合并策略或身份命名空间浏览配置文件。

![](images/b2b-browse-profile.png)

除了客户个人资料中提供的标准信息之外，该个人资料详细信息还包括对[!UICONTROL 帐户]、[!UICONTROL 机会]和[!UICONTROL Source记录]选项卡的访问权限，这些信息还增强了B2B事件和属性。

![](images/b2b-profile-detail.png)

要了解有关平台UI中提供的配置文件详细信息的更多信息，请参阅配置文件仪表板文档](../../dashboards/guides/profiles.md#browse-profiles)的[详细信息部分。

### “帐户”选项卡

选择&#x200B;**[!UICONTROL 帐户]**&#x200B;查看与配置文件相关的帐户列表。 此列表包括来自帐户资料的基本信息，如帐户的名称、网站和行业，以及指向帐户个人资料的链接。

有关查看和浏览帐户配置文件的详细信息，请从阅读[帐户配置文件概述](../accounts/account-profile-overview.md)开始。

![](images/b2b-profile-accounts.png)

### “业务机会”选项卡

**[!UICONTROL 机会]**&#x200B;选项卡提供与帐户相关的未结和已结机会的详细信息。 这些机会可能会从多个来源引入Experience Platform，但是Real-Time CDP B2B版本使营销人员能够轻松地在一个位置一起查看所有这些机会。

每个机会都包括一些信息，如机会的名称、数量、阶段，以及机会是开放、关闭、成功还是失败。

![](images/b2b-profile-opportunities.png)

### “Source记录”选项卡

通过&#x200B;**[!UICONTROL Source记录]**&#x200B;选项卡，您可以轻松查看企业来源产生的对单个客户配置文件有贡献的多个源记录。 除了[!UICONTROL 人员源密钥]和电子邮件地址之外，每个源记录还提供记录类型（例如，“联系人”或“潜在客户”记录）以及源。

![](images/b2b-profile-source-records.png)
