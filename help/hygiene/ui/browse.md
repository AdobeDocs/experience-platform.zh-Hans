---
title: 浏览数据卫生工作单
description: 了解如何在Adobe Experience Platform用户界面中查看和管理现有数据卫生工作单。
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 25%

---

# 浏览数据卫生工作单 {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="工单 ID"
>abstract="在向系统发送数据卫生请求时，将创建工单以执行请求的任务。换句话说，工单代表一个特定的数据卫生流程，包括其当前状态和其他相关详细信息。每个工单在创建后会自动获得其唯一 ID。"
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Adobe Experience Platform中的数据卫生功能目前仅适用于已购买的组织 **Adobe医疗保健盾** 或 **Adobe隐私和安全防护**.

在向系统发送数据卫生请求时，将创建工单以执行请求的任务。工作单表示特定的数据卫生过程，如计划的数据集过期，包括其当前状态和其他相关详细信息。

本指南介绍如何在Adobe Experience Platform UI中查看和管理现有工作单。

## 列出和筛选现有工作单

首次访问 **[!UICONTROL 数据卫生]** 工作区中，会显示现有工作单的列表及其基本详细信息。

![显示 [!UICONTROL 数据卫生] 平台UI中的工作区](../images/ui/browse/work-order-list.png)

该列表一次只显示一个类别的工作单。 选择 **[!UICONTROL 消费者]** 查看记录删除任务列表，以及 **[!UICONTROL 数据集]** 查看计划数据集过期的列表。

![显示 [!UICONTROL 数据集] 选项卡](../images/ui/browse/dataset-tab.png)

选择漏斗图标(![漏斗图标的图像](../images/ui/browse/funnel-icon.png))以查看所显示工作单的过滤器列表。

![显示的工作单过滤器图像](../images/ui/browse/filters.png)

根据您查看的工作单类型，可使用不同的筛选选项。

### 记录删除的过滤器

以下过滤器适用于记录删除请求：

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 状态] | 根据工作单的当前状态进行筛选：<ul><li>**[!UICONTROL 已完成]**:作业已完成。</li><li>**[!UICONTROL 失败]**:作业遇到错误，无法完成。</li><li>**[!UICONTROL 处理]**:请求已启动且当前正在处理。</li></ul> |
| [!UICONTROL 创建日期] | 根据下达工作单的时间进行筛选。 |
| [!UICONTROL 更新日期] | 根据上次更新工作单的时间进行筛选。 创建将计为更新。 |

### 数据集过期的过滤器

以下过滤器适用于数据集过期请求：

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 状态] | 根据工作单的当前状态进行筛选：<ul><li>**[!UICONTROL 已完成]**:作业已完成。</li><li>**[!UICONTROL 待定]**:作业已创建，但尚未执行。 A [数据集过期请求](./dataset-expiration.md) 在计划的删除日期之前假定此状态。 删除日期到达后，状态将更新为 [!UICONTROL 正在执行] 除非事前取消工作。</li><li>**[!UICONTROL 正在执行]**:数据集过期请求已启动且当前正在处理。</li><li>**[!UICONTROL 已取消]**:作为手动用户请求的一部分，作业已取消。</li></ul> |
| [!UICONTROL 创建日期] | 根据下达工作单的时间进行筛选。 |
| [!UICONTROL 过期日期] | 根据相关数据集的计划删除日期过滤数据集过期请求。 |
| [!UICONTROL 更新日期] | 根据上次更新工作单的时间进行筛选。 创建和过期将计为更新。 |

{style="table-layout:auto"}

## 查看工作单的详细信息 {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="按服务显示的状态"
>abstract="数据卫生请求由多个 Experience Platform 服务独立处理。此部分概述了每个相应服务的请求的当前处理状态。要了解更多信息，请参阅《数据卫生 UI 指南》。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="标识数"
>abstract="其记录在此工单中被请求更新或删除的标识的数量。计数中包含的标识不一定存在于受影响的数据集中。要了解更多信息，请参阅《数据卫生 UI 指南》。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="记录删除响应"
>abstract="当记录删除过程收到来自系统的响应时，这些消息将显示在&#x200B;**[!UICONTROL 结果]**&#x200B;部分下。如果在处理工单时出现问题，任何相关的错误消息都会显示在此部分中，帮助您解决问题。要了解更多信息，请参阅《数据卫生 UI 指南》。"

选择列出的工作单的ID以查看其详细信息。

![显示正在选择的工作单ID的图像](../images/ui/browse/select-work-order.png)

根据所选工作单的类型，将提供不同的信息和控件。 以下各节介绍了这些内容。

### 记录删除详细信息 {#record-delete}

记录删除请求的详细信息包括其当前状态以及自请求发出以来经过的时间。 每个请求还包括 **[!UICONTROL 按服务列出的状态]** 部分，提供有关删除中涉及的每个下游服务的各个状态详细信息。 在右边栏中，您可以使用控件来更新工作单的名称和说明。

![显示记录删除工作单详细信息页面的图像](../images/ui/browse/record-delete-details.png)

### 数据集过期详细信息 {#dataset-expiration}

数据集过期的详细信息页面提供了有关其基本属性的信息，包括删除之前剩余日期的计划过期日期。 在右边栏中，您可以使用控件来编辑或取消过期。

![显示数据集过期工作单详细信息页面的图像](../images/ui/browse/ttl-details.png)

## 后续步骤

本指南介绍了如何在Platform UI中查看和管理现有数据卫生工作单。 有关创建您自己的工作单的信息，请参阅以下文档：

* [管理数据集过期日期](./dataset-expiration.md)
<!-- * [Manage record deletes](./record-delete.md) -->
