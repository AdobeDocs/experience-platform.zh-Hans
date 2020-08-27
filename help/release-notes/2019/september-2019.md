---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2019年9月10日
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 5%

---


# Adobe Experience Platform 发行说明

**发行日期：2019 年 9 月 10 日**

Adobe Experience Platform现有功能更新：

* [[!DNL数据摄取]](#ingestion)
* [[!DNL数据科学工作区]](#dsw)
* [[!DNL查询服务]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform提供丰富的功能集，可采集任何类型和延迟的数据。 Adobe Experience Platform [!DNL Data Ingestion] 提供了多种数据替代方法，包括批处理API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience PlatformUI。

**新增功能**

| 功能 | 描述 |
| ----------- | ---------- |
| 流摄取的新域 | 该 `dcs.data.adobe.net` 域已移动到新的公用数据收集域 `dcs.adobedc.net`。 用户必须根据修改后的Adobe Experience Platform流摄取文档更新其实施。 与Adobe Experience Platform流摄取相关的所有文档都已更新为使用新域。 |

有关详细信息，请访 [问数据获取文档](../../ingestion/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 是一项全面管理的服务，它 [!DNL Experience Platform] 使数据科学家能够通过构建和运行机器学习模型，跨Adobe解决方案和第三方系统无缝地从数据和内容生成洞察。 [!DNL Data Science Workspace] 与端对端数 [!DNL Platform] 据科学生命周期紧密集成，并为其提供强大动力，包括探索和准备XDM数据，然后开发和运行模型以自动丰富机器学习 [!DNL Real-time Customer Profile] 的洞察。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 通过UI安排服务 | 与业务流程 [!DNL Platform] 服务集成，借助使用UI的用户定义的计划实现模型培训和评分的自动化。 |
| [!DNL Service Gallery] | 浏览、监控和访问机器学习服务，能够计划自动化培训和评分工作，一切尽在重新设计的 [!DNL Service Gallery]内。 |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] UI改进。 |

**已知问题**

* 当前，删除现有服务 [!DNL Service Gallery] 没有可访问的方式。 同时，请参阅Sensei机器 [学习API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) ，通过API调用删除现有服务。
* 没 [!DNL Service Gallery] 有分页支持来过滤服务的培训和评分运行。
* 在配置计划的培训或评分时， [!DNL Service Gallery]将频率设置为每小时会阻止应用计划。

有关详细信息，请访 [问数据科学工作区概述](../../data-science-workspace/home.md)。

## [!DNL Query Service] {#query}

[!DNL Query Service] 提供在Adobe Experience Platform使用标准SQL查询数据的能力，以支持各种分析和数据管理用例。 It is a serverless tool that allows you to join datasets from the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, [!DNL Data Science Workspace], or for ingestion into [!DNL Real-time Customer Profile].

You can use [!DNL Query Service] to build data analysis ecosystems, creating a picture of customers across their various interaction channels. 这些渠道可能包括销售点系统、Web、移动或CRM系统。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 改进功能 [!DNL Query Editor] | 添加了保存功能，允许您保存查询并稍后处理它。 在Adobe Experience Platform的用户界面中添加了“浏 [!DNL Query Service] 览”选项卡，其中显示由您组织中的用户保存的查询。 已实现“查询详细信息”面板，其中显示有关正在查看的查询的有用元数据。 |
| 新的归因函数 | Adobe定义的函数， [!DNL Query Service] 用于查询具有到期参数的渠道归因。 |
| SQL语法的增强 | 支持iLike语法。 |
| 使用定义的XDM模式生成数据集 | 在“创建表为选择(CTAS)”查询中添加了一个新子句，该子句允许您指定目标模式。 |

For more information, refer to the [Query Service documentation](../../query-service/home.md).