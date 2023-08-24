---
keywords: Experience Platform；用户界面；UI；自定义；许可证使用仪表板；仪表板；许可证使用；权利；使用
title: 许可证使用情况仪表板指南
description: Adobe Experience Platform提供了一个功能板，通过该功能板可查看有关贵组织许可证使用情况的重要信息。
type: Documentation
hide: true
hidefromtoc: true
source-git-commit: c1ad20def39ef58253e8486ca4dcfcce2501510b
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 1%

---

# 许可证使用情况功能板（限量发布） {#license-usage-dashboard-limited-release}

>[!IMPORTANT]
>
>更新的 [!UICONTROL 许可证使用情况] 功能板当前在以下位置可用： **仅限限量发布** 并非所有客户均适用。

您可以通过Adobe Experience Platform查看有关贵组织许可证使用情况的重要信息 [!UICONTROL 许可证使用情况] 仪表板。 此处显示的信息是在Platform实例的每日快照期间捕获的。

许可证使用情况报表可提供比许可证使用情况量度更高级别的粒度。 仪表板提供每个购买产品的使用情况量度、所有生产或开发沙盒中量度的综合使用情况，以及特定沙盒的使用情况量度。 可以使用使用情况量度跟踪以下Experience Platform应用程序：实时客户数据配置文件、Adobe Journey Optimizer和Customer Journey Analytics。

本指南概述如何在UI中访问和使用许可证使用情况仪表板，并提供有关仪表板中显示的可视化的更多信息。

有关Platform UI的概述，请参阅 [Experience Platform用户界面指南](../../landing/ui-guide.md).

## [!UICONTROL 许可证使用情况] 仪表板数据

此 [!UICONTROL 许可证使用情况] 功能板显示您已购买的所有Experience Platform产品的列表。 从该列表中，您可以找到您组织的许可证相关数据的快照，以便Experience Platform在任何关联的沙盒中。

此仪表板中的数据与拍摄快照的特定时间点完全相同。 换句话说，快照不是数据的近似值或样本，并且仪表板没有实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新都不会反映在功能板中，直到拍摄下一个快照为止。

## 浏览许可证使用情况仪表板 {#explore}

要导航到Platform UI中的许可证使用情况仪表板，请选择 **[!UICONTROL 许可证使用情况]** 在左边栏中。 此 [!UICONTROL 概述] 选项卡打开，显示可用产品的列表。

>[!NOTE]
>
>默认情况下，许可证使用情况仪表板未启用。 必须向用户授予»[!UICONTROL 查看许可证使用情况仪表板]”权限才能查看仪表板。 有关授予查看许可证使用仪表板的访问权限的步骤，请参阅 [仪表板权限指南](../permissions.md).

![许可证使用情况仪表板概述选项卡，左侧导航侧边栏中突出显示了许可证使用情况。](../images/license-usage/dashboard-overview.png)

## [!UICONTROL Overview 选项卡] {#overview-tab}

此仪表板以表格式显示您的所有许可Adobe Experience Platform产品，包括加载项。 该表提供了有关所有可用配置文件中许可证使用情况的关键信息。

| 列名称 | 描述 |
|---|---|
| **[!UICONTROL 产品]** | 由您的组织许可的Adobe解决方案。 |
| **[!UICONTROL 主要指标]** | 用于在内跟踪该产品的主要量度。 |
| **[!UICONTROL 许可证金额]** | 产品许可协议中约定的主要量度最大量的约定值。 |
| **[!UICONTROL 用法]** | 您使用的主要量度的数量。 此值提供该量度在所有沙盒（生产沙盒或开发沙盒）中的总使用情况。 |
| **[!UICONTROL 用法 %]** | 根据您的许可证数量使用的主要量度的百分比。 |

>[!NOTE]
>
>增加至 [!UICONTROL 许可证金额] 作为加载项的结果，将添加在 [!UICONTROL 许可证金额] 基础产品，例如实时客户数据配置文件、Adobe Journey Optimizer和Customer Journey Analytics。 通过基础产品跟踪该许可数量（加载项后）的使用情况。 例如，如果您购买一包5个沙盒，则数量5将添加到基础产品的数量。在这种情况下，加载项会显示 [!UICONTROL 许可证金额] 其中，且该加载项的使用是“空白的”，因为使用情况是通过基本产品进行跟踪的。

该表指示了每个产品的主要量度，因为每个产品都可以跟踪大量量度。 要查看有关您的产品许可证使用情况的更多量度和详细分析，请从列表中选择产品名称。 此 [!UICONTROL 摘要] 此时会出现该产品的视图。

## [!UICONTROL 摘要] 选项卡 {#summary-tab}

所有可用量度均显示在 [!UICONTROL 摘要] 选项卡。 可用的量度取决于许可的产品。 此视图提供 **跨所有生产或开发沙盒的所有量度的综合视图**. 为生产沙盒和开发沙盒提供相同级别的分析。

![显示产品所有可用量度的平台产品的摘要视图。]()

在摘要选项卡上，该表包括 [!UICONTROL 量度] 列。 这些易于用户识别的描述指示用于该类型沙盒的所有量度。

