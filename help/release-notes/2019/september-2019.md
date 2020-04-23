---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2019年9月10日
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 26568ebbbe48b5a82e4f6b5cf035c354c11e8ed1

---


# Adobe Experience Platform 发行说明

## 发行日期：2019 年 9 月 10 日

对Adobe Experience Platform中现有功能的更新：

* [数据摄取](#ingestion)
* [数据科学工作区](#dsw)
* [查询服务](#query)

## 数据摄取 {#ingestion}

Adobe Experience Platform提供一组丰富的功能，用于摄取任何类型的数据和延迟。 Adobe Experience Platform Data Ingestion为获取数据提供了多种替代方法，包括批量API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience Platform UI。

**新增功能**

| 功能 | 描述 |
| ----------- | ---------- |
| 流摄取的新域 | 该 `dcs.data.adobe.net` 域已移至新的公用数据收集域 `dcs.adobedc.net`。 用户必须根据修订的Adobe Experience Platform流摄取文档更新其实施。 与Adobe Experience Platform流摄取相关的所有文档均已更新为使用新域。 |

有关详细信息，请访问数 [据摄取文档](../../ingestion/home.md)。

## 数据科学工作区 {#dsw}

Adobe Experience Platform Data Science Workspace是Experience Platform中的一项全面管理服务，它使数据科学家能够通过构建和操作机器学习模型，跨Adobe解决方案和第三方系统无缝地从数据和内容生成洞察。 数据科学工作区与平台紧密集成，支持端对端数据科学的生命周期，包括探索和准备XDM数据，然后开发并实施模型，以利用机器学习洞察自动丰富实时客户用户档案。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 通过UI安排服务 | 与Platform Orcheration Service集成，使用UI通过用户定义的计划自动进行模型培训和评分。 |
| 服务库 | 浏览、监视和访问机器学习服务，并能够在经过重新设计的服务库中计划自动培训和评分工作。 |
| JupyterLab 5.0.0 | JupyterLab UI改进。 |

**已知问题**

* 当前，服务库中没有可用于删除现有服务的可访问方式。 同时，请参阅 [Sensei机器学习API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) ，通过API调用删除现有服务。
* 服务库不支持分页以过滤服务的培训和评分运行。
* 在通过服务库配置计划的培训或评分时，将频率设置为每小时会阻止应用计划。

有关详细信息，请访 [问Data Science Workspace概述](../../data-science-workspace/home.md)。

## 查询服务 {#query}

查询服务提供使用标准SQL在Adobe Experience Platform中查询数据的能力，以支持各种分析和数据管理用例。 它是一个无服务器工具，它允许您从数据湖连接数据集并将查询结果捕获为新数据集，以用于报告、数据科学工作区或引入实时客户用户档案。

您可以使用查询服务来构建数据分析生态系统，从而创建客户跨各种交互渠道的图景。 这些渠道可能包括销售点系统、Web、移动或CRM系统。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 对查询编辑器的改进 | 添加了保存功能，允许您保存查询并稍后处理它。 在Adobe Experience Platform上的查询服务用户界面中添加了“浏览”选项卡，其中显示了组织中用户保存的查询。 实施了“查询详细信息”面板，其中显示有关正在查看的查询的有用元数据。 |
| 新的归因函数 | Adobe在查询服务到查询中定义的函数，用于使用过期参数进行渠道归因。 |
| SQL语法增强 | 支持iLike语法。 |
| 使用定义的XDM模式生成数据集 | 在“创建表为选择(CTAS)”查询中添加了一个新子句，该子句允许您指定目标模式。 |

For more information, refer to the [Query Service documentation](../../query-service/home.md).