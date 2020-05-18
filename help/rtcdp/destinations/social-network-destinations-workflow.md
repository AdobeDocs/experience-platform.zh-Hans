---
title: 社交网络目标工作流
seo-title: 社交网络目标工作流
description: 连接到社交网络广告帐户的说明
seo-description: 连接到社交网络广告帐户的说明
translation-type: tm+mt
source-git-commit: ab53e2efffed536e8028beabd64aee843d1eeee8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# 社交网络目标身份验证工作流程 {#social-network-destinations-workflow}

## 创建社交网络目标的工作流

本教程以Facebook为例，但Adobe实时客户数据平台中的工作流对于所有社交网络目标将保持不变，然后再添加到产品中。

1. 在“ **[!UICONTROL 目标”>]**“目录”中，滚 **[!UICONTROL 动到Social]** 类别。 选择首选社交网络目标，然后选择 **[!UICONTROL Connect目标]**。

   ![连接到社交网络目标](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. 在“身 **份验证** ”步骤中，如果您之前已设置到社交网络目标的连接，请选择“现 **[!UICONTROL 有帐户]** ”并选择现有连接。 或者，您也可以选 **[!UICONTROL 择“新建帐户]** ”来设置到社交网络目标的新连接。 选 **[!UICONTROL 择连接到目]** 标，此操作将带您进入选定的社交网络目标，以登录Adobe Experience Cloud并将其连接到您的社交网络广告帐户。

   >[!NOTE]
   >
   >Adobe实时CDP支持身份验证过程中的凭据验证，如果您向社交网络帐户ID输入了不正确的凭据，则会显示错误消息。 这可确保您没有使用错误的凭据完成工作流。

   ![连接到社交网络目标——身份验证步骤](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. 确认您的凭据并将Adobe Experience Cloud连接到您的社交网络后，您可以选 **[!UICONTROL 择]** “下一步”以继 **[!UICONTROL 续设置]** 。

   ![已确认凭据](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. 在设 **[!UICONTROL 置步]** 骤中，为激活流 **[!UICONTROL 输入名]** 称和说明 **[!UICONTROL ，然后填写社交网]****** 络广告帐户的帐户ID。 选择应应用于此目标的任何市场营销用例。 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

   >[!IMPORTANT]
   >
   > 适用于Facebook目标。 **[!UICONTROL 帐户ID]** 是您的Facebook广告帐户ID。 您可以在Facebook广告管理器中找到此ID。 在ID前加上 `act_` 如下前缀：

   ![连接到社交网络目标——设置步骤](/help/rtcdp/destinations/assets/social-network-setup-step.png)

5. 您的目标现在已创建。 如果要稍后 **[!UICONTROL 激活区段]** ，则可以选择保存并退出 **[!UICONTROL ，也可以选择下一步以继]** 续工作流，然后选择要激活的区段。 在任一情况下，请参阅下一 [节，将区段激活到社交网](#activate-segments)络，以了解工作流的其余部分。

## 将细分激活到社交网络 {#activate-segments}

有关如何将区段激活到社交网络的说明，请参 [阅将数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。


<!--

// update IMPORTANT note in step 4 after marketing use cases are released for RTCDP

    >[!IMPORTANT]
    >
    > * The *Single Identity Personalization* marketing use case is selected by default for social network destinations and cannot be removed. 
    > * For Facebook destinations. **[!UICONTROL Account ID]** is your Facebook Ad Account ID. You can find this ID in the Facebook Ads Manager. Prefix the ID with `act_` as shown below: 

    ![Connect to social network destination - setup step](/help/rtcdp/destinations/assets/social-networks-setup-step.png)