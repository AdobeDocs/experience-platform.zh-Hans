---
title: 监视功能板概述
description: 了解如何使用Adobe Experience Platform UI中的监视仪表板
exl-id: 06ea5380-d66e-45ae-aa02-c8060667da4e
source-git-commit: 710fa6930b27f95d34539a18881c0f9d23e1debd
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 1%

---

# 监视功能板概述

使用Adobe Experience Platform UI中的监视仪表板查看数据从摄取到激活的历程。 使用监视功能板，您可以：

* 监控您的数据从源、Identity服务、实时客户档案、受众到最终目标的历程。
* 查看不同的量度和状态，具体取决于数据所处的阶段。
* 按数据类型筛选数据监视视图。

监视功能板支持查看几种不同的数据类型：

* **客户和帐户**：客户数据是指在中使用的数据 [Real-time Customer Data Platform](../../rtcdp/home.md)，而帐户数据参考 [帐户配置文件数据](../../rtcdp/accounts/account-profile-overview.md) 订阅时可访问的区段 [Real-Time CDP， B2B版本](../../rtcdp/b2b-overview.md). 如果您的Real-Time CDP许可证不包括Real-Time CDP B2B版本，则只能使用监视功能板来监视客户数据。
* **潜在客户**： [目标客户配置文件](../../profile/ui/prospect-profile.md) 用于表示尚未与您的公司联系但您想要联系的人员。 利用潜在客户配置文件，您可以使用来自可信第三方合作伙伴的属性来补充您的客户配置文件。 您必须拥有Real-Time CDP（应用程序服务）、Adobe Experience Platform Activation、Real-Time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate的许可才能查看潜在客户数据类型。
* **帐户配置文件扩充**：使用帐户配置文件，可统一来自多个来源的帐户信息。 您必须被授权使用Real-Time CDP B2B版本，才能监控帐户配置文件扩充数据。

阅读本文档，了解如何使用监控仪表板监控不同Experience Platform服务之间的数据旅程。

## 快速入门

本文档要求您对Experience Platform的以下组件有一定的了解：

