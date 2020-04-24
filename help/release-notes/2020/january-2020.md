---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年1月15日
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 1 月 15 日**

对Adobe Experience Platform中现有功能的更新：

* [体验数据模型(XDM)系统](#xdm)
* [隐私服务](#privacy)
* [来源](#sources)
* [目标](#destinations)

## 体验数据模型(XDM)系统 {#xdm}

标准化和互操作性是Experience Platform的主要概念。 Adobe推动的体验数据模型(XDM)旨在标准化客户体验数据并定义客户体验管理模式。

XDM是一个公开的规范，旨在提高数字体验的强大功能。 它为与Adobe Experience Platform上的服务通信的任何应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到以更快、更集成的方式提供洞察的共同表现形式中。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 等层次字段的字段类型限制 | 在将XDM字段定义为特定类型后，具有相同名称和层次结构的任何其他字段必须使用相同的字段类型，而不管在中使用的类或混音。 例如，如果XDM用户档案类的mixin包含类型为“integer”的字段，则XDM ExperienceEvent的类似mixin不能具有类型为 `profile.age``profile.age` “string”的字段。 要使用不同的字段类型，字段必须具有与先前定义的字段不同的层次结构(例如， `profile.person.age`)。 此功能旨在防止在合并中将模式聚到一起时发生冲突。 虽然约束不会逆向影响现有模式，但强烈建议您查看字段类型冲突的模式并根据需要编辑它们。 |
| 区分大小写的字段验证 | 同一级别的自定义字段名称必须不同，而不考虑大小写。 例如，如果添加一个名为“Email”的自定义字段，则无法在名为“email”的同一级别添加另一个自定义字段。 |

**已知问题**

* None

要了解有关使用模式注册表API和模式编辑器用户界面使用XDM的更多信息，请阅读 [XDM系统文档](../../xdm/home.md)。

## 隐私服务 {#privacy}

新的法律和组织法规授予用户根据请求从数据存储中访问或删除其个人数据的权利。 Adobe Experience Platform Privacy Service提供RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 通过隐私服务，您可以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| Privacy Service重新品牌化 | 先前名为“GDPR服务”的服务已更名为隐私服务，因为该服务已发展为支持除GDPR外的其他法规。 |
| 新的API端点 | 隐私服务API的基本路径已从更新 `/data/privacy/gdpr` 到 `/data/core/privacy/jobs`。 |
| 新的必需 `regulation` 属性 | 在Privacy Service API中创建新作业时，必须在请求有效负荷中提供一个属性，以指示要跟踪作业的规定。 `regulation` 接受的值 `gdpr` 是和 `ccpa`。 |
| 支持Adobe Primetime身份验证 | 隐私服务现在接受Adobe Primetime身份验证的访问／删除请求，并 `primetimeAuthentication` 将其作为产品价值。 |
| 隐私服务UI增强功能 | 为GDPR和CCPA规定单独分别设置作业跟踪页面。 可在 __ GDPR和CCPA的跟踪数据之间切换的新调整类型下拉菜单。 |

**已知问题**

* None

有关隐私服务的更多信息，请阅读隐私服务 [概述开始](../../privacy-service/home.md)。

## 来源 {#sources}

Adobe Experience Platform可以从外部源中摄取数据，同时允许您使用平台服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)获取数据。

Experience Platform提供RESTful API和交互式UI，使您能轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，为摄取运行设置时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 客户属性数据支持 | UI和API支持，用于创建流连接器以获取客户属性数据。 |
| 云存储的其他文件格式支持 | 从云存储获取文件现在支持符合XDM规范的Parke和JSON文件格式。 |
| 支持访问控制权限 | Adobe Experience Platform中的访问控制框架提供了授予访问数据获取中的源所需的权限。 根据用户的权限级别，用户可以视图源、管理源或完全拒绝访问。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 数据摄取 | 管理源 | 访问读取、创建、编辑和禁用源。 |
| 数据摄取 | 视图源 | 对“目录”选项卡中可用源和“浏览”选项卡中 *经过身份验证的* 源的只 *读访问* 。 |

**已知问题**

* None

有关源的详细信息，请参阅源 [概述](../../sources/home.md)

## 目标 {#destinations}

在 [Adobe实时CDP中](../../rtcdp/overview.md)，目标是预建的与目标平台的集成，这些平台可以无缝地向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持访问控制权限 | 实时CDP中的“目标”功能与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以视图、管理和激活目标。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 目标 | 管理目标 | 访问读取、创建、编辑和禁用目标。 |
| 目标 | 视图目标 | 对“目录”选项卡中可用目标和“浏览”选项卡中 _已验证目标_ ，具有只读 _访问权限_ 。 |
| 目标 | 激活目标 | 能够将数据激活到目标。 此权限要求将“管理目标”或“视图目标”添加到产品用户档案。 |

**已知问题**

* None

有关详细 [信息，请参阅](../../rtcdp/destinations/destinations-overview.md) “目标”概述。