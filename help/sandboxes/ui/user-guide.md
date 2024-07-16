---
keywords: Experience Platform；主页；热门主题；沙盒用户指南；沙盒指南
solution: Experience Platform
title: 沙盒UI指南
description: 本文档提供了有关如何在Adobe Experience Platform用户界面中执行与沙盒相关的各种操作的步骤。
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 0db23e475d6546ebb886a56d5915d023ea215125
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 5%

---

# 沙盒UI指南

本文档提供了有关如何在Adobe Experience Platform用户界面中执行与沙盒相关的各种操作的步骤。

## 查看沙盒

在Platform UI中，在左侧导航中选择&#x200B;**[!UICONTROL 沙盒]**，然后选择&#x200B;**[!UICONTROL 浏览]**&#x200B;以打开[!UICONTROL 沙盒]仪表板。 仪表板列出了您组织的所有可用沙盒，包括其各自的类型（生产或开发）。

![查看 — 沙盒](../images/ui/view-sandboxes.png)

## 在沙盒之间切换

沙盒指示器位于Platform UI的顶部标题中，并显示您当前所在的沙盒的标题、其区域和类型。

![沙盒指示器](../images/ui/sandbox-indicator.png)

要在沙盒之间切换，请选择沙盒指示器，然后从下拉列表中选择所需的沙盒。

![switcher-interface](../images/ui/switcher-interface.png)

选择沙盒后，屏幕将刷新并更新到您选择的沙盒。

![沙盒已交换](../images/ui/sandbox-switched.png)

## 创建新沙盒 {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="沙盒名称"
>abstract="沙盒名称是在后端用于为此沙盒创建唯一 ID 的文本。"

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="沙盒标题"
>abstract="沙盒标题是在整个 Experience Platform UI 的菜单和下拉列表中代表沙盒的显示名称。"

>[!NOTE]
>
>创建新沙盒需要先将其添加到[[!UICONTROL 权限]](../../access-control/abac/ui/permissions.md)中的角色，然后才能开始使用。 要了解如何为角色配置沙盒，请参阅[为角色管理沙盒](../../access-control/abac/ui/permissions.md#managing-sandboxes-for-role)文档。

请观看以下视频，快速概述如何在Experience Platform中使用沙盒。

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

要创建新沙盒，请选择屏幕右上角的&#x200B;**[!UICONTROL 创建沙盒]**。

![create-sandbox](../images/ui/create-sandbox.png)

出现&#x200B;**[!UICONTROL 创建沙盒]**&#x200B;对话框。 如果要创建开发沙盒，请在下拉面板中选择&#x200B;**[!UICONTROL 开发]**。 要创建新的生产沙盒，请选择&#x200B;**[!UICONTROL 生产]**。

![沙盒类型](../images/ui/sandbox-type.png)

选择类型后，为您的沙盒提供名称和标题。 标题应该易于用户识别，并且应该具有足够的描述性以便轻松识别。 沙盒名称是用于API调用的全小写标识符，因此应唯一且简洁。 沙盒名称必须以字母开头，最多可包含256个字符，并且仅由字母数字字符和连字符(-)组成。

完成后，选择&#x200B;**[!UICONTROL 创建]**。

![沙盒信息](../images/ui/sandbox-info.png)

创建完沙盒后，刷新页面，新沙盒将出现在&#x200B;**[!UICONTROL 沙盒]**&#x200B;仪表板中，状态为“[!UICONTROL 正在创建]”。 系统配置新沙盒大约需要30秒，之后沙盒的状态将更改为“[!UICONTROL 活动]”。

![new-sandbox](../images/ui/new-sandbox.png)

## 重置沙盒

>[!WARNING]
>
>以下是可阻止您重置默认生产沙盒或用户创建的生产沙盒的异常列表：
>* 如果Adobe Analytics也在使用该沙盒中托管的身份图形进行[Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html)功能，则无法重置默认生产沙盒。
>* 如果Adobe Audience Manager也在使用这个沙盒中托管的身份图形进行[基于人员的目标(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html)，则无法重置默认的生产沙盒。
>* 如果默认生产沙盒包含CDA和PBD功能的数据，则无法重置该沙盒。
>* 用于在警告消息后重置与Adobe Audience Manager或Audience Core Service进行双向区段共享的用户创建的生产沙盒。
>* 在启动沙盒重置之前，您将需要手动删除合成，以确保正确清理关联的受众数据。

### 删除受众合成

受众构成当前未与沙盒重置功能集成，因此需要手动删除受众才能执行沙盒重置。

从左侧导航中选择&#x200B;**[!UICONTROL 受众]**，然后选择&#x200B;**[!UICONTROL 合成]**。

![[!UICONTROL 受众]工作区中的[!UICONTROL 合成]选项卡。](../images/ui/audiences.png)

接下来，选择第一个受众旁边的省略号(`...`)，然后选择&#x200B;**[!UICONTROL 删除]**。

![突出显示[!UICONTROL 删除]选项的受众菜单。](../images/ui/delete-composition.png)

将显示成功删除的确认，并返回到&#x200B;**[!UICONTROL 合成]**&#x200B;选项卡。

对所有合成内容重复上述步骤。 这将从受众清单中删除所有受众。 删除所有受众后，您可以继续重置沙盒。

### 重置沙盒

重置生产或开发沙盒会删除与该沙盒关联的所有资源（架构、数据集等），同时保持沙盒的名称和关联的权限。 对于有权访问此“清理”沙盒的用户，将继续以相同的名称提供该沙盒。

从沙盒列表中选择要重置的沙盒。 在出现的右侧导航面板中，选择&#x200B;**[!UICONTROL 沙盒重置]**。

![重置](../images/ui/reset.png)

将出现一个对话框，提示您确认您的选择。 选择&#x200B;**[!UICONTROL 继续]**&#x200B;以继续。

![重置警告](../images/ui/reset-warning.png)

在最终确认窗口中，在对话框中输入沙盒的名称，然后选择&#x200B;**[!UICONTROL 重置]**。

![重置确认](../images/ui/reset-confirm.png)

## 删除沙盒

>[!WARNING]
>
>您无法删除默认的生产沙盒。 但是，在出现警告消息后，可以删除任何用于与[!DNL Audience Manager]或[!DNL Audience Core Service]进行双向区段共享的用户创建的生产沙盒。

删除生产或开发沙盒将永久删除与该沙盒关联的所有资源，包括权限。

从沙盒列表中选择要删除的沙盒。 在出现的右侧导航面板中，选择&#x200B;**[!UICONTROL 删除]**。

![删除](../images/ui/delete.png)

将出现一个对话框，提示您确认您的选择。 选择&#x200B;**[!UICONTROL 继续]**&#x200B;以继续。

![删除警告](../images/ui/delete-warning.png)

在最终确认窗口中，在对话框中输入沙盒的名称，然后选择&#x200B;**[!UICONTROL 继续]**。

![delete-confirm](../images/ui/delete-confirm.png)

## 后续步骤

本文档演示如何在Experience PlatformUI中管理沙盒。 有关如何使用沙盒API管理沙盒的信息，请参阅[沙盒开发人员指南](../api/getting-started.md)。
