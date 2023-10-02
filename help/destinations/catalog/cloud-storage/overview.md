---
keywords: 云存储目标；云存储
title: 云存储目标概述
description: Adobe Experience Platform可以将受众作为数据文件交付到Amazon S3、AWS Kinesis、Azure事件中心或SFTP云存储位置。
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 8b8abea65ee0448594113ca77f75b84293646146
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 4%

---

# 云存储目标概述 {#cloud-storage-destinations}

## 概述 {#overview}

Adobe Experience Platform可以将受众作为数据文件交付到云存储位置。 这使您能够为通过CSV文件将受众及其配置文件属性发送到内部系统 [!DNL Amazon S3]， [!DNL Azure Blob]， [!DNL Azure Data Lake Storage Gen2]， [!DNL Data Landing Zone]， [!DNL Google Cloud Storage]和SFTP。 对象 [!DNL Amazon Kinesis] 和 [!DNL Azure Event Hubs] 目标，数据流式传输出Experience Platform [!DNL JSON] 格式。

![Adobe云存储目标](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## 支持的云存储目标 {#supported-destinations}

Adobe Experience Platform支持将数据导出到以下云存储目标：

* [Amazon Kinesis连接](amazon-kinesis.md)
* [Amazon S3连接](amazon-s3.md)
* [Azure Blob连接](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure事件中心连接](azure-event-hubs.md)
* [数据登陆区](data-landing-zone.md)
* [Google云存储](google-cloud-storage.md)
* [SFTP连接](sftp.md)

## 连接到新的云存储目标 {#connect-destination}

要将受众发送到营销活动的云存储目标，平台必须首先连接到目标。 请参阅 [目标创建教程](../../ui/connect-destination.md) 以了解有关设置新目标的详细信息。


## 使用宏在存储位置创建一个文件夹 {#use-macros}

>[!NOTE]
>
> 本节中介绍的功能当前适用于 [Amazon S3](amazon-s3.md) 仅限目标。

要在存储位置中为每个受众文件创建自定义文件夹，可以在文件夹路径输入字段中使用宏。 在输入字段的末尾插入宏，如下所示。

![如何使用宏在存储中创建文件夹](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

以下示例引用了一个示例受众 `Luxury Audience` 具有ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**宏1：`%SEGMENT_NAME%`**

输入： `acme/campaigns/2021/%SEGMENT_NAME%`
存储位置中的文件夹路径： `acme/campaigns/2021/Luxury Audience`

**宏2：`%SEGMENT_ID%`**

输入： `acme/campaigns/2021/%SEGMENT_ID%`
存储位置中的文件夹路径： `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**宏3：`%SEGMENT_NAME%/%SEGMENT_ID%`**

输入： `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
存储位置中的文件夹路径： `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## 数据导出类型 {#export-type}

云存储目标支持以下导出类型：
* **基于用户档案的导出**. 这意味着您正在导出有关受众中个人的详细信息。 个性化时需要这些详细信息，它们可以包括属性、事件、受众成员资格等。
* **数据集导出**. 此功能允许您将整个数据集导出到云存储目标。 [了解更多](/help/destinations/ui/export-datasets.md) 功能简介。

## 后续步骤 {#next-steps}

在选择 [支持的云目标](#supported-destinations) 如果您想使用，请阅读 [连接到目标教程](/help/destinations/ui/connect-destination.md) 以了解如何建立与目标的连接。 然后，请阅读基于文件的目标的激活教程，以了解如何开始 [导出](/help/destinations/ui/activate-batch-profile-destinations.md) 将数据发送到云存储目标。
