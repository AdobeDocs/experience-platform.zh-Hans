---
keywords: Experience Platform；洞察；归因ai；热门主题；归因ai洞察
solution: Intelligent Services, Experience Platform
title: 了解Attribution AI
topic-legacy: Attribution AI insights
description: 此文档可作为与Adobe Intelligent Services用户界面中的服务实例洞察交互的指南。
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1584'
ht-degree: 0%

---

# 了解Attribution AI

Attribution AI服务实例提供的洞察可用于帮助制定和衡量与营销绩效和投资回报相关的营销决策。 选择服务实例可提供可视化和过滤器，帮助您了解客户旅程每个阶段每次客户互动的影响。

此文档可作为与Adobe Intelligent Services用户界面中的服务实例洞察交互的指南。

## 入门指南

为了利用洞察来Attribution AI，您需要有一个运行状态成功的服务实例。 要创建新服务实例，请访问[Attribution AI用户界面指南](./user-guide.md)。 如果您最近创建了一个服务实例，但它仍在培训和得分，请允许24小时以完成运行。

## 服务实例分析概述

在[!DNL Adobe Experience Platform] UI中，在左侧导航中选择&#x200B;**[!UICONTROL Services]**。 出现&#x200B;**[!UICONTROL Services]**&#x200B;浏览器并显示可用的Adobe智能服务。 在Attribution AI容器中，选择&#x200B;**[!UICONTROL Open]**。

![访问您的实例](./images/insights/open_Attribution_ai.png)

将显示Attribution AI服务页面。 本页列表Attribution AI的服务实例并显示相关信息，包括实例名称、转换事件、实例的运行频率以及上次更新的状态。 选择要开始的服务实例名称。

>[!NOTE]
>
>只能选择已成功完成评分运行的服务实例。

![创建实例](./images/insights/select-service-instance.png)

接下来，将显示该服务实例的洞察页面，其中为您提供可视化信息和许多与数据交互的过滤器。 本指南中将更详细地说明可视化和过滤器。

![设置页面](./images/insights/landing-page.png)

### 服务实例详细信息

要视图服务实例的其他详细信息，请选择右上角的&#x200B;**[!UICONTROL Show more]**。

![显示更多](./images/insights/show-more.png)

将显示详细列表。 有关所列任何属性的详细信息，请访问[Attribution AI用户指南](./user-guide.md)。

![显示详细信息](./images/insights/advanced-details.png)

### 编辑实例

要编辑实例，请在右上方的导航中选择&#x200B;**[!UICONTROL Edit]**。
![单击“编辑”按钮](./images/insights/edit-button.png)

此时会显示编辑对话框，允许您编辑实例的名称、说明和评分频率。 如果实例状态被禁用，则无法编辑评分频率。 要确认更改并关闭对话框，请选择右下角的&#x200B;**[!UICONTROL Save]**。

![编辑跨页](./images/insights/edit-popover.png)

### 更多操作{#more-actions}

**[!UICONTROL More actions]**&#x200B;按钮位于&#x200B;**[!UICONTROL Edit]**&#x200B;旁边的右上导航中。 选择&#x200B;**[!UICONTROL More actions]**&#x200B;会打开一个下拉列表，允许您选择以下操作之一：

- **[!UICONTROL Clone]**:克隆实例。
- **[!UICONTROL Delete]**:删除实例。
- **[!UICONTROL Download summary data]**:下载包含摘要数据的CSV文件。
- **[!UICONTROL Access scores]**:选择 **[!UICONTROL Access scores]** 会将您重定向到 [Attribution AI教程的访问得分](./download-scores.md)。
- **[!UICONTROL View run history]**:此时会显示一个列表，其中包含与服务实例关联的所有评分运行。

![更多操作](./images/insights/more-actions.png)

## 筛选数据

Attribution AI洞察使您能够过滤数据并根据选定的过滤器自动更新UI可视内容。

### 转换事件

在Attribution AI中创建新实例时，其中一个必填字段是“转换事件”。 转化事件是确定营销活动（如电子商务订单、店内购买和网站访问）影响的业务目标。

在实例中，**[!UICONTROL Conversion events]**&#x200B;下拉列表允许您选择为实例定义的任何事件以筛选数据。 选择特定事件会更改UI可视化，以仅填充属于这些事件的转换。

![转换事件](./images/insights/conversion-event.png)

### 归因模型

选择&#x200B;**[!UICONTROL Attribution Model]**&#x200B;将打开一个下拉列表，其中所有不同的归因模型都可用。 您可以选择多个模型来比较结果。 有关不同归因模型及其工作方式的详细信息，请访问[Attribution AI](./overview.md)概述，其中包含一个包含每个模型相关信息的表。

![归因模型](./images/insights/attribution-model.png)

### 地区

