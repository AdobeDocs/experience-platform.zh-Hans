---
keywords: 查看配置文件rtcdp；rtcdp配置文件视图；rtcdp配置文件
title: 在Real-time Customer Data Platform中浏览配置文件
description: 通过Adobe Real-time Customer Data Platform，您可以使用Adobe Experience Platform用户界面浏览实时客户档案数据。
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# 在Real-time Customer Data Platform中浏览配置文件

Real-time Customer Profile可以为每位客户创建整体视图，结合来自多个渠道（包括在线、离线、CRM和第三方数据）的数据。 由于各个用户档案是根据不同来源带入系统的数据进行汇总的，因此每个用户档案都成为一个可操作的带有时间戳的帐户，说明了您的客户与您的品牌每次互动。

在Adobe Experience Platform用户界面中，您可以查看这些只读配置文件，并查看有关每个客户的重要信息，包括他们的偏好、过去的事件、交互和个人所属的受众。

Adobe Real-time Customer Data Platform构建于Adobe Experience Platform之上，因此能够利用Experience PlatformUI中的用户档案查看功能。 有关在Platform用户界面中查看客户配置文件的详细指南，请参阅 [Real-time Customer Profile用户指南](../../profile/ui/user-guide.md).

## Real-Time CDP B2B版本的配置文件增强功能

除了Adobe Experience Platform支持的配置文件浏览功能外，Real-Time CDP B2B版用户还可以在以下位置访问客户配置文件中的B2B属性和事件： [!UICONTROL 属性] 和 [!UICONTROL 事件] 选项卡。 B2B数据还可用于执行分段，使这些受众出现在客户的 [!UICONTROL 受众会员资格] 选项卡中的非B2B受众。

Real-Time CDP， B2B版本还允许您浏览 [!UICONTROL 帐户]， [!UICONTROL 机会]、和 [!UICONTROL 源记录] 从与单个客户关联的企业源中。

要探究这些增强功能，请首先按照 [Real-time Customer Profile用户指南](../../profile/ui/user-guide.md) 按合并策略或身份命名空间浏览配置文件。

![](images/b2b-browse-profile.png)

配置文件详细信息包括对 [!UICONTROL 帐户]， [!UICONTROL 机会]、和 [!UICONTROL 源记录] 除了客户档案中提供的标准信息之外，该信息还增强了B2B事件和属性。

![](images/b2b-profile-detail.png)

### “帐户”选项卡

选择 **[!UICONTROL 帐户]** 查看与用户档案相关的帐户列表。 此列表包括帐户配置文件中的基本信息，例如帐户的名称、网站和行业，以及指向帐户配置文件的链接。

有关查看和浏览帐户配置文件的更多信息，请从阅读 [帐户配置文件概述](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### “业务机会”选项卡

此 **[!UICONTROL 机会]** 标签页提供与帐户相关的未结和已结业务机会的详细信息。 这些机会可能会从多个来源引入Experience Platform，但是Real-Time CDP， B2B版本使营销人员可以轻松地在一个位置一起查看所有这些机会。

每个机会都包括一些信息，如机会的名称、数量、阶段，以及机会是开放、关闭、成功还是失败。

![](images/b2b-profile-opportunities.png)

### “源记录”选项卡

此 **[!UICONTROL 源记录]** 选项卡使您可以轻松查看来自企业来源且对单个客户配置文件有贡献的多个源记录。 除了 [!UICONTROL 人员源密钥] 和电子邮件地址，每个源记录还提供了记录类型（例如，“联系人”或“潜在客户”记录）以及源。

![](images/b2b-profile-source-records.png)
