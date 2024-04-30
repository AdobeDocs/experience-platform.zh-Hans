---
title: 扩展的激活帐户管理
description: 了解如何对扩展的激活帐户执行管理任务，如监控许可证使用和分配正确的权限。
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# 帐户管理

要从Audience Manager摄取受众并将它们激活到社交和广告目标，您必须首先创建一个扩展的激活用户帐户，并将该帐户分配给正确的权限角色。

本页介绍如何在Admin Console中创建用户帐户，并为扩展激活分配正确的权限。

## 创建用户帐户 {#create-users}

在可以使用之前 [!DNL Audience Manager Expanded Activation]中，您必须创建一个用户帐户。

创建用户帐户 [!DNL Expanded Activation]，按照从管理用户的说明 [Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/manage-users-individually.html) 文档。

## 将用户添加到权限角色 {#permissions}

创建用户帐户后，必须将其添加到 [!DNL Expanded Activation] 权限角色，在 [!DNL Expanded Activation] 用户界面。

转到 **[!UICONTROL 管理]** -> **[!UICONTROL 权限]** -> **[!UICONTROL 角色]**，然后选择 **[!UICONTROL 扩展的激活默认角色]**.

![扩展了显示“角色”页面的“激活”用户界面图像。](assets/expanded-activation-role.png)

转到 **[!UICONTROL 用户]** 选项卡并选择 **[!UICONTROL 添加用户]**.

![扩展了显示“用户”页面的“激活”用户界面图像。](assets/add-users.png)

从可用列表中选择新创建的用户，然后选择 **[!UICONTROL 保存]**.

![扩展了显示“添加用户”页的“激活”用户界面图像。](assets/add-user.png)

现在将创建用户帐户并为其分配正确的角色。 现在可以访问 **[!UICONTROL 扩展的激活]** 用户界面。

## 监测许可证使用情况 {#license-usage}

您的 [!DNL Audience Manager Expanded Activation] 合同指定您可以摄取到帐户的经过哈希处理的电子邮件的最大数量。

您可以通过以下网站查找此信息： **[!UICONTROL 管理]** -> **[!UICONTROL 许可证使用情况]** 页面。

![扩展了显示许可证使用屏幕的激活用户界面图像。](assets/license-usage.png)

在此页上，您可以找到以下信息：

* **[!UICONTROL 产品]**：您获得许可的Adobe产品。 这将永远是 **[!UICONTROL Audience Manager扩展激活]**.
* **[!UICONTROL 主要量度]**：要跟踪以便使用的量度的名称。 这将永远是 **[!UICONTROL 可寻址受众]**.
* **[!UICONTROL 许可证金额]**：您有权摄取的经过哈希处理的电子邮件的最大数量。

  >[!TIP]
  >
  >您通过 [Audience Manager源连接器](../sources/connectors/adobe-applications/audience-manager.md). 请参阅相关文档 [如何激活受众](activate-audiences.md) 以了解更多详细信息。

* **[!UICONTROL 使用情况]**：您摄取的经过哈希处理的电子邮件数。
* **[!UICONTROL 使用率%]**：您已使用的许可证数量百分比。

要了解有关Experience Platform中许可证使用的更多信息，请参见 [许可证使用文档](../dashboards/guides/license-usage.md).

## 后续步骤 {#next-steps}

现在，您已配置至少一个用户帐户以正确访问扩展激活，您可以开始使用该帐户 [激活受众](activate-audiences.md).