* [数据流](../home.md)：数据流是跨Experience Platform移动数据的数据作业的表示形式。 您可以使用源工作区创建数据流，以将数据从给定源摄取到Experience Platform。
* [源](../../sources/home.md)：在Experience Platform中使用源从Adobe应用程序或第三方数据源中摄取数据。
* [Identity Service](../../identity-service/home.md)：通过跨设备和系统桥接身份，更好地了解个人客户及其行为。
* [Real-time Customer Profile](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [分段](../../segmentation/home.md)：使用分段服务根据实时客户档案数据创建区段和受众。
* [目标](../../destinations/home.md)：目标是预建的与常用应用程序的集成，可无缝激活Platform中的数据，以用于跨渠道营销活动、电子邮件活动、定向广告和许多其他用例。

## 监视仪表板指南

在Experience PlatformUI中，选择 **[!UICONTROL 监控]** 下 [!UICONTROL 数据管理] 在左侧导航中。

![Experience PlatformUI中的监视仪表板。](../assets/ui/monitor-overview/monitoring.png)

选择 **[!UICONTROL 数据类型]** 然后使用下拉菜单选择要查看的数据类型。 数据类型由Experience Data Model (XDM)架构类定义，以确保其数据在摄取到Experience Platform中时遵循标准格式。 有关更多信息，请访问以下文档：

* [B2B帐户数据类型](../../rtcdp/b2b-tutorial.md)
* [目标客户数据类型](../../rtcdp/partner-data/prospecting.md)

您可以根据以下数据类型筛选视图：

>[!BEGINTABS]

>[!TAB 全部]

选择 **[!UICONTROL 全部]** 更新您的功能板，并显示指定时间段内摄取到Experience Platform的所有数据的量度。

![监控数据类型设置为“全部”。](../assets/ui/monitor-overview/all.png)

>[!TAB 客户和帐户]

选择 **[!UICONTROL 客户和帐户]** 更新您的信息板，并显示给定时间段内引入到Experience Platform的客户和帐户数据的量度。

![监控数据类型设置为“客户和帐户”。](../assets/ui/monitor-overview/customer-account.png)

>[!TAB 潜在客户]

选择 **[!UICONTROL 潜在客户]** 更新您的仪表板，并显示指定时间段内引入到Experience Platform的潜在客户数据的指标。 **注意**：只有当您符合以下条件时，才能查看目标客户数据类型活动 [有权使用目标客户数据](../../rtcdp/partner-data/prospecting.md).

![监控数据类型设置为“潜在客户”。](../assets/ui/monitor-overview/prospect.png)

>[!TAB 帐户配置文件扩充]

选择 **[!UICONTROL 帐户配置文件扩充]** 以更新您的功能板并显示配置文件扩充数据的量度。 **注意**：只有当您有权查看帐户配置文件扩充指标时，才能 [B2B数据](../../rtcdp/b2b-tutorial.md).

![监控数据类型设置为“帐户配置文件扩充”。](../assets/ui/monitor-overview/account-profile-enrichment.png)

>[!ENDTABS]

使用功能板的顶部标题可获得跨服务监控体验。 您可以通过从数据类别标题中选择您选择的功能卡来过滤量度和图形视图。

>[!BEGINTABS]

>[!TAB 源]

选择 **[!UICONTROL 源]** 以查看源摄取率的量度。 阅读指南： [监控源数据](monitor-sources.md) 以了解更多信息。

![UI中的监控仪表板，其中已选择源信息卡。](../assets/ui/monitor-overview/sources.png)

>[!TAB 身份]

选择 **[!UICONTROL 身份]** 查看身份数据的处理成功率。 阅读指南： [监控身份数据](monitor-identities.md) 以了解更多信息。

![UI中的监视仪表板，已选择身份卡。](../assets/ui/monitor-overview/identities.png)

>[!TAB 用户档案]

选择 **[!UICONTROL 配置文件]** 查看配置文件数据的处理成功率。 阅读指南： [监控配置文件数据](monitor-profiles.md) 以了解更多信息。

![UI中的监视仪表板，已选择用户档案信息卡。](../assets/ui/monitor-overview/profiles.png)

>[!TAB 受众]

选择 **[!UICONTROL 受众]** 要查看受众和分段作业的量度，请执行以下操作： 阅读指南： [监控受众数据](monitor-audiences.md) 以了解更多信息。

![Ui中的监视仪表板，已选择受众信息卡。](../assets/ui/monitor-overview/audiences.png)

>[!TAB 目标]

选择 **[!UICONTROL 目标]** 查看您的量度 [!UICONTROL 流激活率] 和 [!UICONTROL 批处理失败的数据流运行]. 阅读指南： [监控目标数据](monitor-destinations.md) 以了解更多信息。

![UI中的监视仪表板，已选择目标信息卡。](../assets/ui/monitor-overview/destinations.png)

>[!ENDTABS]

### 配置监视时间范围 {#configure-monitoring-time-frame}

默认情况下，监视功能板显示过去24小时内摄取的数据的量度。 要更新时间范围，请选择 **[!UICONTROL 最近24小时]**.

![UI中的监视仪表板，其中包含选定的时间配置。](../assets/ui/monitor-overview/select-time.png)

您可以在显示的对话框中为数据监视视图配置新的时间范围。 您可以选择创建自定义时间范围，或从预配置选项列表中选择：

* [!UICONTROL 最近 24 小时]
* [!UICONTROL 最近7天]
* [!UICONTROL 最近30天]

完成后，选择 **[!UICONTROL 应用]**.

![监视仪表板中的时间范围配置弹出窗口。](../assets/ui/monitor-overview/update-time.png)

## 后续步骤

通过阅读本文档，您现在可以在UI中的监视仪表板中导航。 有关如何监视特定Experience Platform服务的数据的信息，请阅读以下文档：

* [监控源数据](monitor-sources.md).
* [监视身份数据](monitor-identities.md).
* [监测配置文件数据](monitor-profiles.md).
* [监测受众数据](monitor-audiences.md).
* [监视目标数据](monitor-destinations.md).
