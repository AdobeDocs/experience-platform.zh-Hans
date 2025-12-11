---
title: 比较资源修订版本
description: 了解如何在Adobe Experience Platform中查看标记资源的修订历史记录。
exl-id: 95b22641-9f6f-4aac-a727-d99098f040a4
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 97%

---

# 比较资源修订版本

比较资源修订版本可查看单个资源的历史记录。您可以将资源的当前状态与旧版本进行比较，也可以将资源的当前已发布版本与已保存的一组最新更改进行比较。

## 启动比较

对于所有资源类型，启动比较的过程都是相同的。打开单个资源的编辑视图，然后找到 **[!UICONTROL Save]** 按钮旁边的三个圆点图标，即可查看该资源的可用操作。从列表中选择 **[!UICONTROL Compare Revisions]**。

![启动扩展比较](../../images/compare-initiate-extension.png)

对于扩展，您可以在查看已安装的扩展列表时，通过选择 **[!UICONTROL Configure]** 按钮来访问详细信息视图。对于数据元素和规则，从列表中选择一个即可。

## 使用比较视图

启动比较时，默认视图会在右侧显示最新版本。此版本包括您在编辑视图中对资源所做的任何未保存的更改。（请注意下图中右侧的“Unsaved Changes”标签。）

在左侧，您可以从任何现有的修订版本中进行选择，以与“最新版本”进行比较。

![比较 Analytics 扩展的版本](../../images/compare-interpret-extension.png)

选择 **[!UICONTROL Use These Changes]** 可将所选修订版本（左）的设置复制到最新版本（右）中。此操作会将旧版本的设置复制到最新的未保存更改中。如果您希望保留这些更改，请确保在退出比较视图后单击 **[!UICONTROL Save]**。

>[!TIP]
>单个资源可以同时具有属性和设置。这些设置会存储为 JSON 块。JSON 块是一种存储数据的结构化方式，但灵活性较高，扩展开发人员可以放置他们所需的任何内容，以便能够利用扩展实现所需的任何操作。
>比较视图的初始版本将原始形式的设置显示为 JSON。在未来的增强功能中，您将能够以不同的方式查看各个版本，包括进行详细的代码比较和使用扩展开发人员提供的扩展视图。

## 比较扩展

扩展具有单个屏幕来显示不同版本之间的差异。

比较视图会突出显示不同设置版本之间的差异。单个设置的添加和移除通过任意方向上的展开线条来表示。

![比较 Analytics 扩展的不同版本](../../images/compare-extension.png)

在上图中，您可以看到以下更改：

* [!DNL Adobe Analytics] 扩展已更新为新版本，如顶部的橙色版本号所示。
* `orgID` 和 `currencyCode` 已更改为设置中橙色展开部分所指示的设置。

## 比较数据元素

数据元素具有单个屏幕来显示差异，但由于数据元素除了其设置之外还具有其他属性，因此也会显示其他信息。已更改的属性会以橙色突出显示。

![比较数据元素的不同版本](../../images/compare-data-element.png)

在上图中，您可以看到以下更改：

* 名称已从“Page Name 2”更改为“My Special Page Name”，如橙色条所示。
* 类型已从“JavaScript Variable”更改为“Page Info”。
* 已添加默认值“b”。
* 已选中“Force lowercase value”。
* 已选中“Clean text”。
* 设置已更改。（JavaScript Variable 类型的设置与 Page Info 类型的设置不同。）

如果设置块较大，您可以展开设置部分，以便更好地查看。

## 比较规则

规则由许多规则组件组成。要了解如何更改规则，您需要先了解如何添加和移除组件以及如何修改单个组件。因此，在比较规则的版本时，实际上会有两个屏幕。

第一个屏幕显示简要视图，该视图会突出显示规则中规则组件排列的更改。所做的更改会突出显示。显示的更改分为几种不同的类型。

![比较规则的不同版本](../../images/compare-rule.png)

在上图中，您可以看到以下更改：

* 规则名称已从“Analytics”更改为“Baseline Analytics”，如 Name 旁边的橙色条所示。
* 已添加“Core - Domain”条件，如橙色“+”图标和右侧添加的组件所示。
* 已移除“[!DNL Adobe Analytics] - Clear Variables”操作，如橙色“-”图标和右侧缺失的组件所示。
* 已修改“[!DNL Adobe Analytics] - Set Variables”操作，如左侧和右侧组件版本之间的橙色线所示。如果组件顺序未发生更改，则此线为直线。
* “[!DNL Adobe Analytics] - Set Variables”操作和“[!DNL Adobe Analytics] - Send Beacon”操作顺序已更改，如连接左右两侧不同组件版本的曲线所示。

要查看对其中一个规则组件进行的特定修改，请选择要查看的特定组件。将鼠标悬停在线条上时，线条会变为蓝色。

![选择要查看详细信息的组件](../../images/compare-rule-component-click.png)

单个规则组件的比较方式与数据元素的比较方式相同。

![比较单个规则组件的不同版本](../../images/compare-rule-component.png)

在上图中，您可以看到以下更改：

* 规则组件已更改，添加了值为“1”的 eVar2。

如果设置块较大，您可以展开设置部分，以便更好地查看。
