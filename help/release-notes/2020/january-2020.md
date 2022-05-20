---
title: Adobe Experience Platform发行说明2020年1月
description: 2020年1月版Adobe Experience Platform发行说明。
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---

# Adobe Experience Platform 发行说明

**发行日期：2020 年 1 月 15 日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是其背后的关键概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)在Adobe的驱动下，努力标准化客户体验数据并定义客户体验管理架构。

XDM是一项公开记录的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵循XDM标准，所有客户体验数据都可以整合到通用呈现形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 等层级字段的字段类型限制 | 在将XDM字段定义为特定类型后，任何具有相同名称和层次结构的其他字段都必须使用相同的字段类型，而不管它们在中使用的类或架构字段组。 例如，如果XDM的字段组 [!DNL Profile] 类包含 `profile.age` “integer”类型的字段，XDM的类似字段组 [!DNL ExperienceEvent] 不能 `profile.age` “string”类型的字段。 要使用不同的字段类型，该字段必须具有与先前定义的字段不同的层次结构(例如， `profile.person.age`)。 此功能旨在防止在架构合并时发生冲突。 虽然约束不会对现有架构产生追溯性影响，但强烈建议您查看架构中的字段类型冲突，并根据需要对其进行编辑。 |
| 区分大小写的字段验证 | 同一级别的自定义字段必须具有不同的名称，而不考虑大小写。 例如，如果您添加了名为“Email”的自定义字段，则无法在同一级别添加名为“email”的其他自定义字段。 |

**已知问题**

* None

要了解有关使用XDM的更多信息，请使用 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用户界面，请阅读 [XDM系统文档](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 使用 [!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除私有或个人客户数据的请求，以便自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| [!DNL Privacy Service] 重新品牌化 | 以前称为“GDPR服务”的更名为 [!DNL Privacy Service] 随着该服务的发展，除了GDPR之外，还支持其他法规。 |
| 新的API端点 | 的基本路径 [!DNL Privacy Service] API已从 `/data/privacy/gdpr` to `/data/core/privacy/jobs`. |
| 新增必需 `regulation` 属性 | 在 [!DNL Privacy Service] API， a `regulation` 必须在请求有效负载中提供属性，以指示要跟踪作业的法规。 接受的值为 `gdpr` 和 `ccpa`. |
| 支持 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] 现在接受来自Adobe的访问/删除请求 [!DNL Primetime Authentication]，使用 `primetimeAuthentication` 作为其产品价值。 |
| Privacy ServiceUI增强 | 为GDPR和CCPA法规分别设置作业跟踪页面。 新增了**法规类型**下拉列表，用于在GDPR和CCPA的跟踪数据之间切换。 |

**已知问题**

* 无

有关 [!DNL Privacy Service]，请首先阅读 [Privacy Service概述](../../privacy-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用 [!DNL Platform] 服务。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供了RESTful API和交互式UI，让您能够轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持客户属性数据 | 支持创建流连接器以摄取客户属性数据的UI和API。 |
| 对云存储的其他文件格式支持 | 从云存储摄取的文件现在支持符合XDM规范的Parquet和JSON文件格式。 |
| 支持访问控制权限 | Adobe Experience Platform中的访问控制框架提供了授予对数据摄取中源的访问权限所需的权限。 根据用户的权限级别，用户可以查看源、管理源或完全被拒绝访问。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 数据引入 | 管理源 | 对读取、创建、编辑和禁用源的访问权限。 |
| 数据引入 | 查看源 | 对 **[!UICONTROL 目录]** 选项卡和已验证的源 **[!UICONTROL 浏览]** 选项卡。 |

**已知问题**

* 无

有关源的详细信息，请参阅 [源概述](../../sources/home.md)

## 目标 {#destinations}

在 [Real-time CDP](../../rtcdp/overview.md)，目标是与目标平台的预建集成，可无缝地向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持访问控制权限 | Real-time CDP中的“目标”功能可与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以查看、管理和激活目标。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 目标 | 管理目标 | 访问读取、创建、编辑和禁用目标。 |
| 目标 | 查看目标 | 对 **[!UICONTROL 目录]** 选项卡和已验证的目标 **浏览** 选项卡。 |
| 目标 | 激活目标 | 能够将数据激活到目标。 此权限要求将“管理目标”或“查看目标”添加到产品配置文件中。 |

**已知问题**

* 无

请参阅 [目标概述](../../destinations/home.md) 以了解更多信息。
