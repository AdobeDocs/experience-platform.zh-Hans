---
keywords: cloud storage destination;cloud storage
title: 云存储目标工作流
seo-title: 云存储目标工作流
type: Tutorial
description: 连接到云存储位置的说明
seo-description: 连接到云存储位置的说明
translation-type: tm+mt
source-git-commit: 24c8dd0f01d7ea14b2fa5827722e797bd209f50c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# 创建云存储目标的工作流

## 概述

本页介绍如何连接到实时存储平台中的云数据位置。

在“ **[!UICONTROL 连接]** ”>“ **[!UICONTROL 目标]**”中，选择首选云存储目标，然后选择 **[!UICONTROL 配置]**。

![连接到云存储目标](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡 **[!UICONTROL 上看到]** “激活”按钮。 有关激活和配置之 **[!UICONTROL 间差异]** 的详 **[!UICONTROL 细信]**&#x200B;息，请参 [阅目标工](../../ui/destinations-workspace.md#catalog) 作区文档的“目录”部分。

在身份 **[!UICONTROL 验证]** 步骤中，如果您之前已设置到云存储目标的连接，请选择现 **[!UICONTROL 有帐户]** ，然后选择现有连接。 或者，您也可以选 **[!UICONTROL 择新帐户]** ，以设置到云存储目标的新连接。 填写帐户身份验证凭据，然后选 **[!UICONTROL 择连接到目标]**。 或者，您可以附加RSA格式的公钥，以向导出的文件添加加密。 请注意，此公钥 **必须** 作为Base64编码字符串写入。

请参 [阅AmazonS](./amazon-s3.md) 3目标 [[!DNL Amazon Kinesis]](./amazon-kinesis.md) 、目 [[!DNL Azure Event Hubs]](./azure-event-hubs.md) 标、目标和SFTP目标 [，了解身份验证步骤中凭据](./sftp.md) 输入的 **** 具体信息。

>[!NOTE]
>
>实时CDP支持身份验证过程中的凭据验证，如果您向云存储位置输入了不正确的凭据，则会显示错误消息。 这可确保您没有使用错误的凭据完成工作流。

![连接到云存储目标——身份验证步骤](../../assets/catalog/cloud-storage/workflow/destination-account.png)

在设 **[!UICONTROL 置步]** 骤中，输入 **[!UICONTROL 激活流]** 的名 **[!UICONTROL 称和]** 说明。

此外，在此步骤中，您还可以选 **[!UICONTROL 择应用于此目标]** 的任何Marketing用例。 市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](../../../rtcdp/privacy/data-governance-overview.md#destinations) 。 有关各个Adobe定义的营销用例的信息，请参阅数据 [使用策略概述](../../../data-governance/policies/overview.md#core-actions)。

对于AmazonS3目标，请在云 **[!UICONTROL 存储目]** 标中插入存储段 **** 名称和文件夹路径，文件将从中传送。 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

![连接到AmazonS3云存储目标——身份验证步骤](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

对于SFTP目标，插入 **[!UICONTROL 文件传送]** “文件夹”路径。 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

![连接到SFTP云存储目标——身份验证步骤](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

对于 [!DNL Amazon Kinesis] 目标，请提供帐户中现有数据流的 [!DNL Amazon Kinesis] 名称。 实时CDP会将数据导出到此流。 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

![连接到Kinesis云存储目标——身份验证步骤](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

对于 [!DNL Azure Event Hubs] 目标，请提供帐户中现有数据流的 [!DNL Amazon Event Hubs] 名称。 实时CDP会将数据导出到此流。 在 **[!UICONTROL 填写上述字]** 段后，选择创建目标。

![连接到事件中心云存储目标——身份验证步骤](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

您的目标现在已创建。 如果要稍后 **[!UICONTROL 激活区段]** ，则可以选择保存并退出 **[!UICONTROL ，也可以选择下一步继续工作]** 流，然后选择要激活的区段。 无论哪种情况，在导出数据的工 [作流程的其余](#activate-segments)，请参阅下一节激活区段。

## 激活区段 {#activate-segments}

有关 [区段用户档案工作流的信息](../../ui/activate-destinations.md) ，请参阅将激活和区段激活到目标。