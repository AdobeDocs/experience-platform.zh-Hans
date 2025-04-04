---
title: AEM资产分析扩展概述
description: 了解Adobe Experience Platform中的AEM资产分析标记扩展。
exl-id: 7d3edd42-09fe-4e40-93dc-1edd2fdbb121
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 82%

---

# AEM资产分析扩展概述

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

这项扩展旨在与 [AEM 资产分析](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)结合使用。更具体地说，它可以替换“pageTracker”进程和嵌入代码。当完成配置后，这项扩展会向 Adobe Analytics 发送资产“展示次数”和“单击次数”量度，随后，这些量度将导入 AEM 资产分析报表中。****&#x200B;接下来，可使用 AEM 资产分析或 Adobe Analytics 项目工作区来报告资产量度。

## 扩展的先决条件

### Analytics

Analytics 中的 AEM 资产报表包含三个 AEM 维度：

* 资产 ID
* 资源Source
* 已单击资产

另外，还包括两个量度：
* 资产展示次数
* 资产单击次数。

必须通过Analytics管理员来启用这些报表(选择&#x200B;**[!UICONTROL Analytics] > [!UICONTROL 管理员] > [!UICONTROL 报表包] > `<report suite>` > [!UICONTROL 编辑设置] > [!UICONTROL AEM] > [!UICONTROL AEM Assets报表]**)，然后才能使用此扩展填充这些报表。

Adobe Experience Platform的“*Adobe Analytics*”标记扩展必须安装到同一Web属性中。

### Adobe Experience Manager (AEM)

1. 启用 [AEM 资产分析](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)。在AEM中，选择&#x200B;**[!UICONTROL 工具> Assets]**，然后打开&#x200B;**[!UICONTROL 分析配置]**&#x200B;面板。

1. 禁用 UUID 跟踪。

   >[!IMPORTANT]
   >
   >如果选中AEM资源配置设置&#x200B;**[!UICONTROL 禁用UUID跟踪]**，则此扩展将&#x200B;*不是*&#x200B;函数。 默认情况下，该复选框处于未选中状态。

   ![禁用 UUID 跟踪](images/disableassets.jpg)

## 配置 Adobe Experience Manager (AEM)

本部分将介绍如何使用Adobe Experience Platform中的标记配置AEM，如何在AEM中启用资产分析，以及如何为Assets启用UUID跟踪。

### 将AEM与标记集成

通过Adobe I/O，完成了建议的[Experience Platform](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)与Adobe Experience Manager的集成。

1. [使用Adobe I/O连接AEM和标记](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html)。

2. [创建Adobe Experience Platform Cloud Service配置](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/create-launch-cloud-service.html)。

### 在 AEM 中启用资产分析

有关启用资产分析的操作说明，请参阅 [Experience Manager 6.5 Assets 用户指南](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)。

### 启用资产的 UUID 跟踪

通过 AEM 中资产的 UUID 来跟踪 Analytics 中的资产。

要启用资产的 UUID 跟踪功能，请打开可编辑模板的组件策略控制台，并取消选中“禁用 UUID 跟踪”属性。（默认情况下，将为 OOTB 图像组件选中此属性。）

![](images/uuid.png)

启用 UUID 后，您应该会看到“data-asset-id”数据元素已采用资产的 UUID 进行填充。Analytics 使用 UUID 来跟踪资产的单击次数和展示次数。

![](images/uuid-code.png)

## 扩展的用途

这项扩展包含两个事件和一项操作。

* **已单击资产：**&#x200B;作为一个&#x200B;_事件_，它的触发条件是：访客已选择某个为了跟踪而启用的 AEM 资产，且具有目标（href 属性）。

* **已单击资产（无目标）：**&#x200B;作为一个&#x200B;_事件_，它的触发条件是：访客已选择某个为了跟踪而启用的 AEM 资产，但是没有目标（无 href 属性）。

* **设置 AA 变量：**&#x200B;作为一项&#x200B;__&#x200B;操作，它将根据使用的事件以及该事件和操作的配置方式，设置那些为 AEM Assets 保留的 Analytics 变量（上下文数据变量 `a.assets.source`、`a.assets.idlist` 和 `a.asset.clickedid`）。这项扩展不使用任何 Analytics 事件、prop 或 eVar。

### 资产展示次数

将“设置AA变量”操作添加到新的或现有的标记规则中，以便在每个页面上触发并发送Analytics图像请求。 “设置 AA 变量”操作必须显示在“Adobe Analytics - 发送信标”操作&#x200B;**之前**。至于其他操作，可根据需要进行添加。

在 **[设置 AA 变量]** 配置页面中，选中 **[已查看的资产]**（默认）选项。该操作将会专门针对访客实际看到的资产，设置“展示次数”事件。

>[!NOTE]
>
>尽管没有推荐，但是“设置 AA 变量”操作也支持“已加载”选项，无论访客是否看到资产，该选项都会发送页面上每个资产的资产展示次数。

![展示次数](images/sendImpressions.jpg)


### 资产单击次数

通过“已单击资产”事件和“设置 AA 变量”操作，可配置第二个规则。应该配置“已单击资产”事件，以便将“已单击资产的图像请求”设置为“按页面加载”（默认）。这个规则不要求 Adobe Analytics 执行任何操作（如发送信标），因为资产 ID 将保存在 `sessionStorage` 中，并且由后续的展示次数规则发送。

另外，“已单击资产”事件还支持“单击时”的“已单击资产的图像请求”设置。这会将相关的单击量度立即发送至 Analytics，同时还要求执行 Analytics“发送信标”操作。

![页面加载时的资产单击次数](images/sendClickOnPageload.jpg)

配置第三个规则，当页面上的资产没有目标（无 `href` 属性）时，将触发该规则。新规则至少需要使用“已单击资产（无目标）”事件，以及“设置 AA 变量”操作和“Adobe Analytics - 发送信标”操作。至于其他条件和操作，可以根据需要进行添加。

![无目标的资产单击次数](images/sendClickOnClickNoDestination.jpg)

### 扩展测试提示

请根据上述说明，配置三项规则：

* 资产展示次数
* 资产单击次数
* 无目标的资产单击次数

**展示次数**

1. 导航到包含 AEM 资产的页面。

1. 如果浏览器中没有可见的资产，请您滚动浏览，直到您至少能够看见一个资产，然后选择该资产，或者只是导航到其他页面。

1. 查看 Analytics 图像请求。

   如果 `a.assets.idlist` 包含上一页可见的资产 ID，则该规则正确运行。

   如果图像请求中没有出现 `a.assets.idlist`，则很可能是由于以下两个原因之一：

   * 浏览器的查看区域从未出现任何资产

   * 页面上的资产均未使用 AEM 中启用的[资产分析](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)进行配置。

**单击次数**

1. 导航到包含 AEM 资产的页面。

1. 选择其中一个资产。

在生成的 Analytics 图像请求（从下一页开始）中，如果 `a.assets.idlist` 在目标页面上具有资产 ID，并且 `a.assets.clickedid` 具有在原始页面上选择的资产的资产 ID，那么该规则可以正确运行。

如果图像请求中没有出现 `a.assets.clickedid`，则很可能是因为已选择资产未在 AEM 中启用[资产分析](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)。

**无目标单击次数**

1. 导航到一个页面，该页面至少包含一个没有目标（无 `href` 属性）的 AEM 资产。

1. 选择该资产。

在生成的 Analytics 图像请求中，如果 `a.assets.clickedid` 具有资产 ID，则该规则可以正确运行。

如果图像请求中没有出现 `a.assets.clickedid`，则很可能是因为已选择资产未在 AEM 中启用[资产分析](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html)。
