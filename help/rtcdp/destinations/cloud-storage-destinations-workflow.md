---
title: 云存储目标工作流
seo-title: 云存储目标工作流
description: 连接到云存储位置的说明
seo-description: 连接到云存储位置的说明
translation-type: tm+mt
source-git-commit: 37c51435ce8330dbd61857bda408df03ff21a491
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# 创建云存储目标的工作流

## 概述

本页介绍如何连接到Adobe实时存储平台中的云数据位置。

1. 在“ **[!UICONTROL 连接”>“目标]**”中，选择首选云存储目标，然后选择 **[!UICONTROL Connect目标]**。

   ![连接到云存储目标](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. 在身份 **[!UICONTROL 验证]** 步骤中，如果您之前已设置到云存储目标的连接，请选择现 **[!UICONTROL 有帐户]** ，然后选择现有连接。 或者，您也可以选 **[!UICONTROL 择新帐户]** ，以设置到云存储目标的新连接。 填写帐户身份验证凭据，然后选 **[!UICONTROL 择连接到目标]**。 <br> 请参 [阅Amazon](/help/rtcdp/destinations/amazon-s3-destination.md) S3 [目标](/help/rtcdp/destinations/amazon-kinesis-destination.md) 、Amazon Kinesis目标、Azure [事件目标和SS目标，以了](/help/rtcdp/destinations/azure-event-hubs-destination.md)[](/help/rtcdp/destinations/sftp-destination.md)**** 解在FTP步骤中输入的凭据的具体信息。

   >[!NOTE]
   >
   >Adobe实时CDP支持身份验证过程中的凭据验证，如果您向云存储位置输入了不正确的凭据，则会显示错误消息。 这可确保您没有使用错误的凭据完成工作流。

   ![连接到云存储目标——身份验证步骤](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. 在设 **[!UICONTROL 置步]** 骤中，输入 **[!UICONTROL 激活流]** 的名 **[!UICONTROL 称和]** 说明。 <br>
对于Amazon S3目标，在云存储 **[!UICONTROL 目标中]** ，插 **[!UICONTROL 入存储段名]** 称和文件夹路径，文件将从中传送。 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

   ![连接到Amazon S3云存储目标——身份验证步骤](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   对于SFTP目标，插入 **[!UICONTROL 文件传送]** “文件夹”路径。

   ![连接到SFTP云存储目标——身份验证步骤](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

4. 您的目标现在已创建。 如果要稍后 **[!UICONTROL 激活区段]** ，则可以选择保存并退出 **[!UICONTROL ，也可以选择下一步以继]** 续工作流，然后选择要激活的区段。 无论哪种情况，在导出数据的工 [作流程的其余](#activate-segments)，请参阅下一节激活区段。

## 激活区段 {#activate-segments}

有关 [区段用户档案工作流的信息](/help/rtcdp/destinations/activate-destinations.md) ，请参阅将激活和区段激活到目标。