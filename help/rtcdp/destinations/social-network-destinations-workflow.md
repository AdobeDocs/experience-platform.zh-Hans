---
title: 社交网络目标工作流
seo-title: 社交网络目标工作流
description: 连接到社交网络和帐户的说明
seo-description: 连接到社交网络和帐户的说明
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# （测试版）社交网络目标身份验证工作流程 {#social-network-destinations-workflow}


>[!IMPORTANT]
>
>在Adobe Real-time CDP中创建社交网络目标的工作流程目前处于测试阶段，并且并非所有用户都能使用。 文档和功能可能会发生变化。

## 创建云存储目标的工作流

本教程以Facebook为例，但Adobe实时客户数据平台中的工作流程对于所有社交网络目标将保持不变，然后再添加到产品中。

1. 在 **[!UICONTROL Connections > Destinations]**&#x200B;中，滚动到 **[!UICONTROL Social]** 类别。 选择首选社交网络目标，然后选择 **[!UICONTROL Connect destination]**。

   ![连接到社交网络目标](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. 在“身 **份验证** ”步骤中，如果您之前已设置到社交网络目标的连接，请选择并 **[!UICONTROL Existing Account]** 选择您的现有连接。 或者，您也可以选 **[!UICONTROL New Account]** 择设置到社交网络目标的新连接。 选择 **[!UICONTROL Connect to destination]** 此选项后，您将转到选定的社交网络目标，以登录并将Adobe Experience Cloud连接到您的社交网络广告帐户。

   >[!NOTE]
   >
   >Adobe实时CDP支持身份验证过程中的凭据验证，如果您向社交网络帐户ID输入了错误的凭据，则会显示错误消息。 这可确保您不会使用错误的凭据完成工作流。

   ![连接到社交网络目标——身份验证步骤](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. 确认您的凭据并将Adobe Experience Cloud连接到您的社交网络后，您可以选择继 **[!UICONTROL Next]** 续执行该步 **[!UICONTROL Setup]** 骤。

   ![已确认凭据](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. 在该步 **[!UICONTROL Setup]** 骤中，为您的 **[!UICONTROL Name]** 激活流输 **[!UICONTROL Description]** 入和一个，并填写您的社交网络 **[!UICONTROL Account ID]** 广告帐户。 在您 **[!UICONTROL Create Destination]** 填写上面的字段后选择。

   >[!IMPORTANT]
   >
   >适用于Facebook目标。 **[!UICONTROL Account ID]** 是您的Facebook广告帐户ID。 您可以在Facebook广告管理器中找到此ID。 在ID前加 `act_` 上如下：

   ![连接到社交网络目标——设置步骤](/help/rtcdp/destinations/assets/social-network-step.png)

5. 您的目标现已创建。 您可以选择 **[!UICONTROL Save & Exit]** 是稍后激活区段，还是选择继 **[!UICONTROL Next]** 续工作流并选择要激活的区段。 在任一情况下，请参阅下一节，将 [区段激活到社交网络](#activate-segments)，以了解工作流的其余部分。

## 将细分激活到社交网络 {#activate-segments}

有关如何将区段激活到社交网络的说明，请参阅将 [数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。