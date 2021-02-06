---
keywords: Experience Platform；洞察；归因ai；热门主题；归因ai洞察
solution: Intelligent Services, Experience Platform
title: 在Attribution AI中发掘洞察
topic: Attribution AI insights
description: 此文档可作为与Adobe智能服务用户界面中的服务实例洞察交互的指南。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---


# 发掘Attribution AI洞察

Attribution AI服务实例提供的洞察有助于制定和衡量与营销绩效和投资回报相关的营销决策。 选择服务实例可提供可视化和过滤器，帮助您了解客户旅程每个阶段每次客户互动的影响。

此文档可作为与Adobe智能服务用户界面中的服务实例洞察交互的指南。

## 入门指南

为了利用Attribution AI洞察，您需要有一个运行状态成功的服务实例。 要创建新服务实例，请访问[Attribution AI用户界面指南](./user-guide.md)。 如果您最近创建了一个服务实例，但它仍在培训和评分，请允许24小时，它才能完成运行。

## 服务实例洞察概述

在[!DNL Adobe Experience Platform] UI中，在左侧导航中选择&#x200B;**[!UICONTROL 服务]**。 出现&#x200B;**[!UICONTROL 服务]**&#x200B;浏览器并显示可用的Adobe智能服务。 在Attribution AI容器中，选择&#x200B;**[!UICONTROL 打开]**。

![访问实例](./images/insights/open_Attribution_ai.png)

将显示Attribution AI服务页面。 此页列表Attribution AI的服务实例并显示其相关信息，包括实例名称、转换事件、实例的运行频率以及上次更新的状态。 选择要开始的服务实例名称。

>[!NOTE]
>
>只能选择已成功完成评分运行的服务实例。

![创建实例](./images/insights/select-service-instance.png)

接下来，将显示该服务实例的洞察页面，其中为您提供可视化信息和大量过滤器以与数据交互。 本指南中对可视化和过滤器进行了更详细的说明。

![设置页面](./images/insights/landing-page.png)

### 服务实例详细信息

要视图服务实例的其他详细信息，请选择右上角的&#x200B;**[!UICONTROL 显示更多]**。

![显示更多](./images/insights/show-more.png)

将显示详细列表。 有关所列任何属性的详细信息，请访问[Attribution AI用户指南](./user-guide.md)。

![显示详细信息](./images/insights/advanced-details.png)

### 编辑实例

要编辑实例，请在右上方的导航中选择&#x200B;**[!UICONTROL 编辑]**。
![单击“编辑”按钮](./images/insights/edit-button.png)

此时会显示编辑对话框，允许您编辑实例的名称、说明和评分频率。 如果实例状态被禁用，则无法编辑评分频率。 要确认更改并关闭对话框，请选择右下角的&#x200B;**[!UICONTROL 保存]**。

![编辑跨窗格](./images/insights/edit-popover.png)

### 更多操作{#more-actions}

**[!UICONTROL 更多操作]**&#x200B;按钮位于右上导航中的&#x200B;**[!UICONTROL 编辑]**&#x200B;旁边。 选择&#x200B;**[!UICONTROL 更多操作]**&#x200B;将打开一个下拉框，通过该下拉框可以选择下列操作之一：

- **[!UICONTROL 克隆]**:克隆实例。
- **[!UICONTROL 删除]**:删除实例。
- **[!UICONTROL 下载摘要数据]**:下载包含摘要数据的CSV文件。
- **[!UICONTROL 访问分数]**:选择 **[!UICONTROL 访问]** 分数会将您重定向到 [Attribution AI教程的访问分数](./download-scores.md)。
- **[!UICONTROL 视图运行历史]**:此时会显示一个列表，其中包含与服务实例关联的所有评分运行。

![更多操作](./images/insights/more-actions.png)

## 筛选数据

Attribution AI洞察使您能够过滤数据并根据选定过滤器自动更新UI可视内容。

### 转换事件

在Attribution AI中创建新实例时，其中一个必填字段是“转换事件”。 转化事件是确定营销活动（如电子商务订单、店内购买和网站访问）影响的业务目标。

在实例中，**[!UICONTROL 转换事件]**&#x200B;下拉列表允许您选择为实例定义的任何事件，以过滤数据。 选择特定事件会更改UI可视化，以仅填充属于这些事件的转换。

![转换事件](./images/insights/conversion-event.png)

### 归因模型

选择&#x200B;**[!UICONTROL 归因模型]**&#x200B;将打开一个下拉菜单，其中提供所有不同的归因模型。 您可以选择多个模型来比较结果。 有关不同属性模型及其工作方式的详细信息，请访问[Attribution AI](./overview.md)概述，其中包含一个表，其中包含有关每个模型的信息。

![归因模型](./images/insights/attribution-model.png)

### 地区

