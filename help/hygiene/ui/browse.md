---
title: 浏览数据生命周期工作单
description: 了解如何在Adobe Experience Platform用户界面中查看和管理现有数据生命周期工作单。
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 27%

---

# 浏览数据生命周期工单 {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="工单 ID"
>abstract="将数据生命周期请求发送到系统时，将创建工单以执行请求的任务。换句话说，工单代表一个特定的数据生命周期流程，而该流程包括该工单的当前状态和其他相关的详细信息。每个工单在创建后会自动获得其唯一 ID。"
>text="See the data lifecycle UI guide to learn more."

将数据生命周期请求发送到系统时，将创建工单以执行请求的任务。工作单代表特定数据生命周期流程，如计划的数据集到期，其中包括其当前状态和其他相关详细信息。

本指南介绍如何在Adobe Experience Platform UI中查看和管理现有工作单。

## 列出和筛选现有工作单

首次在UI中访问&#x200B;**[!UICONTROL 数据生命周期]**&#x200B;工作区时，将显示现有工作单列表及其基本详细信息。

在Experience Platform UI中显示[!UICONTROL 数据生命周期]工作区的![图像](../images/ui/browse/work-order-list.png)

该列表一次只显示一个类别的工作单。 选择&#x200B;**[!UICONTROL 使用者]**&#x200B;以查看记录删除任务列表，选择&#x200B;**[!UICONTROL 数据集]**&#x200B;以查看计划的数据集过期列表。

![图像显示[!UICONTROL 数据集]选项卡](../images/ui/browse/dataset-tab.png)

选择漏斗图标（![漏斗图标的图像](/help/images/icons/filter.png)）以查看所显示工作单的过滤器列表。

![显示的工作单过滤器图像](../images/ui/browse/filters.png)

根据您查看的工作单类型，可以使用不同的筛选选项。

### 用于记录删除的筛选器

以下过滤器适用于记录删除请求：

| 筛选条件 | 描述 |
| --- | --- |
| [!UICONTROL 状态] | 根据工作单的当前状态进行筛选：<ul><li>**[!UICONTROL 已完成]**：作业已完成。</li><li>**[!UICONTROL 失败]**：作业遇到错误，无法完成。</li><li>**[!UICONTROL 正在处理]**：请求已启动，当前正在处理。</li></ul> |
| [!UICONTROL 创建日期] | 根据生成工单的时间进行筛选。 |
| [!UICONTROL 日期已更新] | 根据上次更新工单的时间进行筛选。 创建的内容将被计为更新。 |

### 数据集过期的筛选器

以下过滤器适用于数据集过期请求：

| 筛选条件 | 描述 |
| --- | --- |
| [!UICONTROL 状态] | 根据工作单的当前状态进行筛选：<ul><li>**[!UICONTROL 已完成]**：作业已完成。</li><li>**[!UICONTROL 挂起]**：作业已创建，但尚未执行。 [数据集到期请求](./dataset-expiration.md)在计划的删除日期之前假定此状态。 一旦到达删除日期，除非提前取消作业，否则状态将更新为[!UICONTROL 正在执行]。</li><li>**[!UICONTROL 正在执行]**：数据集过期请求已启动，当前正在处理。</li><li>**[!UICONTROL 已取消]**：作业已作为手动用户请求的一部分取消。</li></ul> |
| [!UICONTROL 创建日期] | 根据生成工单的时间进行筛选。 |
| [!UICONTROL 到期日期] | 根据相关数据集的计划删除日期筛选数据集到期请求。 |
| [!UICONTROL 日期已更新] | 根据上次更新工单的时间进行筛选。 创建和过期都将被计为更新。 |

{style="table-layout:auto"}

## 查看工单的详细信息 {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="按服务显示的状态"
>abstract="由多个 Experience Platform 服务独立处理数据生命周期请求。此部分概述对于每个相应服务的请求的当前处理状态。要了解详情，请参阅数据生命周期 UI 指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="身份标识数"
>abstract="其记录在此工单中被请求更新或删除的身份标识的数量。计数中包含的身份标识不一定存在于受影响的数据集中。要了解详情，请参阅数据生命周期 UI 指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="记录删除响应"
>abstract="当记录删除过程收到来自系统的响应时，这些消息将显示在&#x200B;**[!UICONTROL 结果]**&#x200B;部分下。如果在处理工单时出现问题，任何相关的错误消息都会显示在此部分中，帮助您解决问题。要了解详情，请参阅数据生命周期 UI 指南。"

选择已列出工作单的ID以查看其详细信息。

![显示正在选择的工作单ID的图像](../images/ui/browse/select-work-order.png)

根据所选工单的类型，会提供不同的信息和控制。 以下各节将介绍这些内容。

### 记录删除详细信息 {#record-delete}

记录删除请求的详细信息包括其当前状态和自发出请求以来经过的时间。 每个请求还包含一个&#x200B;**[!UICONTROL 按服务分类的状态]**&#x200B;部分，该部分提供有关删除中涉及的每个下游服务的单独状态详细信息。 在右边栏中，您可以使用控件来更新工作单的名称和描述。

![显示记录删除工作单的详细信息页面的图像](../images/ui/browse/record-delete-details.png)

### 数据集到期详细信息 {#dataset-expiration}

数据集到期的详细信息页面提供了有关其基本属性的信息，包括计划到期日期（在进行删除前的剩余天数）。 在右边栏中，您可以使用控件编辑或取消过期。

![显示数据集到期工作单详细信息页面的图像](../images/ui/browse/ttl-details.png)

## 后续步骤

本指南介绍了如何在Experience Platform UI中查看和管理现有数据生命周期工作单。 有关创建您自己的工作单的信息，请参阅以下文档：

* [管理数据集过期时间](./dataset-expiration.md)
* [管理记录删除](./record-delete.md)
