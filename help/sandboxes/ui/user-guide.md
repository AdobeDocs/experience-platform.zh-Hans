---
keywords: Experience Platform；主页；热门主题；沙箱用户指南；沙箱指南
solution: Experience Platform
title: 沙箱UI指南
topic: user guide
description: 本文档提供了有关如何执行与Adobe Experience Platform用户界面中的沙箱相关的各种操作的步骤。
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '610'
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

使用以下视频快速概述如何在Experience Platform中使用沙箱。

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

要在UI中创建新沙箱，请选择屏幕右上方的&#x200B;**[!UICONTROL Create Sandbox]**&#x200B;按钮。

![](../images/ui/create-sandbox.png)

将显示&#x200B;**[!UICONTROL Create Sandbox]**&#x200B;对话框，提示您提供沙箱的显示标题和名称。 **显示标题**&#x200B;的用意是可读的，且描述性应足以易于识别。 沙箱&#x200B;**[!UICONTROL Name]**&#x200B;是用于API调用的全小写标识符，因此应该是唯一和简洁的。 沙箱&#x200B;**[!UICONTROL Name]**&#x200B;只能由字母数字字符和连字符&#x200B;**(-)**&#x200B;组成，它必须以字母开头，最多包含256个字符。

完成后，选择&#x200B;**[!UICONTROL Create]**。

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>由于您仅限于创建非生产沙箱类型，因此&#x200B;**[!UICONTROL type]**&#x200B;选项在“非生产”处被锁定，无法进行操作。

创建完沙箱后，请刷新页面，新沙箱将显示在&#x200B;**[!UICONTROL Sandboxes]**&#x200B;仪表板中，状态为“[!UICONTROL Creating]”。 新沙箱需要大约15分钟才能由系统设置，之后其状态将更改为“[!UICONTROL Active]”。

![](../images/ui/creating.png)

## 重置沙箱

>[!NOTE]
>
>此功能仅适用于非生产沙箱。 无法重置生产沙箱。

重置非生产沙箱将删除与该沙箱(模式、数据集等)关联的所有资源，同时保持沙箱的名称和关联权限。 对于具有访问权限的用户，该“干净”沙箱将继续以同一名称可用。

要在UI中重置沙箱，请在左导航中选择&#x200B;**[!UICONTROL Sandboxes]**，然后选择要重置的沙箱。 在屏幕右侧显示的对话框中，选择&#x200B;**[!UICONTROL Reset Sandbox]**。

![](../images/ui/reset-sandbox.png)

将出现一个对话框，提示您确认您的选择。 选择&#x200B;**[!UICONTROL Reset]**&#x200B;继续。

![](../images/ui/reset-confirm.png)

将显示确认消息，沙箱的状态将更改为“**[!UICONTROL Resetting]”**。 系统设置后，其状态将更新为&#x200B;**&quot;[!UICONTROL Active]&quot;**&#x200B;或&#x200B;**&quot;[!UICONTROL Failed]&quot;**。

![](../images/ui/resetting.png)

## 删除沙箱

>[!NOTE]
>
>此功能仅适用于非生产沙箱。 无法删除生产沙箱。

删除非生产沙箱将永久删除与该沙箱关联的所有资源，包括权限。

要在UI中删除沙箱，请在左导航中选择&#x200B;**[!UICONTROL Sandboxes]**，然后选择要删除的沙箱。 在屏幕右侧显示的对话框中，选择&#x200B;**[!UICONTROL Delete Sandbox]**。

![](../images/ui/delete-sandbox.png)

将出现一个对话框，提示您确认您的选择。 选择&#x200B;**[!UICONTROL Delete]**&#x200B;继续。

![](../images/ui/delete-confirm.png)

将显示确认消息，并从&#x200B;**[!UICONTROL Sandboxes]**&#x200B;工作区中删除沙箱。

## 后续步骤

此文档演示了如何在Experience Platform UI中管理沙箱。 有关如何使用沙箱API管理沙箱的信息，请参阅[沙箱开发人员指南](../api/getting-started.md)。