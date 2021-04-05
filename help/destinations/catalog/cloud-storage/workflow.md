---
keywords: 云存储目标；云存储
title: 创建云存储目标
type: 教程
description: 连接到云存储位置的说明
seo-description: 连接到云存储位置的说明
exl-id: 58003c1e-2f70-4e28-8a38-3be00da7cc3c
translation-type: tm+mt
source-git-commit: ecda1f1c4a2829124aedaae2395a74e54929c7ad
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# 创建云存储目标

## 概述 {#overview}

本页介绍如何连接到Adobe Experience Platform中的云存储位置。

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，选择首选云存储目标，然后选择&#x200B;**[!UICONTROL Configure]**。

![连接到云存储目标](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[目录](../../ui/destinations-workspace.md#catalog)部分。

## 帐户步骤{#account}

在&#x200B;**[!UICONTROL Account]**&#x200B;步骤中，如果您之前已设置到云存储目标的连接，请选择&#x200B;**[!UICONTROL Existing Account]**&#x200B;并选择现有连接。 或者，您也可以选择&#x200B;**[!UICONTROL New Account]**&#x200B;来设置到云存储目标的新连接。 填写帐户身份验证凭据并选择&#x200B;**[!UICONTROL Connect to destination]**。 或者，您可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写入为[!DNL Base64]编码字符串。

有关在&#x200B;**身份验证**&#x200B;步骤中输入凭据的具体信息，请参阅[Amazon S3](./amazon-s3.md)目标、[[!DNL Amazon Kinesis]](./amazon-kinesis.md)目标、[[!DNL Azure Event Hubs]](./azure-event-hubs.md)目标和[SFTP](./sftp.md)目标。

>[!NOTE]
>
>平台支持身份验证过程中的凭据验证，如果您向云存储位置输入了不正确的凭据，则会显示错误消息。 这可确保您没有使用不正确的凭据完成工作流。

![连接到云存储目标 — 帐户步骤](../../assets/catalog/cloud-storage/workflow/destination-account.png)

## 身份验证步骤{#authentication}

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步骤中，输入&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Description]**&#x200B;作为激活流。

在此步骤中，您还可以选择应用于此目标的任何&#x200B;**[!UICONTROL Marketing action]**。 营销活动指示要将数据导出到目标的目的。 您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

对于Amazon S3目标，请将&#x200B;**[!UICONTROL Bucket name]**&#x200B;和&#x200B;**[!UICONTROL Folder path]**&#x200B;插入云存储目标，文件将在该目标中传送。 在填写上面的字段后，选择&#x200B;**[!UICONTROL Create Destination]**。

![连接到Amazon S3云存储目标 — 身份验证步骤](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

对于SFTP目标，插入将在其中传送文件的&#x200B;**[!UICONTROL Folder path]**。 在填写上面的字段后，选择&#x200B;**[!UICONTROL Create Destination]**。

![连接到SFTP云存储目标 — 身份验证步骤](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

对于[!DNL Amazon Kinesis]目标，请在[!DNL Amazon Kinesis]帐户中提供现有数据流的名称。 平台会将数据导出到此流。 在填写上面的字段后，选择&#x200B;**[!UICONTROL Create Destination]**。

![连接到Kinesis云存储目标 — 身份验证步骤](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

对于[!DNL Azure Event Hubs]目标，请在[!DNL Amazon Event Hubs]帐户中提供现有数据流的名称。 平台会将数据导出到此流。 在填写上面的字段后，选择&#x200B;**[!UICONTROL Create Destination]**。

![连接到事件中心云存储目标 — 身份验证步骤](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

您的目标现在已创建。 如果您希望稍后激活区段，则可以选择&#x200B;**[!UICONTROL Save & Exit]**，也可以选择&#x200B;**[!UICONTROL Next]**&#x200B;继续工作流，然后选择要激活的区段。 阅读[激活区段](#activate-segments)一节，了解导出数据的工作流程的其余部分。

## 使用宏在存储位置{#use-macros}中创建文件夹

>[!NOTE]
>
> 本节介绍的功能目前仅适用于[Amazon S3](./amazon-s3.md)目标。

要在存储位置为每个区段文件创建自定义文件夹，可以在文件夹路径输入字段中使用宏。 在输入字段的末尾插入宏，如下所示。

![如何使用宏在您的存储中创建文件夹](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

以下示例引用了ID为`25768be6-ebd5-45cc-8913-12fb3f348615`的示例段`Luxury Audience`。

**宏1:`%SEGMENT_NAME%`**

输入：`acme/campaigns/2021/%SEGMENT_NAME%`
您的存储位置中的文件夹路径：`acme/campaigns/2021/Luxury Audience`

**宏2:`%SEGMENT_ID%`**

输入：`acme/campaigns/2021/%SEGMENT_ID%`
您的存储位置中的文件夹路径：`acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**宏3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

输入：`acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
您的存储位置中的文件夹路径：`acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`



## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md)。
