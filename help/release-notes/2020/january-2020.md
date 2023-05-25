---
title: Adobe Experience Platform发行说明2020年1月
description: Adobe Experience Platform 2020年1月版发行说明。
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
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

标准化和互操作性是背后的关键概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)由Adobe驱动，致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 等层级字段的字段类型限制 | 将XDM字段定义为特定类型后，无论名称和层次结构相同的任何其他字段使用的类或架构字段组是什么，这些字段都必须使用相同的字段类型。 例如，如果XDM的字段组 [!DNL Profile] 类包含 `profile.age` “整数”类型的字段，XDM的类似字段组 [!DNL ExperienceEvent] 不能具有 `profile.age` “字符串”类型的字段。 要使用不同的字段类型，字段必须具有与之前定义的字段不同的层次结构(例如， `profile.person.age`)。 此功能旨在防止将架构合并到一起时发生冲突。 虽然该限制不会对现有架构产生追溯性影响，但强烈建议您查看架构以确定字段类型冲突，并在必要时进行编辑。 |
| 区分大小写的字段验证 | 同一级别上的自定义字段必须具有不同的名称，不区分大小写。 例如，如果添加了一个名为“Email”的自定义字段，则无法在名为“email”的同一级别添加另一个自定义字段。 |

**已知问题**

* None

要了解有关使用XDM的更多信息，请使用 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用户界面，请阅读 [XDM系统文档](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和用户界面，以帮助您管理来自客户的数据请求。 替换为 [!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| [!DNL Privacy Service] 品牌再造 | 之前称为“GDPR服务”的服务已更名为 [!DNL Privacy Service] 随着服务的发展，除了GDPR之外，还支持其他法规。 |
| 新API端点 | 的基本路径 [!DNL Privacy Service] API更新自 `/data/privacy/gdpr` 到 `/data/core/privacy/jobs`. |
| 需要新增 `regulation` 属性 | 在中创建新作业时 [!DNL Privacy Service] API， a `regulation` 必须在请求有效负载中提供属性，以指示要跟踪作业的法规。 接受的值包括 `gdpr` 和 `ccpa`. |
| 支持 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] 现在接受来自Adobe的访问/删除请求 [!DNL Primetime Authentication]，使用 `primetimeAuthentication` 作为其产品价值。 |
| Privacy Service用户界面增强 | GDPR和CCPA法规的单独作业跟踪页面。 新增的**法规类型**下拉列表，用于在GDPR和CCPA的跟踪数据之间切换。 |

**已知问题**

* None

有关详情，请参阅 [!DNL Privacy Service]，请先阅读 [Privacy Service概述](../../privacy-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用来构建、标记和增强这些数据 [!DNL Platform] 服务。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

[!DNL Experience Platform] 提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持客户属性数据 | 支持创建流式连接器以摄取客户属性数据的UI和API。 |
| 云存储的其他文件格式支持 | 从云存储摄取文件现在支持符合XDM的Parquet和JSON文件格式。 |
| 支持访问控制权限 | Adobe Experience Platform中的访问控制框架提供了授予对数据摄取中源的访问权限所需的权限。 根据用户的权限级别，用户可以查看源、管理源或完全拒绝访问。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 数据引入 | 管理源 | 有权读取、创建、编辑和禁用源。 |
| 数据引入 | 查看源 | 对中的可用源的只读访问权限 **[!UICONTROL 目录]** 选项卡和经过验证的源 **[!UICONTROL 浏览]** 选项卡。 |

**已知问题**

* None

有关源的更多信息，请参见 [源概述](../../sources/home.md)

## 目标 {#destinations}

In [Real-Time CDP](../../rtcdp/overview.md)，目标是预先构建的与目标平台的集成，可无缝地向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持访问控制权限 | Real-Time CDP中的目标功能可与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以查看、管理和激活目标。 |

**访问控制权限**

| 类别 | 权限 | 描述 |
|--- | --- | ---|
| 目标 | 管理目标 | 有权读取、创建、编辑和禁用目标。 |
| 目标 | 查看目标 | 对中的可用目标的只读访问 **[!UICONTROL 目录]** 选项卡和中的已验证目标 **浏览** 选项卡。 |
| 目标 | 激活目标 | 能够将数据激活到目标。 此权限要求将“管理目标”或“查看目标”添加到产品配置文件中。 |

**已知问题**

* None

请参阅 [目标概述](../../destinations/home.md) 了解更多信息。
