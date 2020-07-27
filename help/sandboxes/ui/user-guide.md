---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 沙箱用户指南
topic: user guide
translation-type: tm+mt
source-git-commit: c52d8cdbc5a4ee6fab8c2b1b284efea5f735d424
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# 沙箱用户指南

此文档提供了如何执行与Adobe Experience Platform用户界面中的沙箱相关的各种操作的步骤。

## 视图沙箱

在Experience PlatformUI中，单 **[!UICONTROL 击左]** 侧导航中的“沙箱 _[!UICONTROL ”以打开“沙]_箱”仪表板。 仪表板会列表组织的所有可用沙箱，包括沙箱类型（生产或开发）和状态（活动、创建、删除或失败）。

![](../images/ui/sandboxes-tab.png)

## 在沙箱之间切换

屏 **幕左上角** 的沙箱切换器控件显示当前活动的沙箱。

![](../images/ui/sandbox-selector.png)

要在沙箱之间切换，请单击沙箱切换器，然后从下拉列表中选择所需的沙箱。

![](../images/ui/switch-sandbox.png)

选择沙箱后，屏幕将刷新，沙箱切换器中现在提供选定沙箱。

![](../images/ui/sandbox-switched.png)

## 创建新沙箱

使用以下视频快速概述如何在Experience Platform中使用沙箱。

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

要在UI中创建新沙箱，请单击左 **[!UICONTROL 导航]** 中的“沙箱”，然后单击“ **[!UICONTROL 创建沙箱”]**。

![](../images/ui/create-sandbox-button.png)

将显 _[!UICONTROL 示“创建沙箱]_”对话框，提示您提供沙箱的显示标题和名称。 显&#x200B;**示标题**（显示标题）的用户可读性高，描述性应足以易于识别。 沙箱名**[!UICONTROL &#x200B;称&#x200B;]**是用于API调用的全小写标识符，因此应该是唯一和简洁的。

完成后，单击“ **[!UICONTROL 创建]**”。

![](../images/ui/create-sandbox-dialog.png)

>[!NOTE]
>
>由于您仅限于创建非生产沙箱类型，因 **[!UICONTROL 此类型]** 选项在“非生产”处被锁定，无法进行操作。

创建完沙箱后，刷新页面，新沙箱将显示在“沙 _[!UICONTROL 箱]_”仪表板中，状态为“[!UICONTROL 创建]”。 新沙箱需要大约15分钟时间才能由系统设置，之后其状态将变为“[!UICONTROL 活动]”。

![](../images/ui/sandbox-created.png)

## 重置沙箱

>[!NOTE]
>
>此功能仅适用于非生产沙箱。 无法重置生产沙箱。

重置非生产沙箱将删除与该沙箱(模式、数据集等)关联的所有资源，同时保留沙箱的名称和相关权限。 对于具有访问权限的用户，该“干净”沙箱将继续以相同的名称可用。

要在UI中重置沙箱，请单 **[!UICONTROL 击左]** 导航中的“沙箱”，然后单击要重置的沙箱。 在屏幕右侧显示的对话框中，单击“重置沙 **[!UICONTROL 箱”]**。

![](../images/ui/reset-sandbox-button.png)

将显示一个对话框，提示您确认您的选择。 Click **[!UICONTROL Reset]** to continue.

<img src="../images/ui/reset-are-you-sure.png" width="350"><br>

将显示一条确认消息，沙箱的状态将更改为“[!UICONTROL 重置]”。 系统设置它后，其状态将更新为“[!UICONTROL Active]”或“[!UICONTROL Failed]”。

![](../images/ui/sandbox-resetting.png)

## 删除沙箱

>[!NOTE]
>
>此功能仅适用于非生产沙箱。 无法删除生产沙箱。

删除非生产沙箱将永久删除与该沙箱相关的所有资源，包括权限。

要在UI中删除沙箱，请单 **[!UICONTROL 击左]** 导航中的“沙箱”，然后单击要删除的沙箱。 在屏幕右侧显示的对话框中，单击“删除沙 **[!UICONTROL 箱”]**。

![](../images/ui/delete-sandbox-button.png)

将显示一个对话框，提示您确认您的选择。 Click **[!UICONTROL Delete]** to continue.

<img src="../images/ui/delete-are-you-sure.png" width="350"><br>

此时会显示一条确认消息，沙箱会从“沙箱”工 _[!UICONTROL 作区中]_删除。

## 后续步骤

此文档演示了如何在Experience PlatformUI中管理沙箱。 有关如何使用沙箱API管理沙箱的信息，请参阅沙箱开 [发人员指南](../api/getting-started.md)。