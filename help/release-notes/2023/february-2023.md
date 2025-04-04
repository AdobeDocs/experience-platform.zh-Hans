---
title: Adobe Experience Platform 发行说明（2023 年 2 月）
description: Adobe Experience Platform 的 2023 年 2 月发行说明。
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 91%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 2 月 22 日**

Adobe Experience Platform 中现有功能的更新：

- [数据收集](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [查询服务](#query-service)
- [Real-Time Customer Data Platform B2B 版](#b2b)
- [源](#sources)

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

### Assurance {#assurance}

Adobe Assurance 可帮助您检查、校对、模拟和验证您在移动应用程序中收集数据或提供体验的方式。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 公共 API | Adobe Assurance API 现已推出。Assurance API 是 API 的收藏集，当用户配备带有 Mobile SDK 的 Adobe Assurance 扩展时，它们使用户能够测试和调试自己的 Web 和移动应用程序。要详细了解 Assurance API，请阅读 [Assurance API 概述](https://developer.adobe.com/adobe-assurance-public-apis/)。 |

{style="table-layout:auto"}

有关 Assurance 的详细信息，请阅读 [Assurance 文档](https://developer.adobe.com/client-sdks/documentation/platform-assurance/)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增功能或更新后的功能** {#destinations-new-updated-features}

| 功能 | 描述 |
| ----------- | ----------- |
| [同意策略增强](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement)用于与[基于文件（批次）的目标](/help/destinations/destination-types.md#file-based)集成 | <p> 当轮廓不再符合同意策略时，Experience Platform 现在会主动将其策略退出通知给基于文件的目标。这是在[ 2023 年 2 月发布](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality)用于流媒体目标的相同功能后推出的。 </p> <p> <b>注释</b>：此功能仅适用于&#x200B;**[!UICONTROL Privacy and Security Shield]**&#x200B;以及&#x200B;**[!UICONTROL Healthcare Shield]**&#x200B;的客户。 </p> |

{style="table-layout:auto"}

**新增或更新文档**{#destinations-new-updated-documentation}

| 文档 | 描述 |
| ----------- | ----------- |
| 目标如何运作文档 | <p>我们根据用户的常见问题发布了三篇关于目标如何运作的新文章：</p> <p><ul><li>[目标中可配置的通用导出设置](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[不同目标类型的轮廓导出行为](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[目标激活工作流程中的身份标识处理](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 通过 UI 弃用字段 | 现在可[在摄取数据后从架构中弃用字段](../../xdm/tutorials/field-deprecation-ui.md)。XDM 字段弃用功能允许您从 UI 视图中删除字段，同时保留它们以供使用。如果需要，您可以再次显示已弃用的字段，引用这些字段的任何区段、查询或下游解决方案都将照常运行。 |

{style="table-layout:auto"}

**新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL XDM 单个潜在客户轮廓]](https://github.com/adobe/xdm/pull/1669/files) | XDM 单个潜在客户轮廓类引入了合作伙伴提供的 ID。 |

{style="table-layout:auto"}

**更新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [!UICONTROL 频次封顶约束] | [!UICONTROL 频次封顶约束]字段组已[更新以支持重复和自定义事件](https://github.com/adobe/xdm/pull/1641/files)。 |
| 数据类型 | [!UICONTROL Web 反向链接] | Web 反向链接属性已[更新，以包括 `xdm:linkName` 和 `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files)。它们分别是在上一页上选择的 HTML 元素的名称和区域。 |
| 字段组 | [!UICONTROL Adobe CJM ExperienceEvent - 消息交互详细信息] | [已将[!UICONTROL 跟踪器 URL ]字段添加](https://github.com/adobe/xdm/pull/1665/files)到 [!UICONTROL Adobe CJM ExperienceEvent]。此跟踪器提供由用户选择的 URL。 |
| 字段组 | [!UICONTROL Adobe CJM ExperienceEvent - 消息交互详细信息] | [空的`meta:enum`属性已从 URL [!UICONTROL 跟踪类型] 字段中删除](https://github.com/adobe/xdm/pull/1668/files)。 |
| 数据类型 | [!UICONTROL 媒体信息] | [[!UICONTROL 媒体信息]数据类型中`videoSegment`属性的正则表达式模式已删除](https://github.com/adobe/xdm/pull/1667/files)。 |

{style="table-layout:auto"}

有关Experience Platform中XDM的更多信息，请阅读[XDM系统概述](../../xdm/home.md)&#x200B;。

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL Data Lake] 中的数据。您可以加入数据湖的任何数据集，并作为新数据集获取查询结果，以用于报表、Data Science Workspace，或将数据摄取到实时客户轮廓。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 使用 SQL 为轮廓启用数据集 | [在 CTAS 查询中使用 LABEL 使数据集“启用轮廓”](../../query-service/sql/syntax.md#create-table-as-select)，或使用 ALTER 更新要为轮廓启用的现有数据集。您可以使用此扩展的SQL构造为Real-time Customer Profile业务用例提供对派生数据集的无缝支持。 有关更多详细信息，请参阅派生数据集的[无缝SQL流文档](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md)。 |
| 监测计划查询 | 使用[计划查询选项卡](../../query-service/ui/monitor-queries.md)，查找有关查询运行的重要信息并订阅警报。监测查询以获取计划详细信息、状态和错误消息/代码（如果失败）。 |
| 切换自动完成功能 | [切换查询编辑器自动完成功能](../../query-service/ui/user-guide.md#auto-complete)，消除某些元数据命令并缩短处理时间。此功能会在您编写查询时自动建议潜在的 SQL 关键字和表详细信息。 |
| 数据集样本 | 在查询中指定采样率，[使用数据集样本创建统一随机样本](../../query-service/key-concepts/dataset-samples.md)，或根据特定标准创建条件样本。 |

{style="table-layout:auto"}

有关查询服务的详细信息，请参阅[查询服务概述](../../query-service/home.md)。


## Real-Time Customer Data Platform B2B 版 {#b2b}

Real-Time CDP B2B 版本基于 Real-Time Customer Data Platform (Real-Time CDP) 构建，专为采用业务对业务服务模式运营的营销人员而构建。它将来自多个来源的数据汇集在一起&#x200B;，并将其组合成人员和帐户轮廓的单一视图。这种统一的数据使营销人员能够精确锁定特定受众，并通过所有可用渠道吸引这些受众。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 启用关联账户服务 | 新的切换功能允许您在您的帐户上启用相关帐户服务。有关更多信息，请阅读有关[启用相关账户服务](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable)的指南。 |

{style="table-layout:auto"}

要详细了解 Real-Time CDP B2B 版本，请阅读 [Real-Time CDP B2B 版本概述](../../rtcdp/overview.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 用 [!DNL Google PubSub] 指定订阅级访问权限 | 现在，您可以通过在身份验证时提供订阅 ID 来定义在使用 [!DNL Google PubSub] 源时对特定主题订阅的访问权限。有关详细信息，请使用流服务API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md)或[Experience Platform UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md)阅读[!DNL Google PubSub]身份验证教程[。 |
| 从 [!DNL Marketo] 提取自定义活动数据 | 您现在可以将自定义活动数据从 [!DNL Marketo] 实例带到 Experience Platform。要提取自定义活动数据，您必须在 B2B 活动架构中设置自定义活动字段组，并使用活动数据集创建数据流。完成数据流后，摄取的数据集将会包含来自 [!DNL Marketo] 实例的标准和自定义活动。然后，您可以使用[查询服务](../../query-service/home.md)来访问Experience Platform上的自定义活动记录。 若要了解更多信息，请阅读有关[为自定义活动数据创建数据流](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md)的指南。 |
| 从 [!DNL Marketo] 中排除无人认领的帐户 | 现在，您可以配置在为公司数据创建数据流时是否要排除或包含无人认领的帐户。若要了解更多信息，请阅读有关[为  [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md) 创建源连接和数据流的指南。 |

{style="table-layout:auto"}

若要了解有关源的更多信息，请阅读[源概述](../../sources/home.md)。
