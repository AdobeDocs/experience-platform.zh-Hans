---
solution: Experience Platform
title: 将Experience Platform功能板下载到PDF
type: Documentation
description: 使用Experience PlatformUI中提供的“下载到PDF”功能保存功能板可视化的副本。
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: 5d9428c4323e65c2605fd116160e160af7d9086d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 将功能板下载到PDF

可以从Platform用户界面中将Adobe Experience Platform中的功能板下载到PDF中，以便与您组织的成员共享信息。

本文档概要介绍了如何使用Platform UI下载功能板，以及如何使用默认的浏览器打印菜单保存功能板以PDF。

>[!WARNING]
>
>功能板中包含的数据可能包含有关客户的个人身份信息(PII)或与贵组织相关的敏感数据。 保存到PDF的任何功能板数据都应根据贵组织的数据隐私准则进行适当处理。

## 下载功能板

要开始下载功能板，请导航到要下载的功能板(例如， [!UICONTROL 用户档案] 功能板)，然后选择更多选项菜单(**`...`**)。 接下来，选择 **[!UICONTROL 下载]**.

![Experience Platform配置文件功能板中突出显示了省略号和下载下拉菜单。](images/download/download-button.png)

## 预览PDF

选择后 **[!UICONTROL 下载]**，则会打开浏览器的默认打印菜单。 在此示例中，显示了Google Chrome打印菜单。

利用打印菜单，可预览将保存的PDF。 PDF是功能板小组件在Platform UI中显示的真实表示形式，并且PDF的大小会自动调整以在单个页面上显示所有当前可见的功能板小组件。

![以单页格式显示“配置文件”概述，右侧为“打印选项”面板。](images/download/download-chrome-print.png)

该PDF包含自动生成的标题，其中包含Experience Platform徽标、功能板名称、您的名称以及功能板的下载日期和时间。 此信息是只读的，无法在PDF中编辑。

![自动生成的标题突出显示的打印预览的特写。](images/download/download-pdf.png)

## 另存为PDF

预览PDF后，选择 **保存** ，以选择要保存PDF的位置。

>[!NOTE]
>
>如有必要，您可以使用 **目标** 选择下拉列表 **另存为PDF** 如果未为您自动选择该选项，则。

![以单页格式显示配置文件概述，并突出显示“目标”下拉列表“另存为PDF打印”选项。](images/download/download-chrome-print-destination.png)

## 自定义功能板PDF

生成的PDF与您在UI中可以看到的功能板相匹配，并且只包含功能板中当前可见的小组件。 可以自定义某些功能板以更改小组件的大小和位置，或在视图中添加和删除小组件。 在Platform UI中自定义功能板的外观也会更改所生成PDF的外观。

例如，您可以修改用户档案仪表板的外观，以包含堆叠在三个标准小组件上的多个全宽小组件。

![展示细长小组件显示的用户档案仪表板。](images/download/download-modify.png)

选择下载更新的功能板，将会生成与自定义用户档案功能板的外观相匹配的新PDF预览。 它还会自动调整PDF的大小，以确保所有可见小组件都包含在一页PDF中。

![以单页格式显示“配置文件”概述，右侧为“打印选项”面板。](images/download/download-chrome-print-modified.png)

要了解有关自定义功能板的更多信息，请首先阅读 [功能板自定义概述](customize/overview.md).

## 后续步骤

现在，您已下载功能板并将其另存为PDF，接下来可以重复这些步骤以下载其他功能板或与组织成员共享PDF。
