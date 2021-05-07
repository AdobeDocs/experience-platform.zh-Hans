---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年1月15日
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 7%

---

# Adobe Experience Platform 发行说明

**发行日期：2020 年 1 月 15 日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM)系统  {#xdm}

标准化和互操作性是[!DNL Experience Platform]背后的关键概念。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。

XDM是一个公开存档的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到以更快、更集成的方式提供洞察的常见表现形式中。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 等层次域的域类型限制 | 在将XDM字段定义为特定类型后，任何具有相同名称和层次结构的其他字段都必须使用相同的字段类型，而不管在中使用的类或模式字段组。 例如，如果XDM [!DNL Profile]类的字段组包含类型为“integer”的`profile.age`字段，则XDM [!DNL ExperienceEvent]的类似字段组不能具有类型为“string”的`profile.age`字段。 要使用不同的字段类型，该字段必须具有与先前定义的字段不同的层次结构（例如`profile.person.age`）。 此功能旨在防止将模式放在合并中时发生冲突。 虽然约束不会追溯影响现有模式，但强烈建议您查看字段类型冲突的模式并根据需要编辑它们。 |
| 区分大小写的字段验证 | 同一级别的自定义字段必须具有不同的名称，而不考虑大写。 例如，如果您添加了名为“Email”的自定义字段，则无法在名为“email”的同一级别添加其他自定义字段。 |

**已知问题**

* None

要进一步了解如何使用[!DNL Schema Registry] API和[!DNL Schema Editor]用户界面使用XDM，请阅读[ XDM系统文档](../../xdm/home.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和组织法规授予用户在请求时从您的数据存储中访问或删除其个人数据的权利。 Adobe Experience Platform [!DNL Privacy Service]提供一个RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 通过[!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| [!DNL Privacy Service] 重品牌 | 之前名为“GDPR服务”的服务已更名为[!DNL Privacy Service]，因为该服务已发展为支持除GDPR外的其他法规。 |
| 新的API端点 | [!DNL Privacy Service] API的基本路径已从`/data/privacy/gdpr`更新为`/data/core/privacy/jobs`。 |
| 新的必需`regulation`属性 | 在[!DNL Privacy Service] API中创建新作业时，必须在请求有效负荷中提供`regulation`属性，以指示跟踪该作业所依据的规则。 接受的值为`gdpr`和`ccpa`。 |
| 支持 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] 现在接受来自Adobe的访问/删 [!DNL Primetime Authentication]除请求， `primetimeAuthentication` 使用作其产品值。 |
| Privacy ServiceUI增强 | 为GDPR和CCPA规定分别设置工作跟踪页面。 新**规章类型**下拉列表，用于在GDPR和CCPA的跟踪数据之间切换。 |

**已知问题**

* 无

有关[!DNL Privacy Service]的详细信息，请阅读[开始概述](../../privacy-service/home.md)进行Privacy Service。

## 源 {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强该数据。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供RESTful API和交互式UI，让您可以轻松为各种数据提供者设置源连接。这些源连接允许您对外部存储系统和CRM服务进行身份验证并连接，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持客户属性数据 | 用于创建流连接器以摄取客户属性数据的UI和API支持。 |
| 对云存储的其他文件格式支持 | 云存储的文件摄取现在支持符合XDM规范的Parke和JSON文件格式。 |
| 支持访问控制权限 | Adobe Experience Platform中的访问控制框架提供授予访问数据获取中的源所需的权限。 根据用户的权限级别，用户可以视图源、管理源或完全拒绝访问。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 数据获取 | 管理源 | 访问读取、创建、编辑和禁用源。 |
| 数据获取 | 视图源 | 对&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡中可用源的只读访问，对&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡中已验证源的只读访问。 |

**已知问题**

* 无

有关源的详细信息，请参阅[源概述](../../sources/home.md)

## 目标 {#destinations}

在[实时CDP](../../rtcdp/overview.md)中，目标是预构建的与目标平台的集成，这些平台可以无缝地向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持访问控制权限 | 实时CDP中的目标功能可以与Adobe Experience Platform访问控制权限一起使用。 根据用户的权限级别，您可以视图、管理和激活目标。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 目标 | 管理目标 | 访问读取、创建、编辑和禁用目标。 |
| 目标 | 视图目标 | 对&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡中可用目标和&#x200B;**浏览**&#x200B;选项卡中已验证目标的只读访问。 |
| 目标 | 激活目标 | 能够将数据激活到目标。 此权限要求将“管理目标”或“视图目标”添加到产品用户档案。 |

**已知问题**

* 无

有关详细信息，请参阅[目标概述](../../destinations/home.md)。
