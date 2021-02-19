---
keywords: Facebook;Facebook；社交网络；社交网络；社交网络；社交网络身份验证；社交网络身份验证
title: 创建社交网络目标
type: Tutorial
description: 了解如何连接到Adobe Experience Platform中的社交网络广告帐户。
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---


# 创建社交网络目标{#social-network-destinations-workflow}

本教程以[!DNL Facebook]为例，但Adobe Experience Platform中的工作流对于所有社交网络目标将保持不变，然后再添加到产品中。

在&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**&#x200B;中，滚动到&#x200B;**[!UICONTROL Social]**&#x200B;类别。 选择首选社交网络目标，然后选择&#x200B;**[!UICONTROL 配置]**。

![连接到社交网络目标](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

在&#x200B;**身份验证**&#x200B;步骤中，如果您之前已设置到社交网络目标的连接，请选择&#x200B;**[!UICONTROL 现有帐户]**&#x200B;并选择现有连接。 或者，您可以选择&#x200B;**[!UICONTROL 新建帐户]**&#x200B;来设置到社交网络目标的新连接。 选择&#x200B;**[!UICONTROL 连接到目标]**，此操作将带您到选定的社交网络目标以登录，并将Adobe Experience Cloud连接到您的社交网络广告帐户。

>[!NOTE]
>
>平台支持身份验证过程中的凭据验证，如果您向社交网络帐户ID输入了不正确的凭据，则会显示错误消息。 这可确保您没有使用不正确的凭据完成工作流。

![连接到社交网络目标 — 身份验证步骤](../../assets/catalog/social/workflow/pre-connect.png)

确认您的凭据并将Adobe Experience Cloud连接到您的社交网络后，您可以选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行&#x200B;**[!UICONTROL 设置]**&#x200B;步骤。

![已确认凭据](../../assets/catalog/social/workflow/post-connect.png)

在&#x200B;**[!UICONTROL 设置]**&#x200B;步骤中，输入激活流的[!UICONTROL 名称]和[!UICONTROL 说明]，并填写社交网络和帐户的[!UICONTROL 帐户ID]。

此外，在此步骤中，您还可以选择应用于此目标的任何&#x200B;**[!UICONTROL 营销操作]**。 营销活动指示要将数据导出到目标的目的。 您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

在填写上面的字段后，选择&#x200B;**[!UICONTROL 创建目标]**。

>[!IMPORTANT]
>
> * 对于[!DNL Facebook]目标。 **[!UICONTROL 帐]** 户ID是您 [!DNL Facebook Ad Account ID]的。您可以在[!DNL Facebook Ads Manager]中找到此ID。 将ID前缀为`act_`，如下所示：


![连接到社交网络目标 — 设置步骤](../../assets/catalog/social/workflow/setup.png)

您的目标现在已创建。 如果您希望稍后激活区段，可以选择&#x200B;**[!UICONTROL 保存并退出]**，也可以选择&#x200B;**[!UICONTROL 下一步]**&#x200B;继续工作流并选择要激活的区段。 在任一情况下，请参阅工作流的下一节[将区段激活到社交网络](#activate-segments)。

## 将区段激活到社交网络{#activate-segments}

有关如何将区段激活到社交网络的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。