---
title: 云存储目标工作流程
seo-title: 云存储目标工作流程
description: 连接到云存储位置的说明
seo-description: 连接到云存储位置的说明
translation-type: tm+mt
source-git-commit: 225f18bd0d092bdae7b4cc99c278e850be9cfd56

---


# 创建云存储目标的工作流程

## 概述

本页介绍如何连接到Adobe实时客户数据平台中的云存储位置。

1. 在“ **[!UICONTROL 连接”>“目标]**”中，选择您的首选云存储目标，然后选择 **[!UICONTROL Connect目标]**。

   ![连接到云存储目标](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. 在身份验证 **步骤中** ，如果您之前已设置到云存储目标的连接，请选择现有帐户 **** ，然后选择您的现有连接。 或者，您也可以选择 **[!UICONTROL 新帐户]** ，以设置到云存储目标的新连接。 填写帐户身份验证凭据，然后选择 **[!UICONTROL 连接到目标]**。

   >[!NOTE]
   >
   >Adobe实时CDP支持身份验证过程中的凭据验证，如果您向云存储位置输入了错误的凭据，则会显示一条错误消息。 这可确保您不会使用错误的凭据完成工作流。

   ![连接到云存储目标——身份验证步骤](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. 在设 **[!UICONTROL 置步骤中]** ，为激活流程输入名称和目标，然后在将要传送文件的云存储目标中插入 ************ Folder路径。 在您 **[!UICONTROL 填写上述字段后]** ，选择创建目标。

   ![连接到云存储目标——身份验证步骤](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. 您的目标现已创建。 如果您希望 **[!UICONTROL 稍后激活区段]** ，则可以选择保存并退出 **** ，也可以选择下一步以继续工作流，然后选择要激活的区段。 无论哪种情况，在工作流的其 [余部分](#activate-segments)，请参阅激活区段。

## 激活区段 {#activate-segments}

有关 [细分激活工作流的信息，请参阅将配置文件和细分激活到目标](/help/rtcdp/destinations/activate-destinations.md) 。