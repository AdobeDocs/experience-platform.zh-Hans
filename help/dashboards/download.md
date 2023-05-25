---
solution: Experience Platform
title: 下载Experience Platform功能板以PDF
type: Documentation
description: 使用Experience PlatformUI中提供的“下载到PDF”功能保存功能板可视化图表的副本。
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: 5d9428c4323e65c2605fd116160e160af7d9086d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 下载功能板以PDF

可以从Platform用户界面中下载Adobe Experience Platform中的仪表板以PDF，以促进与组织成员共享信息。

本文档概要介绍了如何使用Platform UI下载功能板，以及使用默认浏览器打印菜单将功能板保存到PDF。

>[!WARNING]
>
>功能板中包含的数据可能包含有关客户的个人身份信息(PII)或与您的组织相关的敏感数据。 任何保存到PDF的仪表板数据都应根据贵组织的数据隐私准则进行适当处理。

## 下载仪表板

要开始下载功能板，请导航到要下载的功能板(例如， [!UICONTROL 配置文件] 功能板)，然后选择更多选项菜单(**`...`**)。 接下来，选择 **[!UICONTROL 下载]**.

![突出显示带有省略号和下载下拉列表的Experience Platform配置文件仪表板。](images/download/download-button.png)

## 预览PDF

选择后 **[!UICONTROL 下载]**，将会打开浏览器的默认打印菜单。 在此示例中，显示Google Chrome打印菜单。

打印菜单允许您预览将保存的PDF。 该PDF真实地呈现了仪表板小组件在Platform UI中的显示效果，并且该PDF的大小会自动调整为在单个页面上显示当前可见的所有仪表板小组件。

![配置文件概述以单页格式显示，打印选项面板位于右侧。](images/download/download-chrome-print.png)

该PDF包含一个自动生成的标头，其中包含Experience Platform徽标、功能板名称、您的姓名以及功能板的下载日期和时间。 此信息是只读的，无法在PDF中编辑。

![突出显示自动生成标题的打印预览的特写。](images/download/download-pdf.png)

## 另存为PDF

预览PDF后，选择 **保存** 选择要保存PDF的位置。

>[!NOTE]
>
>如有必要，您可以使用 **目标** 下拉菜单选择 **另存为PDF** 如果未自动为您选择此选项。

![配置文件概述以单页格式显示，其中目标下拉菜单另存为PDF打印选项突出显示。](images/download/download-chrome-print-destination.png)

## 自定义功能板PDF

生成的PDF与可在UI中看到的仪表板匹配，并且仅包括当前在仪表板中可见的小部件。 可以自定义某些仪表板，以更改小部件的大小和位置，或从视图中添加和删除小部件。 在Platform UI中自定义仪表板的外观也会更改生成的PDF的外观。

例如，您可以修改用户档案仪表板的外观，使其包含栈叠在三个标准构件上方的多个全角构件。

![此时会显示展示细长小部件的用户档案仪表板。](images/download/download-modify.png)

选择以下载更新的仪表板会导致出现一个与自定义配置文件仪表板外观匹配的新PDF预览。 它还会自动调整PDF的大小，以确保所有可见小组件都包含在单页PDF中。

![配置文件概述以单页格式显示，打印选项面板位于右侧。](images/download/download-chrome-print-modified.png)

要了解有关自定义功能板的更多信息，请从阅读 [仪表板自定义概述](customize/overview.md).

## 后续步骤

现在您已经下载了功能板并将其另存为PDF，您可以重复这些步骤来下载其他功能板或与PDF成员共享该功能。
