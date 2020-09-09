---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年9月9日
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 64b6b59923d549cdcbf35d2e375529aec8cf81b8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 9 月 9 日**

Adobe Experience Platform现有功能更新：

* [[!DNL数据管理]](#governance)
* [[!DNL目标]](#destinations)
* [[!DNL源]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform数据治理是用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策的一系列战略和技术。 它在各个层次中都起 [!DNL Experience Platform] 着关键作用，包括编目、数据谱系、数据使用标签、数据访问策略和访问控制营销行动的数据。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 数据集标记UI增强功能 | 为了更轻松地处理大型模式，已在数据集标签UI中添加了多个新的排序和过滤控件： <ul><li>根据完整的模式路径按字母顺序对字段排序。</li><li>对字段路径名执行部分搜索。</li><li>筛选没有标签、选定标签或标签类别的字段。</li></ul> |

有关该 [服务的更多信息](../../data-governance/home.md) ，请参阅数据管理概述。

## 目标 {#destinations}

在 [Adobe实时数据平台中](../../rtcdp/overview.md)，目标是预建的与目标平台集成，以无缝方式向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| UX改进 | 用户可以访问内联表操作，以更轻松地访问主操作，如添加数据、编辑计划和添加区段。 有关详细 [信息，请参](../../rtcdp/destinations/destinations-workspace.md) 阅目标工作区文档。 |

要了解更多信息，请访问目 [标概述](../../rtcdp/destinations/destinations-overview.md)

## 源 {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用服务来构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 自动映射 | [!DNL Platform] 根据用户选择的目标模式或数据集，为数据获取工作流期间的自动映射提供智能建议。 您可以手动调整灵活的自动映射规则以适合您的使用情况。 |
| UX改进 | 用户可以访问内联表操作，以更轻松地访问主操作，如添加数据、编辑计划和添加区段。 有关详细 [信息，请参见](../../sources/tutorials/ui/monitor.md) “监视数据流”文档。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md)。