>[!NOTE]
>
>仅当您在创建服务实例时执行了Attribution AI用户界面指南中的可选步骤[基于区域的建模](./user-guide.md#region-based-modeling-optional)时，才显示此筛选器。

此过滤器允许您选择在实例创建过程中设置的任何区域。

### 添加过滤器

您可以通过选择&#x200B;**filter**&#x200B;图标打开&#x200B;**[!UICONTROL Add filters]**&#x200B;快显窗口来添加其他过滤器。 **[!UICONTROL Add filters]**&#x200B;弹出窗口允许您按渠道、地理位置、媒体类型和产品进行筛选。 只有服务实例的适用过滤器会由跨距填充。 例如，如果您未提供地理数据或媒体类型，则这些过滤器属性将不对您的实例可用。

![额外过滤器](./images/insights/additional-filters.png)

![筛选](./images/insights/filter-popover.png)

- **[!UICONTROL Channel]：选** 择“渠道”属性后，您可以过滤任何可用的营销渠道。您可以选择多个渠道进行比较。
- **[!UICONTROL Geography]：选** 择地理属性后，您可以根据基于区域的模型筛选国家代码。根据您的数据，此过滤器可能存在，也可能不存在。 国家代码长度为两个字符。 请参阅完整的国家/地区代码列表[此处](https://datahub.io/core/country-list)。
- **[!UICONTROL Media type]：选** 择媒体类型属性后，可以过滤任何定义的媒体类型。
- **[!UICONTROL Product]：选** 择产品属性后，您可以从创建实例时最初摄取的任何产品进行筛选。

### Date Range

选择日历图标以打开日期范围快显。 开始和结束转换事件日期决定在UI中填充的数据量。 您可以选择缩小或扩大日期范围，以集中或扩展已填充的数据量。

![日期范围](./images/insights/display-date-range.png)

## 数据概述

**[!UICONTROL Overview]**&#x200B;信息卡按归因模型显示转化总数。 根据您使用本文档中前面列出的过滤器进行搜索的具体程度，更改的总数。 选择更多模型会向“概述”添加其他圆，每个圆都有与图例对应的颜色。

![概述](./images/insights/Overview.png)

## 每周趋势

**[!UICONTROL Weekly trends]**&#x200B;卡按您在筛选过程中设置的日期范围划分您的总转化率。

选择&#x200B;**每周趋势**&#x200B;卡右上角的省略号会显示一个下拉框，允许您选择每日、每周或每月趋势。

将指针悬停在特定归因模型的数据行上，可创建一个跨距，显示该日期的转换总数。

![趋势](./images/insights/weekly-trends.png)

## 按渠道划分

**[!UICONTROL Breakdown by channel]**&#x200B;卡用于确定与每个渠道相关的转换总数。 此卡可帮助决定每个渠道的有效性和投资回报。

选择&#x200B;**[!UICONTROL Breakdown by channel]**&#x200B;卡右上角的省略号会打开一个下拉列表，允许您根据接触点填充数据。

![划分渠道](./images/insights/channel-breakdown.png)

## 热门活动

**[!UICONTROL Top campaigns]**&#x200B;卡显示活动的概述以及活动在每个渠道中的执行情况。 此信息卡可帮助您的团队了解特定活动对于特定渠道的有效性，并提供您应进一步投资的活动等洞察。

![顶级活动](./images/insights/top-campaigns.png)

## 按接触点位置划分

选择&#x200B;**[!UICONTROL Path Analysis]**&#x200B;选项卡将加载&#x200B;**[!UICONTROL Breakdown by touchpoint position]**&#x200B;和&#x200B;**[!UICONTROL Top conversion paths]**&#x200B;图形。

**[!UICONTROL Breakdown by touchpoint position]**&#x200B;图表按所有转化路径中比较的接触点位置划分属性转化。 此图表可帮助您了解哪些接触点在转化路径的不同阶段更为有效。 舞台是开始、玩家和接近的。

- **起始：** 指示触点是转换路径中的首次触摸。
- **播放器：** 指示接触点不是通向转换的第一次或最后一次接触。
- **近距：** 指示触点是转换前的最后一次接触。

>!![NOTE]
所有接触点和位置中的归因模型贡献百分比之和应等于100。

![用户路径划分接触点](./images/insights/user-paths.png)

## 顶级转换路径

**[!UICONTROL Top conversion paths]**&#x200B;图表显示所选区域中顶部转换路径上受影响和算法得分。 此图表允许您直观地显示哪些接触点对转化的贡献以及每个接触点的归因得分。 您可以使用此信息来视图特定区域中最频繁的路径，并查看不同接触点集之间是否出现任何模式。

![最常见的用户路径](./images/insights/Touchpoint-paths.png)

## 接触点有效性

选择&#x200B;**[!UICONTROL Touchpoint Effectiveness]**&#x200B;选项卡将加载&#x200B;**[!UICONTROL Touchpoint effectiveness]**&#x200B;卡。 此卡使用Attribution AI的数据分发来显示每个接触点的信息。 此表的数据仅针对卡右上角的&#x200B;**[!UICONTROL As of]**&#x200B;日期所指示的特定时间段生成。

![触点有效性](./images/insights/Touchpoint-effectiveness.png)

您可以使用&#x200B;**[!UICONTROL Touchpoint effectiveness]**&#x200B;卡信息来了解触点对转换的贡献。 您还可以通过以下绩效指标了解每个接触点的效果：

**接触的路径**:此量度显示达到/未达到接触点转换的路径百分比。如果实现路径转换的路径（百分比）与未实现转换的路径的比率较高，您会看到较高的归因转换。

![接触路径量度](./images/insights/Touchpoint-metrics.png)

**效率衡量**:此量度以1到5的比例显示星形。比例表示触点对进行转换的相对重要性。

>[!NOTE]
更高的接触点容量不能保证更高的效率衡量。

**总量**:聚合用户触碰接触点的次数。这包括在实现转换的路径上显示的接触点以及不导致转换的路径。

## 后续步骤

过滤完数据并能够显示相应信息后，您可以选择访问分数。 有关如何访问得分的详细指南，请访问Attribution AI教程](./download-scores.md)中的[访问得分。 此外，您还可以按[更多操作](#more-actions)中的指示下载摘要数据。 选择“下载摘要数据”将下载按日期聚集的摘要数据。

## 其他资源

以下视频旨在帮助学习如何使用Attribution AI洞察页面了解营销渠道和活动的ROI。

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
