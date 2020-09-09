---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年9月9日
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 312794af2cdb111fb81c0aa226dec68db2cbc374
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 4%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 9 月 9 日**

Adobe Experience Platform现有功能更新：

- [[!DNL数据管理]](#governance)
- [[!DNL目标]](#destinations)
- [[!DNL可观性洞察]](#observability)
- [[!DNLPrivacy Service]](#privacy)
- [[!DNL实时客户用户档案]](#profile)
- [[!DNL分段服务]](#segmentation)
- [[!DNL源]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform数据治理是用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策的一系列战略和技术。 它在各个层次中都起 [!DNL Experience Platform] 着关键作用，包括编目、数据谱系、数据使用标签、数据访问策略和访问控制营销行动的数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据集标记UI增强功能 | 为了更轻松地处理大型模式，已在数据集标签UI中添加了多个新的排序和过滤控件： <ul><li>根据完整的模式路径按字母顺序对字段排序。</li><li>对字段路径名执行部分搜索。</li><li>筛选没有标签、选定标签或标签类别的字段。</li></ul> |

有关该 [服务的更多信息](../../data-governance/home.md) ，请参阅数据管理概述。

## 目标 {#destinations}

在 [Adobe实时数据平台中](../../rtcdp/overview.md)，目标是预建的与目标平台集成，以无缝方式向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| UX改进 | 用户可以访问内联表操作，以更轻松地访问主操作，如添加数据、编辑计划和添加区段。 有关详细 [信息，请参](../../rtcdp/destinations/destinations-workspace.md) 阅目标工作区文档。 |

要了解更多信息，请访问目 [标概述](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] 允许您通过使用统计指标和活动通知来监视Adobe Experience Platform的事件。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| AdobeI/O事件通知 | [!DNL Observability Insights] 利用AdobeI/O事件为多个Experience Platform服务创建事件通知。 通知负载将发送到已配置的网络挂接，然后您可以使用它来自动执行进一步的下游流程。 有关更多 [信息，请参](../../observability/notifications/overview.md) 阅通知概述。 |

有关该 [[!DNL Observability Insights] 服务的](../../observability/home.md) 更多信息，请参阅概述。

## [!DNL Privacy Service] {#privacy}

一些法律和组织法规允许用户根据请求从数据存储中访问或删除其个人数据。 Adobe Experience Platform [!DNL Privacy Service] 提供了RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 您可 [!DNL Privacy Service]以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持LGPD（巴西） | 如今，隐私工作可以根据巴西的(LGPD) [!DNL Lei Geral de Proteção de Dados] 法规创造。 这些工作是根据监管法规进行跟踪的 `lgpd_bra`。 |

有关该 [服务的更](../../privacy-service/home.md) 多信息，请参阅Privacy Service概述。

## 实时客户资料 {#profile}

Adobe Experience Platform使您能够为客户提供协调、一致和相关的体验，无论客户在何处或何时与您的品牌互动。 您 [!DNL Real-time Customer Profile]可以看到每个客户的整体视图，该渠道组合了多个的数据，包括在线、离线、CRM和第三方数据。 [!DNL Profile] 允许您将不同的客户数据整合到统一的视图中，为每次客户互动提供可操作、有时间戳的帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 用户档案查看器 | 用户档案查看器在平台UI中已更新为完全自定义的仪表板。 用户现在可以选择执行以下任务: <ul><li>更新基本信息构件中选定的标准属性和自定义属性。</li><li>创建、编辑和删除自定义构件</li><li>调整构件大小并重新排列构件</li></ul> |

有关更多信息( [!DNL Real-time Customer Profile]包括有关使用数据的教程和最 [!DNL Profile] 佳实践)，请阅 [读实时客户用户档案概述](../../profile/home.md)。

## 分段服务 {#segmentation}

Adobe Experience Platform分段服务提供用户界面和RESTful API，使您能够构建细分并根据数据生成 [!DNL Real-time Customer Profile] 受众。 这些细分集中配置并维护， [!DNL Platform]使任何Adobe应用程序都能轻松访问它们。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准，定义特定的用户档案子集。 细分可以基于记录数据（如人口统计信息）或表示客户与您品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 导出作业 | 添加了标记，以允许将区段评估为导出作业的一部分。 因此，用户可以在单个作业中运行分段和导出。 |
| 合并策略 | 可以在单个批处理分段作业中包含多个合并策略。 |

有关的详细信 [!DNL Segmentation Service]息，请参阅分 [段概述](../../segmentation/home.md)

## 源 {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用服务来构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 自动映射 | [!DNL Platform] 根据用户选择的目标模式或数据集，为数据获取工作流期间的自动映射提供智能建议。 您可以手动调整灵活的自动映射规则以适合您的使用情况。 |
| UX改进 | 用户可以访问内联表操作，以更轻松地访问主操作，如添加数据、编辑计划和添加区段。 有关详细 [信息，请参见](../../sources/tutorials/ui/monitor.md) “监视数据流”文档。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md)。
