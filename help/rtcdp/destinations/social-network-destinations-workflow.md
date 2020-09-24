---
keywords: Facebook;facebook;Social network;Social Network;social network authentication;Social network authentication
title: 社交网络目标工作流
type: Tutorial
seo-title: 社交网络目标工作流
description: 连接到社交网络广告帐户的说明
seo-description: 连接到社交网络广告帐户的说明
translation-type: tm+mt
source-git-commit: 120ba866cf6e6509c51a29cb07e73550006fe5eb
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# 社交网络目标身份验证工作流程 {#social-network-destinations-workflow}

## 创建社交网络目标的工作流

本教程以 [!DNL Facebook] 一个示例为例，但Adobe实时客户数据平台中的工作流对于所有社交网络目标将保持不变，然后再添加到产品中。

1. 在“ **[!UICONTROL 目标]** ”> **[!UICONTROL “目录]**”中，滚 **[!UICONTROL 动到Social]** 类别。 选择首选社交网络目标，然后选择 **[!UICONTROL 配置]**。

   ![连接到社交网络目标](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

   >[!NOTE]
   >
   >如果与此目标的连接已存在，您可以在目标卡 **[!UICONTROL 上看到]** “激活”按钮。 有关激活和配置之 **[!UICONTROL 间差异]** 的详 **[!UICONTROL 细信]**&#x200B;息，请参 [阅目标工](/help/rtcdp/destinations/destinations-workspace.md#catalog) 作区文档的“目录”部分。

2. 在“身 **份验证** ”步骤中，如果您之前已设置到社交网络目标的连接，请选择“现 **[!UICONTROL 有帐户]** ”并选择现有连接。 或者，您也可以选 **[!UICONTROL 择“新建帐户]** ”来设置到社交网络目标的新连接。 选 **[!UICONTROL 择连接到目标]** ，此操作将带您进入选定的社交网络目标，以登录并将Adobe Experience Cloud连接到您的社交网络广告帐户。

   >[!NOTE]
   >
   >Adobe实时CDP支持身份验证过程中的凭据验证，如果您向社交网络帐户ID输入了不正确的凭据，则会显示一条错误消息。 这可确保您没有使用错误的凭据完成工作流。

   ![连接到社交网络目标——身份验证步骤](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. 确认您的凭据并将Adobe Experience Cloud连接到您的社交网络后，您可以选 **[!UICONTROL 择]** “下一步”以继续 **[!UICONTROL 设置]** 步骤。

   ![已确认凭据](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. 在设 **[!UICONTROL 置步]** 骤中，为激活流 **[!UICONTROL 输入名]** 称和说明 **[!UICONTROL ，然后填写社交网]****** 络广告帐户的帐户ID。 <br> 此外，在此步骤中，您还可以选 **[!UICONTROL 择应用于此目标]** 的任何Marketing用例。 市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 有关各个Adobe定义的营销用例的信息，请参阅数据 [使用策略概述](/help/data-governance/policies/overview.md#core-actions)。 <br> 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

   >[!IMPORTANT]
   >
   > * 默认 *情况下，对于社交网络目标* ,“单一身份个性化”营销用例处于选中状态，无法删除。
   > * 针对目 [!DNL Facebook] 的地。 **[!UICONTROL 帐户ID]** 是您的 [!DNL Facebook Ad Account ID]。 您可以在中找到此ID [!DNL Facebook Ads Manager]。 在ID前加上 `act_` 如下前缀：


   ![连接到社交网络目标——设置步骤](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. 您的目标现在已创建。 如果要稍后 **[!UICONTROL 激活区段]** ，则可以选择保存并退出 **[!UICONTROL ，也可以选择下一步继续工作]** 流，然后选择要激活的区段。 在任一情况下，请参阅下一 [节，将区段激活到社交网](#activate-segments)络，以了解工作流的其余部分。

## 将细分激活到社交网络 {#activate-segments}

有关如何将区段激活到社交网络的说明，请参 [阅将数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。