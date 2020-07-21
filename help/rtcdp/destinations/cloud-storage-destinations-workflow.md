---
title: 云存储目标工作流
seo-title: 云存储目标工作流
description: 连接到云存储位置的说明
seo-description: 连接到云存储位置的说明
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# 创建云存储目标的工作流

## 概述

本页介绍如何连接到Adobe实时存储平台中的云数据位置。

1. 在“ **[!UICONTROL 连接”>“目标]**”中，选择首选云存储目标，然后选择 **[!UICONTROL Connect目标]**。

   ![连接到云存储目标](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. 在身份 **[!UICONTROL 验证]** 步骤中，如果您之前已设置到云存储目标的连接，请选择现 **[!UICONTROL 有帐户]** ，然后选择现有连接。 或者，您也可以选 **[!UICONTROL 择新帐户]** ，以设置到云存储目标的新连接。 填写帐户身份验证凭据，然后选 **[!UICONTROL 择连接到目标]**。 <br> 请参 [阅Amazon](/help/rtcdp/destinations/amazon-s3-destination.md) S3目标 [!DNL Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) 、目 [!DNL Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) 标、目标和 [SFTP目标](/help/rtcdp/destinations/sftp-destination.md) ，了解AuthenticationStep中凭据输入 **** 的具体信息。

   >[!NOTE]
   >
   >Adobe实时CDP支持身份验证过程中的凭据验证，如果您向云存储位置输入了不正确的凭据，则会显示错误消息。 这可确保您没有使用错误的凭据完成工作流。

   ![连接到云存储目标——身份验证步骤](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. 在设 **[!UICONTROL 置步]** 骤中，输入 **[!UICONTROL 激活流]** 的名 **[!UICONTROL 称和]** 说明。 <br>
此外，在此步骤中，您还可以选 **[!UICONTROL 择应用于此目标]** 的任何Marketing用例。 市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 有关Adobe定义的个别营销用例的信息，请参阅数 [据使用策略概述](/help/data-governance/policies/overview.md#core-actions)。 <br>
对于Amazon S3目标，在云存储 **[!UICONTROL 目标中]** ，插 **[!UICONTROL 入存储段名]** 称和文件夹路径，文件将从中传送。 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

   ![连接到Amazon S3云存储目标——身份验证步骤](/help/rtcdp/destinations/assets/amazon-s3-setup-step.png)

   对于SFTP目标，插入 **[!UICONTROL 文件传送]** “文件夹”路径。 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

   ![连接到SFTP云存储目标——身份验证步骤](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

   对于 [!DNL Amazon Kinesis] 目标，请在帐户中提供现有数据流的 [!DNL Amazon Kinesis] 名称。 Adobe实时CDP会将数据导出到此流。 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

   ![连接到Kinesis云存储目标——身份验证步骤](/help/rtcdp/destinations/assets/kinesis-destinations-setup-step.png)

   对于 [!DNL Azure Event Hubs] 目标，请在帐户中提供现有数据流的 [!DNL Amazon Kinesis] 名称。 Adobe实时CDP会将数据导出到此流。 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

   ![连接到Kinesis云存储目标——身份验证步骤](/help/rtcdp/destinations/assets/eventhubs-destinations-setup-step.png)

4. 您的目标现在已创建。 如果要稍后 **[!UICONTROL 激活区段]** ，则可以选择保存并退出 **[!UICONTROL ，也可以选择下一步以继]** 续工作流，然后选择要激活的区段。 无论哪种情况，在导出数据的工 [作流程的其余](#activate-segments)，请参阅下一节激活区段。

## 激活区段 {#activate-segments}

有关 [区段用户档案工作流的信息](/help/rtcdp/destinations/activate-destinations.md) ，请参阅将激活和区段激活到目标。