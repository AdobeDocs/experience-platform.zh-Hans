---
title: Adobe Experience Platform 发行说明（2020 年 1 月）
description: Adobe Experience Platform 的 2020 年 1 月发行说明。
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 24%

---

# Adobe Experience Platform 发行说明

**发行日期： 2020年1月15日**

Adobe Experience Platform 中现有功能的更新：

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是[!DNL Experience Platform]背后的关键概念。 由Adobe驱动的[!DNL Experience Data Model] (XDM)致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 等层级字段的字段类型限制 | 将XDM字段定义为特定类型后，无论在中使用何种类或架构字段组，具有相同名称和层次结构的任何其他字段都必须使用相同的字段类型。 例如，如果XDM [!DNL Profile]类的字段组包含“整数”类型的`profile.age`字段，则XDM [!DNL ExperienceEvent]的类似字段组不能包含“字符串”类型的`profile.age`字段。 为了利用不同的字段类型，该字段必须具有与之前定义的字段不同的层次结构（例如，`profile.person.age`）。 此功能旨在防止将架构合并到一起时发生冲突。 虽然该限制不会对现有架构产生追溯性影响，但强烈建议您查看架构以确定字段类型冲突，并在必要时进行编辑。 |
| 区分大小写的字段验证 | 同一级别上的自定义字段必须具有不同的名称，不区分大小写。 例如，如果添加名为“Email”的自定义字段，则无法在名为“email”的同一级别添加其他自定义字段。 |

**已知问题**

* None

要了解有关使用[!DNL Schema Registry] API和[!DNL Schema Editor]用户界面使用XDM的更多信息，请阅读[XDM系统文档](../../xdm/home.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和组织法规授予用户权利，允许他们根据请求从您的数据存储中访问或删除其个人数据。 Adobe Experience Platform [!DNL Privacy Service] 提供 RESTful API 和用户界面，帮助您管理客户数据请求。借助 [!DNL Privacy Service]，您可以提交从 Adobe Experience Cloud 应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| [!DNL Privacy Service] 品牌重塑 | 之前的“GDPR 服务”现已更名为 [!DNL Privacy Service]，因为该服务经过发展现在支持 GDPR 之外的其他法规。 |
| 新的 API 端点 | [!DNL Privacy Service] API的基本路径已从`/data/privacy/gdpr`更新为`/data/core/privacy/jobs`。 |
| 新的必需 `regulation` 属性 | 在 [!DNL Privacy Service] API 中创建新作业时，必须在请求负载中提供 `regulation` 属性，以指示根据哪条规定跟踪该作业。接受的值为`gdpr`和`ccpa`。 |
| 支持 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service]现在接受来自Adobe [!DNL Primetime Authentication]的访问/删除请求，使用`primetimeAuthentication`作为其产品值。 |
| Privacy Service UI增强 | 根据GDPR和CCPA法规，单独设置作业跟踪页面。 新的&#x200B;**法规类型**&#x200B;下拉列表，用于在GDPR和CCPA的跟踪数据之间切换。 |

**已知问题**

* None

有关[!DNL Privacy Service]的详细信息，请先阅读[Privacy Service概述](../../privacy-service/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强该数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform]提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持客户属性数据 | 支持创建流式连接器以摄取客户属性数据的UI和API。 |
| 云存储的其他文件格式支持 | 从云存储中摄取的文件现在支持符合XDM的Parquet和JSON文件格式。 |
| 支持访问控制权限 | Adobe Experience Platform中的访问控制框架提供了授予对摄取数据中的源的访问权限所需的权限。 根据用户的权限级别，用户可以查看源、管理源或被拒绝访问。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 数据引入 | 管理源 | 有权读取、创建、编辑和禁用源。 |
| 数据引入 | 查看源 | 对&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中的可用源以及&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中的已验证源的只读访问权限。 |

**已知问题**

* None

有关源的更多信息，请参阅[源概述](../../sources/home.md)

## 目标 {#destinations}

在[Real-Time CDP](../../rtcdp/overview.md)中，目标是与目标平台预先构建的集成，这些平台以无缝方式向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持访问控制权限 | Real-Time CDP中的目标功能可与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以查看、管理和激活目标。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 目标 | 管理目标 | 有权读取、创建、编辑和禁用目标。 |
| 目标 | 查看目标 | 对&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中的可用目标和&#x200B;**浏览**&#x200B;选项卡中的已验证目标的只读访问。 |
| 目标 | 激活目标 | 能够将数据激活到目标。 此权限要求将“管理目标”或“查看目标”添加到产品配置文件中。 |

**已知问题**

* None

有关详细信息，请参阅[目标概述](../../destinations/home.md)。
