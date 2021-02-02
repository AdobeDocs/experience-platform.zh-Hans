---
keywords: 云存储目标；云存储
title: 云存储目标工作流
seo-title: 云存储目标工作流
type: Tutorial
description: 连接到云存储位置的说明
seo-description: 连接到云存储位置的说明
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# 创建云存储目标的工作流

## 概述

本页介绍如何连接到Adobe Experience Platform的云存储位置。

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择首选云存储目标，然后选择&#x200B;**[!UICONTROL 配置]**。

![连接到云存储目标](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

在&#x200B;**[!UICONTROL 身份验证]**&#x200B;步骤中，如果您之前已设置到云存储目标的连接，请选择&#x200B;**[!UICONTROL 现有帐户]**&#x200B;并选择现有连接。 或者，您也可以选择&#x200B;**[!UICONTROL 新帐户]**&#x200B;来设置到云存储目标的新连接。 填写帐户身份验证凭据，然后选择&#x200B;**[!UICONTROL 连接到目标]**。 或者，您可以附加RSA格式的公钥，以向导出的文件添加加密。 请注意，此公钥&#x200B;**必须**&#x200B;写成Base64编码字符串。

有关在&#x200B;**身份验证**&#x200B;步骤中输入凭据的具体信息，请参见[AmazonS3](./amazon-s3.md)目标、[[!DNL Amazon Kinesis]](./amazon-kinesis.md)目标、[[!DNL Azure Event Hubs]](./azure-event-hubs.md)目标和[SFTP](./sftp.md)目标。

>[!NOTE]
>
>平台支持身份验证过程中的凭据验证，如果您向云存储位置输入了不正确的凭据，则会显示错误消息。 这可确保您没有使用错误的凭据完成工作流。

![连接到云存储目标——身份验证步骤](../../assets/catalog/cloud-storage/workflow/destination-account.png)

在&#x200B;**[!UICONTROL 设置]**&#x200B;步骤中，为激活流输入&#x200B;**[!UICONTROL 名称]**&#x200B;和&#x200B;**[!UICONTROL 说明]**。

此外，在此步骤中，您还可以选择应用于此目标的任何&#x200B;**[!UICONTROL 营销用例]**。 市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关市场营销用例的详细信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

对于AmazonS3目标，在将要传送文件的云存储目标中插入&#x200B;**[!UICONTROL 存储段名称]**&#x200B;和&#x200B;**[!UICONTROL 文件夹路径]**。 在填写上述字段后，选择&#x200B;**[!UICONTROL 创建目标]**。

![连接到AmazonS3云存储目标——身份验证步骤](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

对于SFTP目标，插入&#x200B;**[!UICONTROL 文件夹路径]**，将在其中传送文件。 在填写上述字段后，选择&#x200B;**[!UICONTROL 创建目标]**。

![连接到SFTP云存储目标——身份验证步骤](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

对于[!DNL Amazon Kinesis]目标，请在[!DNL Amazon Kinesis]帐户中提供现有数据流的名称。 平台会将数据导出到此流。 在填写上述字段后，选择&#x200B;**[!UICONTROL 创建目标]**。

![连接到Kinesis云存储目标——身份验证步骤](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

对于[!DNL Azure Event Hubs]目标，请在[!DNL Amazon Event Hubs]帐户中提供现有数据流的名称。 平台会将数据导出到此流。 在填写上述字段后，选择&#x200B;**[!UICONTROL 创建目标]**。

![连接到事件中心云存储目标——身份验证步骤](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

您的目标现在已创建。 如果您希望稍后激活区段，可以选择&#x200B;**[!UICONTROL 保存并退出]**，也可以选择&#x200B;**[!UICONTROL 下一步]**&#x200B;继续工作流并选择要激活的区段。 在任一情况下，请参阅用于导出数据的工作流的下一节[激活区段](#activate-segments)。

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md)。