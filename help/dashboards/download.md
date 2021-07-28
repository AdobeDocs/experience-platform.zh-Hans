---
solution: Experience Platform
title: 将Experience Platform功能板下载为PDF
type: Documentation
description: 使用Experience PlatformUI中提供的下载到PDF功能，保存功能板可视化的副本。
source-git-commit: a95f77d048b5bb9562507122d249f592e68a1bcf
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# 将功能板下载为PDF

可以从Platform用户界面中将Adobe Experience Platform中的功能板下载为PDF，以便与您组织的成员共享信息。

本文档概要介绍了如何使用Platform UI下载功能板，以及如何使用默认的浏览器打印菜单将功能板保存为PDF。

>[!WARNING]
>
>功能板中包含的数据可能包含有关客户的个人身份信息(PII)或与贵组织相关的敏感数据。 保存为PDF的任何功能板数据都应根据贵组织的数据隐私准则进行适当处理。

## 下载功能板

要开始下载功能板，请导航到要下载的功能板（例如，[!UICONTROL Profiles]功能板），然后从功能板右上角选择更多选项菜单(**`...`**)。 接下来，选择&#x200B;**[!UICONTROL Download]**。

![](images/download/download-button.png)

## 预览PDF

选择&#x200B;**[!UICONTROL Download]**&#x200B;后，将打开浏览器的默认打印菜单。 在此示例中，显示Google Chrome打印菜单。

利用打印菜单，可预览将保存的PDF。 PDF是功能板小组件在平台UI中显示时的真实表示形式，并且PDF的大小会自动调整以在单个页面上显示所有当前可见的功能板小组件。

![](images/download/download-chrome-print.png)

PDF包含自动生成的标题，其中包含Experience Platform徽标、功能板名称、您的名称以及功能板下载的日期和时间。 此信息为只读，无法在PDF中编辑。

![](images/download/download-pdf.png)

## 另存为PDF

预览PDF后，选择&#x200B;**保存**&#x200B;以选择要保存PDF的位置。

>[!NOTE]
>
>如果需要，可以使用&#x200B;**目标**&#x200B;下拉列表选择&#x200B;**另存为PDF**（如果未自动为您选择该选项）。

![](images/download/download-chrome-print-destination.png)

## 自定义功能板PDF

生成的PDF与您在UI中可以看到的功能板相匹配，并且只包含功能板中当前可见的小组件。 可以自定义某些功能板以更改小组件的大小和位置，或在视图中添加和删除小组件。 在Platform UI中自定义功能板的外观也会更改生成的PDF的外观。

例如，您可以修改用户档案仪表板的外观，以包含堆叠在三个标准小组件上的多个全宽小组件。

![](images/download/download-modify.png)

选择下载更新的功能板会生成与自定义用户档案功能板的外观相匹配的新PDF预览。 它还会自动调整PDF的大小，以确保所有可见小组件都包含在一页PDF中。

![](images/download/download-chrome-print-modified.png)

要了解有关自定义功能板的更多信息，请首先阅读[功能板自定义概述](customize/overview.md)。

## 后续步骤

现在，您已下载功能板并将其另存为PDF，接下来可以重复执行这些步骤以下载其他功能板或与组织成员共享该PDF。