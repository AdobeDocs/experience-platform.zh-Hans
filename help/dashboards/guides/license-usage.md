---
keywords: Experience Platform；用户界面；UI；自定义；许可证使用仪表板;仪表板；许可证使用；授权；消耗
title: 许可证使用仪表板
description: Adobe Experience Platform提供了一个仪表板，您可以通过它视图有关组织许可证使用情况的重要信息。
topic-legacy: guide
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 2%

---

# （测试版）许可证使用仪表板{#license-usage-dashboard}

>[!IMPORTANT]
>
>此文档中概述的仪表板功能当前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Platform用户界面(UI)提供了一个仪表板，通过它可以视图有关组织许可证使用情况的重要信息，这些信息在每日快照中捕获。 本指南概述了如何在UI中访问和使用许可证使用仪表板，并提供了有关仪表板中显示的可视化的更多信息。

有关平台UI的一般概述，请访问[Experience PlatformUI指南](../../landing/ui-guide.md)。

## 许可证使用仪表板数据

许可证使用仪表板显示您组织的许可证相关数据的快照以供Experience Platform。 仪表板中的数据会与拍摄快照时在特定时间点显示的数据完全一样。 换句话说，快照不是数据的近似值或样本，仪表板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新将不会反映在仪表板中，直到拍摄下一个快照。

## 浏览许可证使用仪表板

要导航到平台UI中的许可证使用仪表板，请选择左边栏中的&#x200B;**[!UICONTROL License usage]**。 此时将打开&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡，其中显示仪表板。

![](../images/license-usage/dashboard-overview.png)

### 选择沙箱

要在仪表板中选择要视图的沙箱，请选择[!UICONTROL Production]或[!UICONTROL Development]。 选定的沙箱由沙箱名称旁边的单选按钮指示。

>[!NOTE]
>
>沙箱的消耗报告对于相同类型的所有沙箱是累积的。 换句话说，选择[!UICONTROL Production]或[!UICONTROL Development]分别为所有生产沙箱或开发沙箱提供消费报告。

![](../images/license-usage/select-sandbox.png)

### 选择日期范围

选择沙箱后，可以使用日期范围下拉列表选择要在仪表板中显示的时间段。 有三种可用选项：[!UICONTROL Last 30 days]、[!UICONTROL Last 90 days]和[!UICONTROL Last 12 months]。 默认情况下，将选择最近30天。

![](../images/license-usage/select-date-range.png)

## 构件

许可证使用仪表板由构件组成，构件显示只读量度，提供有关组织许可证使用情况的重要信息。 可见量度取决于贵组织的特定许可（有关详细信息，请参阅[可用量度](#available-metrics)部分）。

每个小部件都会显示一个线形图，比较您组织的实际数字与您组织的许可提供的总数，并提供总使用量的百分比。

![](../images/license-usage/widgets.png)

## 可用量度

许可证使用仪表板当前提供四个量度：

* [!UICONTROL Addressable Audience] (按用户档案数衡量)
* [!UICONTROL Average profile richness]
* [!UICONTROL Total consumed storage]
* [!UICONTROL Data scanned per segmentation ratio]

这些量度的定义因单位购买的许可而异。 有关每个量度的详细定义，请参阅相应的产品说明文档：

| 许可 | 产品说明 |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD标准</li><li>Adobe Experience Platform:OD重</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform、App Services和Intelligent Services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT客户数据平台：OD</li><li>RT客户数据平台：OD PRFL至10M</li><li>RT客户数据平台：OD PRFL至50M</li></ul> | [Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD激活</li><li>AEP:OD激活PRF至10M</li><li>AEP:OD激活最多50米</li></ul> | [Adobe Experience Platform 激活](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

## 后续步骤

读取此文档后，您可以找到许可证使用仪表板并选择要视图的沙箱。 您还可以根据单位购买的许可找到有关单位可用指标的更多信息。

要进一步了解Experience Platform UI中的其他功能，请参阅[平台UI指南](../../landing/ui-guide.md)。
