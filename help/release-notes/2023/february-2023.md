---
title: Adobe Experience Platform发行说明2023年2月
description: 2023年2月版Adobe Experience Platform发行说明。
source-git-commit: 72ae96f72bfffe376fec5c0e1dcf79406cb86a26
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 2 月 22 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Destinations]](#destinations)
- [体验数据模型(XDM)](#xdm)
- [查询服务](#query-service)
- [Real-Time Customer Data Platform B2B 版](#b2b)
- [源](#sources)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新增功能或更新功能** {#destinations-new-updated-features}

| 功能 | 描述 |
| ----------- | ----------- |
| [同意策略增强](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 与 [基于文件（批处理）的目标](/help/destinations/destination-types.md#file-based) | <p> 当用户档案不再符合同意策略的条件时，Experience Platform现在会主动将其策略退出通信到基于文件的目标。 这跟 [2023年2月发布](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) 流目标的相同功能。 </p> <p> <b>注意</b>:此功能仅适用于 **[!UICONTROL 隐私和安全防护]**，以及 **[!UICONTROL 医疗盾]**. </p> |

{style=&quot;table-layout:auto&quot;}

**新文档或更新的文档** {#destinations-new-updated-documentation}

| 文档 | 描述 |
| ----------- | ----------- |
| 目标工作原理文档 | <p>我们根据用户的常见问题发布了三篇关于目标工作方式的新解释文章：</p> <p><ul><li>[目标中的可配置和常用导出设置](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[不同目标类型的配置文件导出行为](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[目标激活工作流中的身份处理](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 通过UI弃用字段 | 您现在可以 [摄取数据后，将弃用架构中的字段](../../xdm/tutorials/field-deprecation-ui.md). XDM字段弃用允许您从UI视图中删除字段，同时保留这些字段以供使用。 如果需要，您可以再次显示已弃用的字段，并且引用这些字段的任何区段、查询或下游解决方案将照常运行。 |

{style=&quot;table-layout:auto&quot;}

**新的XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL XDM单个潜在客户配置文件]](https://github.com/adobe/xdm/pull/1669/files) | XDM Individual Prospect Profile类引入了合作伙伴提供的ID。 |

{style=&quot;table-layout:auto&quot;}

**更新了XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [!UICONTROL 频度上限约束] | 的 [!UICONTROL 频度上限约束] 字段组 [更新以支持重复事件和自定义事件](https://github.com/adobe/xdm/pull/1641/files). |
| 数据类型 | [!UICONTROL Web反向链接] | Web反向链接属性已 [已更新以包含 `xdm:linkName` 和 `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). 分别是在上一页面上选择的HTML元素的名称和区域。 |
| 字段组 | [!UICONTROL AdobeCJM ExperienceEvent — 消息交互详细信息] | [的 [!UICONTROL 跟踪器URL] 字段](https://github.com/adobe/xdm/pull/1665/files) 到 [!UICONTROL AdobeCJM ExperienceEvent]. 此跟踪器提供用户选择的URL。 |
| 字段组 | [!UICONTROL AdobeCJM ExperienceEvent — 消息交互详细信息] | [空 `meta:enum` 属性已删除](https://github.com/adobe/xdm/pull/1668/files) 从URL [!UICONTROL 跟踪类型] 字段。 |
| 数据类型 | [!UICONTROL 媒体信息] | [从 `videoSegment` 属性 [!UICONTROL 媒体信息] 数据类型已删除](https://github.com/adobe/xdm/pull/1667/files). |

{style=&quot;table-layout:auto&quot;}

有关Platform中XDM的更多信息，请阅读 [XDM系统概述](../../xdm/home.md). &#x200B;

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以加入来自数据湖的任何数据集，并作为新数据集捕获查询结果，以用于报表、Data Science Workspace或将其摄取到实时客户资料中。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 为使用SQL的配置文件启用数据集 | [在CTAS查询中使用LABEL来创建数据集“启用了配置文件”](../../query-service/sql/syntax.md#create-table-as-select)，或使用ALTER更新要为配置文件启用的现有数据集。 您可以使用此扩展SQL结构为实时客户资料业务用例的派生属性提供无缝支持。 请参阅 [派生属性文档的无缝SQL流](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md) 以了解更多详细信息。 |
| 监视计划查询 | 使用 [“计划查询”选项卡](../../query-service/ui/monitor-queries.md) 以查找有关查询运行和订阅警报的重要信息。 如果计划详细信息、状态和错误消息/代码失败，则监视查询。 |
| 切换自动完成功能 | 通过消除某些元数据命令并缩短处理时间 [切换查询编辑器自动完成功能](../../query-service/ui/user-guide.md#auto-complete). 此功能会在您编写查询时自动为查询建议潜在的SQL关键字和表详细信息。 |
| 数据集示例 | 在查询中指定采样率，并 [使用数据集示例创建统一的随机示例](../../query-service/essential-concepts/dataset-samples.md)，或根据特定条件创建条件示例。 |

{style=&quot;table-layout:auto&quot;}

有关查询服务的更多信息，请参阅 [查询服务概述](../../query-service/home.md).


## Real-Time Customer Data Platform B2B 版 {#b2b}

Real-Time CDP B2B Edition基于Real-time Customer Data Platform(Real-Time CDP)而构建，专为以企业对企业服务模式运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其整合为人员和帐户配置文件的单一视图。 通过这种统一的数据，营销人员可以准确定位特定受众并在所有可用渠道中吸引这些受众。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 启用相关帐户服务 | 新的切换功能允许您在帐户上启用相关帐户服务。 有关更多信息，请阅读 [启用相关帐户服务](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

要了解有关Real-Time CDP B2B Edition的更多信息，请阅读 [Real-Time CDP B2B版概述](../../rtcdp/overview.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 指定订阅级别访问 [!DNL Google PubSub] | 现在，您可以在使用 [!DNL Google PubSub] 来源，方法是在进行身份验证时提供订阅ID。 有关更多信息，请阅读 [!DNL Google PubSub] 身份验证教程 [使用流量服务API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) 或 [平台UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| 从中摄取自定义活动数据 [!DNL Marketo] | 您现在可以从 [!DNL Marketo] 实例Experience Platform。 要摄取自定义活动数据，您必须在B2B活动架构中设置自定义活动字段组，并使用活动数据集创建数据流。 数据流完成后，摄取的数据集将同时包含您 [!DNL Marketo] 实例。 然后，您可以使用 [查询服务](../../query-service/home.md) 以在Platform上访问自定义活动记录。 有关更多信息，请阅读 [为自定义活动数据创建数据流](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| 从 [!DNL Marketo] | 现在，您可以配置在为公司数据创建数据流时，是要从摄取中排除还是包含未声明的帐户。 有关更多信息，请阅读 [创建源连接和数据流 [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

要进一步了解来源，请阅读 [源概述](../../sources/home.md).
