---
keywords: Experience Platform;home;popular topics;sandbox user guide;sandbox guide
solution: Experience Platform
title: 沙箱用户指南
topic: user guide
description: 此文档提供了如何在Adobe Experience Platform用户界面中执行与沙箱相关的各种操作的步骤。
translation-type: tm+mt
source-git-commit: 2d1a9699866bd39de7251731e9f0cd2f753a5083
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---


# 沙箱用户指南

此文档提供了如何在Adobe Experience Platform用户界面中执行与沙箱相关的各种操作的步骤。

## 视图沙箱

在Experience PlatformUI中，在左 **[!UICONTROL 侧导航]** 中选择“沙箱”以打开“ **[!UICONTROL 沙箱]** ”仪表板。 仪表板会列表组织的所有可用沙箱，包括沙箱类型（生产或开发）和状态（活动、创建、删除或失败）。

![](../images/ui/view-sandboxes.png)

## 在沙箱之间切换

屏 **幕左上角** 的沙箱切换器控件显示当前活动的沙箱。

![](../images/ui/sandbox-switcher.png)

要在沙箱之间切换，请选择沙箱切换器，然后从下拉列表中选择所需的沙箱。

![](../images/ui/switcher-menu.png)

选择沙箱后，屏幕将刷新，沙箱切换器中现在提供选定沙箱。

![](../images/ui/switched.png)

## 沙箱会话

您可以使用沙箱切换器菜单中的搜索功能，在沙箱列表中导航。 键入要访问的沙箱的名称，以过滤组织可用的所有沙箱。

![](../images/ui/sandbox-search.png)

## 创建新沙箱

使用以下视频快速概述如何在Experience Platform中使用沙箱。

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

要在UI中创建新沙箱，请选 **[!UICONTROL 择屏幕右上]** 方的“创建沙箱”按钮。

![](../images/ui/create-sandbox.png)

将显 **[!UICONTROL 示“创建沙箱]** ”对话框，提示您提供沙箱的显示标题和名称。 显 **示标题** （显示标题）的用户可读性高，描述性应足以易于识别。 沙箱名 **[!UICONTROL 称]** 是用于API调用的全小写标识符，因此应该是唯一和简洁的。 沙箱名 **[!UICONTROL 称]** 只能由字母数字字符和连字符 **(-)组成**，它必须以字母开头，最多包含256个字符。

完成后，选择 **[!UICONTROL 创建]**。

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>由于您仅限于创建非生产沙箱类型，因 **[!UICONTROL 此类型]** 选项在“非生产”处被锁定，无法进行操作。

创建完沙箱后，刷新页面，新沙箱将显示在“沙 **[!UICONTROL 箱]** ”仪表板中，状态为“[!UICONTROL 创建]”。 新沙箱需要大约15分钟时间才能由系统设置，之后其状态将变为“[!UICONTROL 活动]”。

![](../images/ui/creating.png)

## 重置沙箱

>[!NOTE]
>
>此功能仅适用于非生产沙箱。 无法重置生产沙箱。

重置非生产沙箱将删除与该沙箱(模式、数据集等)关联的所有资源，同时保留沙箱的名称和相关权限。 对于具有访问权限的用户，该“干净”沙箱将继续以相同的名称可用。

要在UI中重置沙箱，请在 **[!UICONTROL 左导航]** 中选择“沙箱”，然后选择要重置的沙箱。 在屏幕右侧显示的对话框中，选择“重置沙 **[!UICONTROL 箱”]**。

![](../images/ui/reset-sandbox.png)

将显示一个对话框，提示您确认您的选择。 选择 **[!UICONTROL 重置]** ，继续。

![](../images/ui/reset-confirm.png)

将显示一条确认消息，沙箱的状态将更改为“**[!UICONTROL 重置]”**。 一旦系统设置了它，其状态将更新为“ **活[!UICONTROL 动]”** 或“ **失[!UICONTROL 败]”**。

![](../images/ui/resetting.png)

## 删除沙箱

>[!NOTE]
>
>此功能仅适用于非生产沙箱。 无法删除生产沙箱。

删除非生产沙箱将永久删除与该沙箱相关的所有资源，包括权限。

要在UI中删除沙箱，请 **[!UICONTROL 在左导航]** 中选择“沙箱”，然后选择要删除的沙箱。 在屏幕右侧显示的对话框中，选择“删除沙 **[!UICONTROL 箱”]**。

![](../images/ui/delete-sandbox.png)

将显示一个对话框，提示您确认您的选择。 选择 **[!UICONTROL 删除]** ，继续。

![](../images/ui/delete-confirm.png)

此时会显示一条确认消息，沙箱会从“沙箱”工 **[!UICONTROL 作区中]** 删除。

## 后续步骤

此文档演示了如何在Experience PlatformUI中管理沙箱。 有关如何使用沙箱API管理沙箱的信息，请参阅沙箱开 [发人员指南](../api/getting-started.md)。