---
title: 浏览数据卫生工作单
description: 了解如何在Adobe Experience Platform用户界面中查看和管理现有数据卫生工作单。
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: e57b5ec6c6234d4d1fe22f8d03c70d6bd9c02f0f
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 2%

---

# 浏览数据卫生工作单 {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="工作单ID"
>abstract="当向系统发送数据卫生请求时，创建工作命令以执行所请求的任务。 换言之，工作单代表特定的数据卫生过程，包括其当前状态和其他相关详细信息。 每个工作单在创建时会自动分配其自己的唯一ID。"
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Adobe Experience Platform中的数据卫生功能目前仅适用于已购买Healthcare Shield的组织。

当向系统发送数据卫生请求时，创建工作命令以执行所请求的任务。 工作单表示特定的数据卫生过程，如数据集的计划生存时间(TTL)，其中包括其当前状态和其他相关详细信息。

本指南介绍如何在Adobe Experience Platform UI中查看和管理现有工作单。

## 列出和筛选现有工作单

首次访问 **[!UICONTROL 数据卫生]** 工作区中，会显示现有工作单的列表及其基本详细信息。

![显示 [!UICONTROL 数据卫生] 平台UI中的工作区](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of time-to-live (TTL) schedules for datasets.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

选择漏斗图标(![漏斗图标的图像](../images/ui/browse/funnel-icon.png))以查看所显示工作单的过滤器列表。

![显示的工作单过滤器图像](../images/ui/browse/filters.png)

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 状态] | 根据工作单的当前状态进行筛选：<ul><li>**[!UICONTROL 已完成]**:作业已完成。</li><li>**[!UICONTROL 待定]**:作业已创建，但尚未执行。 A [数据集生存时间(TTL)请求](./ttl.md) 在计划的删除日期之前假定此状态。 删除日期到达后，状态将更新为 [!UICONTROL 正在执行] 除非事前取消工作。</li><li>**[!UICONTROL 正在执行]**:作业已启动且当前正在处理。</li><li>**[!UICONTROL 已取消]**:作为手动用户请求的一部分，作业已取消。</li></ul> |
| [!UICONTROL 创建日期] | 根据下达工作单的时间进行筛选。 |
| [!UICONTROL 过期日期] | 根据相关数据集的计划删除日期过滤TTL请求。 |
| [!UICONTROL 更新日期] | 根据上次更新工作单的时间筛选TTL请求。 TTL创建和过期将计为更新。 |

{style=&quot;table-layout:auto&quot;}

## 查看工作单的详细信息

选择列出的工作单的ID以查看其详细信息。

![显示正在选择的工作单ID的图像](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset TTL details -->

数据集TTL的详细信息页面提供了有关其基本属性的信息，包括删除前剩余天数的计划过期日期。 在右边栏中，您可以使用控件来编辑或取消TTL。

![显示数据集TTL工作顺序详细信息页面的图像](../images/ui/browse/ttl-details.png)

## 后续步骤

本指南介绍了如何在Platform UI中查看和管理现有数据卫生工作单。 有关创建您自己的工作单的信息，请参阅 [计划数据集TTL](./ttl.md).
