---
title: Adobe Experience Platform发行说明2019年9月
description: 2019年9月版Adobe Experience Platform发行说明。
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发布日期：2019 年 9 月 10 日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform提供丰富的功能集，用于摄取任何类型的数据和延迟。 Adobe Experience Platform [!DNL Data Ingestion] 提供了多个用于摄取数据的替代方法，包括批量API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience Platform UI。

**新增功能**

| 功能 | 描述 |
| ----------- | ---------- |
| 用于流式引入的新域 | 的 `dcs.data.adobe.net` 域已移至新的常用数据收集域 `dcs.adobedc.net`. 用户必须根据修订的Adobe Experience Platform流摄取文档更新其实施。 所有与Adobe Experience Platform流摄取相关的文档都已更新，可使用新域。 |

有关更多信息，请访问 [数据摄取文档](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 是 [!DNL Experience Platform] 通过构建和运行机器学习模型，数据科学家能够跨Adobe解决方案和第三方系统无缝地从数据和内容生成洞察。 [!DNL Data Science Workspace] 与 [!DNL Platform] 并支持端到端数据科学的生命周期，包括探索和准备XDM数据，随后开发和实施模型以自动丰富 [!DNL Real-Time Customer Profile] 和机器学习分析。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 通过UI计划服务 | 与集成 [!DNL Platform] 编排服务，使用UI通过用户定义的计划自动进行模型培训和评分。 |
| [!DNL Service Gallery] | 浏览、监控和访问机器学习服务，并能够计划自动培训和评分工作，所有这些工作都在重新设计的 [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI改进。 |

**已知问题**

* 当前，中没有可访问的方式 [!DNL Service Gallery] 删除现有服务。 同时，请参阅 [Sensei机器学习API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 通过API调用删除现有服务。
* 的 [!DNL Service Gallery] 不支持分页以过滤服务的培训和评分运行。
* 在配置计划培训或评分时，将通过 [!DNL Service Gallery]，将频率设置为每小时可阻止应用计划。

有关更多信息，请访问 [数据科学工作区概述](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] 提供使用标准SQL在Adobe Experience Platform中查询数据的功能，以支持各种分析和数据管理用例。 它是一个无服务器工具，允许您连接 [!DNL Data Lake] 并将查询结果捕获为新数据集以用于报表， [!DNL Data Science Workspace]或 [!DNL Real-Time Customer Profile].

您可以使用 [!DNL Query Service] 构建数据分析生态系统，创建客户在各种交互渠道中的全景图。 这些渠道可能包括销售点系统、Web、移动设备或CRM系统。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 改进了 [!DNL Query Editor] | 添加了保存函数，以便保存查询并稍后对其进行处理。 在 [!DNL Query Service] Adobe Experience Platform上的用户界面，显示由您组织中的用户保存的查询。 实施了“查询详细信息”面板，该面板显示有关所查看查询的有用元数据。 |
| 新的归因函数 | Adobe定义的函数 [!DNL Query Service] 用于使用过期参数查询渠道归因。 |
| 对SQL语法的增强 | 支持iLike语法。 |
| 使用定义的XDM架构生成数据集 | 在创建表作为选择(CTAS)查询中添加了新子句，该子句允许您指定目标架构。 |

有关更多信息，请参阅 [查询服务文档](../../query-service/home.md).
