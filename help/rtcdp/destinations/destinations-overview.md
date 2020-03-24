---
title: 目标概述
seo-title: 目标概述
description: 目标是预建的与目标平台的集成，允许从实时客户数据平台无缝激活数据。 您可以使用Adobe实时客户数据平台中的目标来激活您的已知和未知数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他使用案例。
seo-description: 目标是预建的与目标平台的集成，允许从实时客户数据平台无缝激活数据。 您可以使用Adobe实时客户数据平台中的目标来激活您的已知和未知数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他使用案例。
translation-type: tm+mt
source-git-commit: e66f4df13afb3c9f9ddb440ccb5e479caeef2142

---


# 目标概述

![目标概述横幅](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**目标** ，是与目标平台预建的集成，允许从实时客户数据平台无缝激活数据。 您可以使用 **目标** ，为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他使用案例激活已知和未知的数据。

## 目标和来源

实时CDP的核心功能之一是摄取第一方数据并根据业务需求激活它。 使 **[!UICONTROL Sources]** 用将数据引入实时CDP中， **[!UICONTROL Destinations]** 并从实时CDP中导出数据。

## 目标步骤

* 使用 **[!UICONTROL Destinations]** 激活 [档案](/help/rtcdp/destinations/activate-destinations.md) ，并将其发送到营销自动化平台、数字广告平台等。
* 从实时 [CDP中提供的所有目标的自助](/help/rtcdp/destinations/destinations-catalog.md) -服务目录中进行选择。
* 计划定期向首选目标导出数据。

## 控件

“目标”工作区中 [的控件](/help/rtcdp/destinations/destinations-workspace.md) ，允许您：

* 浏览可激活数据的目标平台目录；
* 创建、编辑、激活和禁用数据流至目录中的目标；
* 在存储位置创建一个帐户或将实时CDP链接到目标平台中的帐户；
* 选择应激活到目标的区段；
* 在将区段 [激活到电子邮件营销目标时](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/xdm_system/xdm_system_in_experience_platform.md) ，选择要导出的体验数据模型(XDM)字段。

## 目标类型和类别——视频概述

在Adobe实时CDP中，有两种目标类型：配置文件导出目标和区段导出目标。 以下视频介绍了两种目标类型。

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### 配置文件导出目标

配置文件导出目标会生成包含配置文件和／或属性的文件。 这些目标使用原始数据，通常以电子邮件地址作为主要密钥。

### 区段导出目标

区段导出目标会发送配置文件及其符合条件的区段。 这些目标使用区段ID或用户ID。

### 目标类别

目标目录中的目 [标按目标类别](/help/rtcdp/destinations/destinations-catalog.md) (**Advertising**、 **Cloud storage**、 **Email Marketing**)进行分组。 有关每个目标的详细信息，请参阅目 [标目录](/help/rtcdp/destinations/destinations-catalog.md)。

## 目标和访问控制

实 **[!UICONTROL Destinations]** 时CDP中的功能与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以查看、管理和激活目标。 有关各个权限的信息，请参 [阅Adobe Experience Platform中的访问控制](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-overview.md) ，然后向下滚动到页面底部。

有关访问控制的详细信息，请参阅 [访问控制用户指南](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-user-guide.md)。