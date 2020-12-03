---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年1月15日
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 7%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 1 月 15 日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是背后的关键概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到一个通用表现形式中，以更快、更集成的方式提供洞察。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 等层次结构字段的字段类型限制 | 在将XDM字段定义为特定类型后，任何具有相同名称和层次结构的其他字段必须使用相同的字段类型，而不管在中使用的类或混合。 例如，如果XDM类的混 [!DNL Profile] 音包含 `profile.age` 类型为“integer”的字段，则XDM的类似混音 [!DNL ExperienceEvent] 不能包含类型 `profile.age` 为“string”的字段。 要使用不同的字段类型，该字段必须具有与先前定义的字段不同的层次结构(例如 `profile.person.age`)。 此功能旨在防止在模式在合并中聚集时发生冲突。 虽然约束不会追溯影响现有模式，但强烈建议您查看字段类型冲突的模式，并根据需要编辑它们。 |
| 区分大小写的字段验证 | 同一级别的自定义字段必须具有不同的名称，而不考虑大小写。 例如，如果添加一个名为“Email”的自定义字段，则不能在名为“email”的同一级别添加另一个自定义字段。 |

**已知问题**

* None

要进一步了解如何使用API和 [!DNL Schema Registry] 用户 [!DNL Schema Editor] 界面使用XDM，请阅 [读XDM系统文档](../../xdm/home.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和组织法规授予用户根据请求从数据存储中访问或删除其个人数据的权利。 Adobe Experience Platform [!DNL Privacy Service] 提供了RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 您可 [!DNL Privacy Service]以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| [!DNL Privacy Service] 重新品牌 | 由于服务已发展为支持除GDPR外的其 [!DNL Privacy Service] 他法规，先前命名的“GDPR服务”已重新命名为。 |
| 新的API端点 | API的基本路 [!DNL Privacy Service] 径已从更新 `/data/privacy/gdpr` 为 `/data/core/privacy/jobs`。 |
| 新的必需 `regulation` 属性 | 在API中创建新作业时，必 [!DNL Privacy Service] 须在请求 `regulation` 有效负荷中提供一个属性，以指示要跟踪作业的法规。 接受的值 `gdpr` 是和 `ccpa`。 |
| 支持 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] 现在接受来自Adobe的访问／删 [!DNL Primetime Authentication]除请求， `primetimeAuthentication` 使用作其产品价值。 |
| Privacy ServiceUI增强 | 为GDPR和CCPA规定分别设置工作跟踪页面。 新**规则类型**下拉列表，用于在GDPR和CCPA的跟踪数据之间切换。 |

**已知问题**

* None

有关更多信 [!DNL Privacy Service]息，请阅读开始 [概述](../../privacy-service/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用服务来构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持客户属性数据 | 用于创建流连接器以采集客户属性数据的UI和API支持。 |
| 对云存储的其他文件格式支持 | 从云存储获取文件现在支持符合XDM规范的Parke和JSON文件格式。 |
| 支持访问控制权限 | Adobe Experience Platform的访问控制框架提供授予访问数据获取来源所需的权限。 根据用户的权限级别，用户可以视图源、管理源或完全拒绝访问。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 数据获取 | 管理源 | 访问读取、创建、编辑和禁用源。 |
| 数据获取 | 视图源 | 对“目录”选项卡中的可用源和“浏览” **[!UICONTROL 选项卡中]** 经过身份验证的源进行只 **[!UICONTROL 读访问]** 。 |

**已知问题**

* None

有关源的详细信息，请参阅源 [概述](../../sources/home.md)

## 目标 {#destinations}

在实 [时CDP中](../../rtcdp/overview.md)，目标是预建的与目标平台集成，这些平台可以无缝地向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持访问控制权限 | 实时CDP中的目标功能可与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以视图、管理和激活目标。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 目标 | 管理目标 | 访问读取、创建、编辑和禁用目标。 |
| 目标 | 视图目标 | 对“目录”选项卡中的可用目标和“浏 **[!UICONTROL 览]** ”选项卡中的已验证目标进行只 **读访问** 。 |
| 目标 | 激活目标 | 能够将数据激活到目标。 此权限要求将“管理目标”或“视图目标”添加到产品用户档案。 |

**已知问题**

* None

See the [Destinations overview](../../destinations/home.md) for more information.