### 选择沙盒 {#select-sandbox}

要更改生产和开发沙盒类型之间的视图，请选择 [!UICONTROL 生产沙盒] 或 [!UICONTROL 开发沙盒]. 沙盒名称旁边的单选按钮表示所选的沙盒类型。

沙盒的使用情况报告对于同一类型的所有沙盒是累计的。 换句话说，选择 [!UICONTROL 生产] 或 [!UICONTROL 开发] 分别提供所有生产沙盒或开发沙盒的使用情况报表。

![突出显示了生产沙盒和开发沙盒的Platform产品的摘要视图。](../images/license-usage/summary-tab.png)

>[!WARNING]
>
>必须在沙盒级别指定查看许可证使用情况仪表板的权限。 您必须向每个沙盒添加权限，才能在功能板中查看它们。 此限制将在未来版本中解决。 同时，提供以下解决方法：
>
>1. 在Adobe Admin Console中创建产品配置文件。
>2. 在沙盒类别中的权限下，添加您希望在许可证使用情况仪表板中查看的所有沙盒。
>3. 在“用户仪表板权限”类别下，添加“查看许可证使用情况仪表板”权限。

## 此 [!UICONTROL 详细信息] 选项卡 {#details-tab}

查看 **来自特定沙盒的特定使用量度**，导航到 [!UICONTROL 详细信息] 选项卡。 此 [!UICONTROL 详细信息] 选项卡显示“生产”或“开发”沙盒中的所有可用沙盒。

![许可证使用情况仪表板的详细信息选项卡。](../images/license-usage/details-tab.png)

从该视图中，您可以选择 ![检查图标。](../images/license-usage/inspect-icon.png) 在沙盒名称旁边，可查看该量度的可视化图表。 此时将打开一个对话框，其中包含该量度的可视化图表。

### 可视化图表 {#visualizations}

每个可视化小组件包括以下方面：

- 跟踪量度随时间变化的折线图
- 折线图的键
- 沙盒名称
- 用于调整折线图时段的下拉菜单

线形图将贵组织的使用量数字与贵组织许可的总可用量进行比较，并提供总使用量的百分比。

![量度可视化。](../images/license-usage/visualization.png)

可以从下拉菜单中调整分析的回顾时间段。 过去30天的默认值

要选择日期范围，您可以使用日期范围下拉菜单选择要显示在仪表板中的时间段。 提供了多个选项，包括最近30天的默认值。

![可视化对话框，其中突出显示了日期范围下拉列表。](../images/license-usage/date-range.png)

您还可以选择 **[!UICONTROL 自定义日期]** 以选择显示的时间段。

![突出显示了自定义日期范围选项的许可证使用情况仪表板概述选项卡。](../images/license-usage/custom-date-range.png)

## 可用量度

许可证使用情况仪表板报告适用于组织中多个产品的多个唯一量度。 可用的量度包括：

- [!UICONTROL 沙盒数]
- [!UICONTROL 可寻址受众]
- [!UICONTROL 平均配置文件丰富度]
- [!UICONTROL 核心小时数]
- [!UICONTROL 数据湖存储]
- [!UICONTROL 每个分段扫描的数据比率]
- [!UICONTROL 可参与受众]
- [!UICONTROL 已使用的存储总数]
- [!UICONTROL 总存储空间]
- [!UICONTROL 查询服务计算小时数]

这些指标的可用性和每个指标的特定定义因贵组织购买的许可而异。 有关每个量度的详细定义，请参阅相应的产品描述文档：

| 许可 | 产品描述 |
|---|---|
| <ul><li>Adobe Experience Platform：OD LITE</li><li>Adobe Experience Platform：OD STANDARD</li><li>Adobe Experience Platform：OD粗</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform：OD</li></ul> | [Experience Platform、应用程序服务和智能服务](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT CUSTOMER DATA PLATFORM：OD</li><li>RT客户数据平台：OD PRFL到10M</li><li>RT客户数据平台：OD PRFL到50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP：OD激活</li><li>AEP：OD激活PRFL至10M</li><li>AEP：OD激活PRFL，最长50米</li></ul> | [Adobe Experience Platform激活](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP：OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>Journey Optimizer SELECT：OD</li><li>Journey Optimizer PRIME：OD</li><li>Journey Optimizer ULTIMATE：OD</li><li>UNP AJO PRIME简易版：OD</li><li>UNP AJO ULTIMATE STARTER：OD</li><li>UNP Real-Time CDP：OD配置文件编排</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/cn/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>许可证使用仪表板仅报告为您的组织配置的最新许可证。 如果为贵组织配置的最新许可证未在上表中显示，则许可证使用情况仪表板可能无法正确显示。 计划在未来的版本中，支持单个组织中的其他许可证和多个许可证。

## 后续步骤

阅读本文档后，您可以找到许可证使用情况仪表板，并查看每个已购产品、所有生产或开发沙盒以及特定沙盒的使用量度。 您可以根据贵组织购买的许可协议，查找有关贵组织可用量度的更多信息。

要了解有关Experience PlatformUI中可用的其他功能的更多信息，请参阅 [Platform UI指南](../../landing/ui-guide.md).
