---
title: 扩展版本视图
description: 本指南详细介绍了Adobe Experience Platform保障中有关“扩展版本”视图的信息。
exl-id: a3a649da-1ef1-45a3-a1ed-6a7bc16c2987
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# “扩展版本”视图

扩展版本视图允许您快速排序和查看已安装的Adobe Experience Platform Mobile扩展，以及这些扩展是否在连接到保障会话的客户端中处于最新状态。

## 扩展版本视图入门

晚于 [设置Assurance](../tutorials/implement-assurance.md)，在 **主页** 视图，选择 **[!UICONTROL 扩展版本]**

![扩展版本](./images/versions/versions-extension.png)

## 检查您的版本是否为最新版本

在此视图中，有一个表格既显示每个Mobile SDK的最新版本，也显示您安装的当前版本（如果适用）。 当版本与最新版本同步时，安装的版本将显示绿色标记。 否则，徽章将显示为红色。

![扩展版本比较](./images/versions/versions-extension-version.png)

## 导出版本

在视图的右上方，您可以选择 **[!UICONTROL 导出版本]** 这会为您提供包含所有扩展信息的JSON有效负载以及客户端使用的平台。 您可以选择将此数据导出到JSON文件，或将其复制到剪贴板。

![扩展版本导出](./images/versions/versions-extension-export.png)