>[!NOTE]
>
>仅当您在创建服务实例时执行了Attribution AI用户界面指南中的可选步骤[基于区域的建模](./user-guide.md#region-based-modeling-optional)时，此过滤器才存在。

此过滤器允许您选择在实例创建过程中设置的任何区域。

### 添加过滤器

选择&#x200B;**过滤器**&#x200B;图标可以添加其他过滤器，打开&#x200B;**[!UICONTROL 添加过滤器]**&#x200B;弹出窗口。 **[!UICONTROL 添加过滤器]**&#x200B;弹出窗口允许您按渠道、地理位置、媒体类型和产品进行筛选。 只有适用于服务实例的过滤器才会由弹出窗口填充。 例如，如果您没有提供地理数据或媒体类型，则这些过滤器属性将不对您的实例可用。

![额外过滤器](./images/insights/additional-filters.png)

![筛选条目](./images/insights/filter-popover.png)

- **[!UICONTROL 渠道]** ：选择渠道属性后，您可以过滤任何可用的营销渠道。您可以选择多个渠道进行比较。
- **[!UICONTROL 地理]:** 选择地理属性后，您可以根据基于区域的模型筛选国家代码。根据您的数据，此筛选器可能存在，也可能不存在。 国家代码长度为两个字符。 请参阅完整的国家／地区代码列表[此处](https://datahub.io/core/country-list)。
- **[!UICONTROL 媒体类型]:** 选择媒体类型属性后，您可以过滤任何定义的媒体类型。
- **[!UICONTROL 产品]：选** 择产品属性后，您可以过滤在创建实例时最初引入的任何产品。

### Date Range

选择日历图标以打开日期范围窗格。 开始和结束转换事件日期决定在UI中填充的数据量。 您可以选择缩小或扩大日期范围，以集中或扩展已填充的数据量。

![日期范围](./images/insights/display-date-range.png)

## 数据概述

**[!UICONTROL 概述]**&#x200B;卡按归因模型显示您的转化总数。 根据您使用本文档中前面列出的过滤器进行搜索的具体程度，更改总数。 选择更多模型会向“概述”添加其他圆，每个圆都有与图例对应的颜色。

![概述](./images/insights/Overview.png)

## 每周趋势

**[!UICONTROL 每周趋势]**&#x200B;卡按您在筛选过程中设置的日期范围细分您的总转化率。

选择&#x200B;**每周趋势**&#x200B;卡右上方的省略号会显示一个下拉菜单，允许您选择每日、每周或每月趋势。

将指针悬停在特定归因模型的数据线上，可创建一个跨距，其中显示该日期的转换总数。

![趋势](./images/insights/weekly-trends.png)

## 按渠道细分

**[!UICONTROL 按渠道细分]**&#x200B;卡用于确定与每个渠道相关的转换总数。 此卡可用于帮助决定每个渠道的有效性和投资回报。

选择&#x200B;**[!UICONTROL 按渠道]**&#x200B;细分卡右上方的省略号将打开一个下拉菜单，允许您根据接触点填充数据。

![细分渠道](./images/insights/channel-breakdown.png)

## 顶级活动

**[!UICONTROL 顶级活动]**&#x200B;卡显示活动的概述以及活动在每个渠道中的执行情况。 此信息卡可帮助您的团队了解特定活动对特定渠道的有效性，并提供您应进一步投资的活动等洞察。

![顶级活动](./images/insights/top-campaigns.png)

## 按触点位置细分

选择&#x200B;**[!UICONTROL 路径分析]**&#x200B;选项卡将加载按触点位置&#x200B;]**和**[!UICONTROL &#x200B;顶部转换路径&#x200B;]**图形进行细分。**[!UICONTROL 

**[!UICONTROL 按接触点位置划分]**&#x200B;图表是按所有转换路径中比较的接触点位置划分的属性转换。 此图表可帮助您了解哪些接触点在转化路径的不同阶段更为有效。 舞台是入门、玩家和更近的。

- **起始：** 指示触点是转换路径中的第一次触点。
- **播放器：** 指示触点不是导致转换的第一个或最后一个触点。
- **更近：** 指示触点是转化前的最后一次接触。

>!![NOTE]
所有接触点和职位的归因模型贡献百分比之和应等于100。

![用户路径细分触点](./images/insights/user-paths.png)

## 顶级转换路径

**[!UICONTROL 顶转换路径]**&#x200B;图显示了所选区域中顶转换路径的影响和算法得分。 此图表允许您直观地显示哪些接触点有助于转化以及每个接触点的归因得分。 您可以使用此信息视图特定区域中最频繁的路径，并查看不同接触点集之间是否出现任何模式。

![最常见的用户路径](./images/insights/Touchpoint-paths.png)

## 触点有效性

选择&#x200B;**[!UICONTROL 触点有效性]**&#x200B;选项卡可加载&#x200B;**[!UICONTROL 触点有效性]**&#x200B;卡。 此卡使用Attribution AI的数据分发来显示每个触点的信息。 此表的数据仅针对卡右上方的&#x200B;**[!UICONTROL 截止]**&#x200B;日期所指示的特定时间段生成。

![触点有效性选择](./images/insights/Touchpoint-effectiveness.png)

您可以使用&#x200B;**[!UICONTROL 触点有效性]**&#x200B;卡信息来了解触点对转换的贡献。 您还可以通过以下绩效指标了解每个接触点的有效性：

**接触的路径**:此度量显示达到／未达到触点转换的路径百分比。如果实现路径转换的路径（百分比）与未实现转换的路径的比率较高，则您会看到较高的归因转换。

![接触路径量度](./images/insights/Touchpoint-metrics.png)

**效率衡量**:此度量以1到5的比例显示星体。比例表示触点在进行转换时的相对重要性。

>[!NOTE]
更高的接触点容量不能保证更高的效率衡量。

**总量**:聚合用户触碰触点的次数。这包括在实现转换的路径上显示的接触点，以及不导致转换的路径。

## 后续步骤

过滤完数据并能够显示相应的信息后，您便可以选择访问分数。 有关如何访问得分的详细指南，请访问Attribution AI](./download-scores.md)教程中的[access得分。 此外，还可以按[更多操作](#more-actions)中的指示下载摘要数据。 选择“下载摘要数据”将下载按日期聚集的摘要数据。

## Journey Orchestration

以下视频旨在帮助学习如何使用Attribution AI洞察页面了解营销渠道和活动的ROI。

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)