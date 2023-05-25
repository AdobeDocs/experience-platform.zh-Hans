---
title: Adobe Experience Platform发行说明2019年9月
description: Adobe Experience Platform 2019年9月版发行说明。
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

Adobe Experience Platform提供了一组丰富的功能，可用于摄取任何类型和延迟的数据。 Adobe Experience Platform [!DNL Data Ingestion] 为摄取数据提供了多个替代方案，包括批处理API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience Platform UI。

**新增功能**

| 功能 | 描述 |
| ----------- | ---------- |
| 用于流式摄取的新域 | 此 `dcs.data.adobe.net` 域已移至新的通用数据收集域 `dcs.adobedc.net`. 用户必须根据修订的Adobe Experience Platform流摄取文档更新其实施。 所有与Adobe Experience Platform流摄取相关的文档已更新为使用新域。 |

欲知更多信息，请访问 [数据引入文档](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 是一项完全托管的服务，位于 [!DNL Experience Platform] 它使数据科学家能够通过构建和运行机器学习模型，从Adobe解决方案和第三方系统中的数据和内容无缝地生成见解。 [!DNL Data Science Workspace] 紧密集成 [!DNL Platform] 并支持端到端的数据科学生命周期，包括XDM数据的探索和准备，然后开发和实施模型以自动丰富 [!DNL Real-Time Customer Profile] 使用机器学习分析。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 通过UI计划服务 | 与集成 [!DNL Platform] 编排服务可使用UI通过用户定义的计划自动进行模型训练和评分。 |
| [!DNL Service Gallery] | 浏览、监控和访问机器学习服务，并安排自动培训和评分工作，所有这些都在重新设计的范围内 [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI改进。 |

**已知问题**

* 中目前没有可访问的方式 [!DNL Service Gallery] 删除现有服务。 同时，请参阅 [Sensei机器学习API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 通过API调用删除现有服务。
* 此 [!DNL Service Gallery] 不支持分页以过滤服务的训练和评分运行。
* 在配置计划的培训或评分时，通过 [!DNL Service Gallery]，将频率设置为每小时，可阻止应用计划。

欲知更多信息，请访问 [数据科学工作区概述](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] 提供了在Adobe Experience Platform中使用标准SQL查询数据的能力，以支持各种分析和数据管理用例。 它是一个无服务器工具，允许您从 [!DNL Data Lake] 并将查询结果捕获为新的数据集以用于报告， [!DNL Data Science Workspace]，或进行摄取 [!DNL Real-Time Customer Profile].

您可以使用 [!DNL Query Service] 构建数据分析生态系统，全面了解客户在不同互动渠道中的行为。 这些渠道可能包括销售点系统、Web、移动或CRM系统。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 改进 [!DNL Query Editor] | 添加了保存功能，可让您保存查询并稍后处理。 向添加了“浏览”选项卡 [!DNL Query Service] Adobe Experience Platform的用户界面，其中显示由您组织中的用户保存的查询。 实施了“查询详细信息”面板，该面板显示有关正在查看的查询的有用元数据。 |
| 新的归因函数 | 中的Adobe定义函数 [!DNL Query Service] 使用过期参数查询渠道归因。 |
| 对SQL语法的增强 | 支持iLike语法。 |
| 使用定义的XDM架构生成数据集 | 在Create Table as Select (CTAS)查询中添加了新的子句，用于指定目标模式。 |

欲了解更多信息，请参见 [查询服务文档](../../query-service/home.md).
