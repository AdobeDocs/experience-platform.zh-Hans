---
title: Adobe Experience Platform 发行说明（2019 年 9 月）
description: Adobe Experience Platform 2019 年 9 月发行说明。
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 8%

---

# Adobe Experience Platform 发行说明

**发行日期： 2019年9月10日**

Adobe Experience Platform 中现有功能的更新：

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform提供了一组丰富的功能，可用于摄取任何类型和延迟的数据。 Adobe Experience Platform [!DNL Data Ingestion]提供了多种方法来摄取数据，包括批处理API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience Platform UI。

**新增功能**

| 功能 | 描述 |
| ----------- | ---------- |
| 用于流式摄取的新域 | `dcs.data.adobe.net`域已移至新的通用数据收集域`dcs.adobedc.net`。 用户必须根据修订的Adobe Experience Platform流摄取文档更新其实施。 所有与Adobe Experience Platform流摄取相关的文档都已更新为使用新域。 |

有关详细信息，请访问[数据摄取文档](../../ingestion/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace]是[!DNL Experience Platform]中的完全托管服务，它通过构建和运行机器学习模型，使数据科学家能够跨Adobe解决方案和第三方系统无缝地从数据和内容生成见解。 [!DNL Data Science Workspace]与[!DNL Experience Platform]紧密集成，支持端到端数据科学生命周期，包括探索和准备XDM数据，然后开发和操作模型，以使用机器学习分析自动丰富[!DNL Real-Time Customer Profile]。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 通过用户界面安排服务 | 与[!DNL Experience Platform]编排服务集成，以使用UI通过用户定义的计划自动进行模型训练和评分。 |
| [!DNL Service Gallery] | 浏览、监控和访问机器学习服务，并安排自动训练和评分作业，所有这些都在重新设计的[!DNL Service Gallery]内。 |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab]用户界面改进。 |

**已知问题**

* [!DNL Service Gallery]中当前没有删除现有服务的访问方式。 同时，请参阅[Sensei机器学习API引用](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/)以通过API调用删除现有服务。
* [!DNL Service Gallery]不支持对服务的训练和评分运行进行分页。
* 在整个[!DNL Service Gallery]中配置计划的训练或评分运行时，将频率设置为每小时可阻止应用计划。

有关详细信息，请访问[数据科学Workspace概述](../../data-science-workspace/home.md)。

## [!DNL Query Service] {#query}

[!DNL Query Service]提供在Adobe Experience Platform中使用标准SQL查询数据的功能，以支持各种分析和数据管理用例。 它是一个无服务器工具，允许您从[!DNL Data Lake]加入数据集，并将查询结果捕获为新的数据集，以用于报告[!DNL Data Science Workspace]或将其摄取到[!DNL Real-Time Customer Profile]中。

您可以使用[!DNL Query Service]构建数据分析生态系统，从而创建客户在各种交互渠道中的全景图。 这些渠道可能包括销售点系统、Web、移动或CRM系统。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 对[!DNL Query Editor]的改进 | 添加了保存功能，允许您保存查询并稍后处理它。 在Adobe Experience Platform的[!DNL Query Service]用户界面中添加了“浏览”选项卡，该选项卡显示由您组织中的用户保存的查询。 实施了“查询详细信息”面板，该面板可显示有关正在查看的查询的有用元数据。 |
| 新的归因函数 | [!DNL Query Service]中的Adobe定义的函数，用于通过过期参数查询渠道归因。 |
| 对SQL语法的增强 | 支持Like语法。 |
| 使用定义的XDM架构生成数据集 | 在Create Table as Select (CTAS)查询中添加了新的子句，用于指定目标模式。 |

有关详细信息，请参阅[查询服务文档](../../query-service/home.md)。
