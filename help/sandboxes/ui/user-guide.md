---
keywords: Experience Platform；主页；热门主题；沙箱用户指南；沙箱指南
solution: Experience Platform
title: 沙箱UI指南
topic: 用户指南
description: 本文档提供了有关如何执行与Adobe Experience Platform用户界面中的沙箱相关的各种操作的步骤。
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# 沙箱UI指南

本文档提供了有关如何执行与Adobe Experience Platform用户界面中的沙箱相关的各种操作的步骤。

## 视图沙箱

在Experience PlatformUI中，在左侧导航中选择&#x200B;**[!UICONTROL Sandboxes]**&#x200B;以打开&#x200B;**[!UICONTROL Sandboxes]**&#x200B;仪表板。 仪表板将列表组织的所有可用沙箱，包括沙箱类型（生产或开发）和状态（活动、创建、删除或失败）。

![](../images/ui/view-sandboxes.png)

## 在沙箱之间切换

屏幕左上角的&#x200B;**沙箱切换器**&#x200B;控件显示当前活动的沙箱。

![](../images/ui/sandbox-switcher.png)

要在沙箱之间切换，请选择沙箱切换器，然后从下拉列表中选择所需的沙箱。

![](../images/ui/switcher-menu.png)

选择沙箱后，屏幕将刷新，沙箱切换器中现在提供选定沙箱。

![](../images/ui/switched.png)

## 沙箱会话

使用沙箱切换器菜单中的搜索功能，您可以浏览可用沙箱的列表。 键入要访问的沙箱的名称，以过滤组织可用的所有沙箱。

![](../images/ui/sandbox-search.png)

## 创建新沙箱

>[!NOTE]
>
>“多个制作沙箱”功能是测试版。

使用以下视频快速概述如何在Experience Platform中使用沙箱。

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

要创建新沙箱，请选择屏幕右上方的&#x200B;**[!UICONTROL Create Sandbox]**&#x200B;按钮。

![](../images/ui/create-sandbox.png)

将显示&#x200B;**[!UICONTROL Create Sandbox]**&#x200B;对话框，提示您提供沙箱的类型、标题和名称。 如果要创建开发沙箱，请在显示的下拉面板中选择&#x200B;**[!UICONTROL Development]**。 如果要创建生产沙箱，请选择&#x200B;**[!UICONTROL Production]**。

标题的用意是人可读，并且应具有足够的描述性，以便于识别。 沙箱名称是API调用中使用的全小写标识符，因此应是唯一和简洁的。 沙箱名称必须只包含字母数字字符和连字符(`-`)，且必须以字母开头，最多包含256个字符。

完成后，选择&#x200B;**[!UICONTROL Create]**。

![](../images/ui/create-dialog.png)

创建完沙箱后，请刷新页面，新沙箱将显示在&#x200B;**[!UICONTROL Sandboxes]**&#x200B;仪表板中，状态为“[!UICONTROL Creating]”。 新沙箱需要大约15分钟才能由系统设置，之后其状态将更改为“[!UICONTROL Active]”。

## 重置沙箱

>[!NOTE]
>
>除了默认的生产沙箱外，您可以重置组织中的任何生产沙箱或开发沙箱。

重置生产或开发沙箱将删除与该沙箱(模式、数据集等)关联的所有资源，同时保留沙箱的名称和关联权限。 对于具有访问权限的用户，该“干净”沙箱将继续以同一名称可用。

从沙箱列表中选择要重置的沙箱。 在出现的右侧导航面板中，选择&#x200B;**[!UICONTROL Sandbox reset]**。

![](../images/ui/reset-sandbox.png)

将出现一个对话框，提示您确认您的选择。 选择&#x200B;**[!UICONTROL Continue]**&#x200B;以继续。

![](../images/ui/reset-confirm.png)

在最终确认窗口中，在对话框中输入沙箱的名称，然后选择&#x200B;**[!UICONTROL Reset]**

![](../images/ui/reset-final-confirm.png)

## 删除沙箱

>[!NOTE]
>
>除了默认的生产沙箱外，您可以删除组织中的任何生产沙箱或开发沙箱。

删除生产沙箱或开发沙箱将永久删除与该沙箱关联的所有资源，包括权限。

从沙箱列表中选择要删除的沙箱。 在出现的右侧导航面板中，选择&#x200B;**[!UICONTROL Delete]**。

![](../images/ui/delete-sandbox.png)

将出现一个对话框，提示您确认您的选择。 选择&#x200B;**[!UICONTROL Continue]**&#x200B;以继续。

![](../images/ui/delete-confirm.png)

在最终确认窗口中，在对话框中输入沙箱的名称，然后选择&#x200B;**[!UICONTROL Delete]**

![](../images/ui/delete-final-confirm.png)

## 后续步骤

此文档演示了如何在Experience Platform UI中管理沙箱。 有关如何使用沙箱API管理沙箱的信息，请参阅[沙箱开发人员指南](../api/getting-started.md)。