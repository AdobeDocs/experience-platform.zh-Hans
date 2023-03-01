---
title: Adobe Experience Platform发行说明2023年2月
description: Adobe Experience Platform 2023年2月版发行说明。
source-git-commit: 0935a50527800b255901f8047051c47b45ab33b8
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 2 月 22 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据收集](#data-collection)
- [[!DNL Destinations]](#destinations)
- [体验数据模型(XDM)](#xdm)
- [查询服务](#query-service)
- [Real-Time Customer Data Platform B2B 版](#b2b)
- [源](#sources)

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中扩充和转换数据，并将其分发到Adobe或非Adobe目标。

### Assurance {#assurance}

Adobe保证允许您检查、校对、模拟和验证在移动应用程序中收集数据或提供体验的方式。

**新增或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 公共API | Adobe保障API现已可用。 Assurance API是API的集合，当用户配备了Mobile SDK的Adobe保证扩展时，这些API使用户能够测试和调试他们自己的Web和移动应用程序。 要了解有关Assurance API的更多信息，请参阅 [Assurance API概述](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style=&quot;table-layout:auto&quot;}

欲知Assurance的详情，请阅读 [保证文档](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。

**新增或更新功能** {#destinations-new-updated-features}

| 功能 | 描述 |
| ----------- | ----------- |
| [同意政策增强](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 用于与集成 [基于文件（批量）的目标](/help/destinations/destination-types.md#file-based) | <p> 当配置文件不再符合同意策略的条件时，Experience Platform现在会主动将其策略退出告知基于文件的目标。 这遵循 [2023年2月发布](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) 流目标的相同功能。 </p> <p> <b>注释</b>：此功能仅适用于以下客户： **[!UICONTROL 隐私和安全防护板]**，以及 **[!UICONTROL Health Shield]**. </p> |

{style=&quot;table-layout:auto&quot;}

**新增或更新文档** {#destinations-new-updated-documentation}

| 文档 | 描述 |
| ----------- | ----------- |
| 目标如何工作文档 | <p>我们根据用户的常见问题，发布了三篇关于目标如何工作的新解释者文章：</p> <p><ul><li>[目标中的可配置和常用导出设置](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[不同目标类型的配置文件导出行为](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[目标激活工作流中的身份处理](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一个开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 通过UI弃用字段 | 您现在可以 [摄取数据后弃用架构中的字段](../../xdm/tutorials/field-deprecation-ui.md). XDM字段弃用允许您从UI视图中删除字段，同时保留它们以供使用。 如果需要，您可以再次显示已弃用的字段，并且引用这些字段的任何区段、查询或下游解决方案都将照常运行。 |

{style=&quot;table-layout:auto&quot;}

**新XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL XDM单个潜在客户配置文件]](https://github.com/adobe/xdm/pull/1669/files) | XDM Individual Prospect Profile类引入合作伙伴提供的ID。 |

{style=&quot;table-layout:auto&quot;}

**更新的XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [!UICONTROL 频率上限约束] | 此 [!UICONTROL 频率上限约束] 字段组已 [更新了以支持重复事件和自定义事件](https://github.com/adobe/xdm/pull/1641/files). |
| 数据类型 | [!UICONTROL Web反向链接] | Web反向链接属性已 [已更新以包含 `xdm:linkName` 和 `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). 它们分别是上一页选择的HTML元素的名称和区域。 |
| 字段组 | [!UICONTROL AdobeCJM ExperienceEvent — 消息交互详细信息] | [此 [!UICONTROL 跟踪器URL] 字段已添加](https://github.com/adobe/xdm/pull/1665/files) 到 [!UICONTROL AdobeCJM ExperienceEvent]. 此跟踪器提供用户选择的URL。 |
| 字段组 | [!UICONTROL AdobeCJM ExperienceEvent — 消息交互详细信息] | [空 `meta:enum` 属性已删除](https://github.com/adobe/xdm/pull/1668/files) 从URL [!UICONTROL 跟踪类型] 字段。 |
| 数据类型 | [!UICONTROL 媒体信息] | [来自的正则表达式模式 `videoSegment` 中的属性 [!UICONTROL 媒体信息] 已删除数据类型](https://github.com/adobe/xdm/pull/1667/files). |

{style=&quot;table-layout:auto&quot;}

有关Platform中XDM的更多信息，请阅读 [XDM系统概述](../../xdm/home.md). &#x200B;

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以加入数据湖中的任何数据集，并将查询结果捕获为新数据集，以用于报表、数据科学工作区或将其摄取到实时客户档案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 使用SQL为配置文件启用数据集 | [在CTAS查询中使用LABEL使数据集“启用配置文件”](../../query-service/sql/syntax.md#create-table-as-select)，或使用ALTER更新要为配置文件启用的现有数据集。 您可以使用此扩展SQL构造为Real-Time Customer Profile业务用例提供派生属性的无缝支持。 请参阅 [派生属性文档的无缝SQL流](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md) 了解更多详细信息。 |
| 监视计划查询 | 使用 [“计划查询”选项卡](../../query-service/ui/monitor-queries.md) 查找有关查询运行的重要信息并订阅警报。 监测计划详细信息、状态和错误消息/代码失败（如果失败）的查询。 |
| 切换自动完成功能 | 通过消除某些元数据命令并缩短处理时间 [切换查询编辑器自动完成功能](../../query-service/ui/user-guide.md#auto-complete). 此功能会在您编写查询时自动为查询建议潜在的SQL关键字和表详细信息。 |
| 数据集示例 | 在查询中指定采样率并 [使用数据集样本创建统一的随机样本](../../query-service/essential-concepts/dataset-samples.md)，或根据特定条件创建条件示例。 |

{style=&quot;table-layout:auto&quot;}

有关查询服务的详细信息，请参阅 [查询服务概述](../../query-service/home.md).


## Real-Time Customer Data Platform B2B 版 {#b2b}

Real-Time CDP B2B版构建于Real-time Customer Data Platform (Real-Time CDP)之上，专为以B2B服务模式运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其合并到人员和帐户配置文件的单一视图中。 此统一数据允许营销人员准确地定位特定受众，并在所有可用渠道中吸引这些受众。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 启用相关帐户服务 | 新的切换功能允许您在帐户上启用相关的帐户服务。 有关详细信息，请阅读以下指南： [启用相关的帐户服务](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

要了解有关Real-Time CDP B2B版本的更多信息，请阅读 [Real-Time CDP B2B版本概述](../../rtcdp/overview.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 指定订阅级别的访问权限 [!DNL Google PubSub] | 现在，在使用时，您可以定义对特定主题订阅的访问权限 [!DNL Google PubSub] 源，方法是在身份验证时提供订阅ID。 有关详细信息，请阅读 [!DNL Google PubSub] 身份验证教程 [使用流服务API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) 或 [平台UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| 从引入自定义活动数据 [!DNL Marketo] | 您现在可以从以下位置引入自定义活动数据 [!DNL Marketo] 实例到Experience Platform。 要摄取自定义活动数据，您必须在B2B活动架构中设置自定义活动字段组，并使用活动数据集创建数据流。 数据流完成后，摄取的数据集将包含中的标准活动和自定义活动 [!DNL Marketo] 实例。 然后，您可以使用 [查询服务](../../query-service/home.md) 以访问Platform上的自定义活动记录。 有关详细信息，请阅读以下指南： [为自定义活动数据创建数据流](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| 从排除无人认领的帐户 [!DNL Marketo] | 您现在可以配置在为公司数据创建数据流时是希望从引入中排除还是包含无人认领的帐户。 有关详细信息，请阅读以下指南： [创建源连接和数据流 [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

要了解有关来源的更多信息，请阅读 [源概述](../../sources/home.md).
