---
keywords: 云存储目标；云存储
title: 云存储目标概述
description: Adobe Experience Platform可以将受众作为数据文件交付到Amazon S3、AWS Kinesis、Azure事件中心或SFTP云存储位置。
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 6%

---

# 云存储目标概述 {#cloud-storage-destinations}

## 概述 {#overview}

Adobe Experience Platform可以将受众作为数据文件交付到云存储位置。 这使您能够通过[!DNL Amazon S3]、[!DNL Azure Blob]、[!DNL Azure Data Lake Storage Gen2]、[!DNL Data Landing Zone]、[!DNL Google Cloud Storage]和SFTP的CSV文件将受众及其配置文件属性发送到您的内部系统。 对于[!DNL Amazon Kinesis]和[!DNL Azure Event Hubs]目标，数据将以[!DNL JSON]格式流式传输出Experience Platform。

![Adobe云存储目标](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## 支持的云存储目标 {#supported-destinations}

Adobe Experience Platform支持将数据导出到以下云存储目标：

* [Amazon Kinesis连接](amazon-kinesis.md)
* [Amazon S3连接](amazon-s3.md)
* [Azure Blob连接](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure事件中心连接](azure-event-hubs.md)
* [数据登陆区](data-landing-zone.md)
* [Google 云存储](google-cloud-storage.md)
* [SFTP连接](sftp.md)

## 连接到新的云存储目标 {#connect-destination}

要将受众发送到营销活动的云存储目标，Experience Platform必须首先连接到目标。 有关设置新目标的详细信息，请参阅[目标创建教程](../../ui/connect-destination.md)。


## 使用宏在存储位置创建一个文件夹 {#use-macros}

>[!NOTE]
>
> 此部分中描述的功能适用于所有云存储目标。 但是，[Amazon S3](amazon-s3.md)目标当前仅支持`%SEGMENT_ID%`和`%SEGMENT_NAME%`宏。

要在存储位置中为每个受众文件创建自定义文件夹，可以在文件夹路径输入字段中使用宏。 在输入字段的末尾插入宏，如下所示。

![如何使用宏在存储中创建文件夹](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

以下示例引用了ID为`25768be6-ebd5-45cc-8913-12fb3f348615`的示例受众`Luxury Audience`。

**宏1：`%SEGMENT_NAME%`**

输入： `acme/campaigns/2021/%SEGMENT_NAME%`
存储位置中的文件夹路径： `acme/campaigns/2021/Luxury Audience`

**宏2：`%SEGMENT_ID%`**

输入： `acme/campaigns/2021/%SEGMENT_ID%`
存储位置中的文件夹路径： `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**宏3：`%SEGMENT_NAME%/%SEGMENT_ID%`**

输入： `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
存储位置中的文件夹路径： `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

**其他宏**

与上面的示例类似，您可以使用其他宏在文件夹位置中创建自定义文件夹结构：

* `%DATETIME%`或`%TIMESTAMP%`以根据文件的导出时间添加自定义文件夹名称。 第一个宏的格式为`MMDDYYYY_HHMMSS`，第二个宏的格式为UNIX 10位数。
* `%DESTINATION_NAME%`添加基于目标数据流名称的自定义文件夹。

## 数据导出类型 {#export-type}

云存储目标支持以下导出类型：
* **基于配置文件的导出**。 这意味着您正在导出有关受众中个人的详细信息。 个性化时需要这些详细信息，它们可以包括属性、事件、受众成员资格等。
* **数据集导出**。 此功能允许您将整个数据集导出到云存储目标。 [参阅更多](/help/destinations/ui/export-datasets.md)关于该功能的信息。

## 后续步骤 {#next-steps}

选择想要使用的[支持的云目标](#supported-destinations)之一后，请阅读[连接到目标教程](/help/destinations/ui/connect-destination.md)，了解如何建立与目标之间的连接。 然后，阅读基于文件的目标的激活教程，了解如何开始[将](/help/destinations/ui/activate-batch-profile-destinations.md)数据导出到云存储目标。
