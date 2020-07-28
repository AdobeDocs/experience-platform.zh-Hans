---
title: 云存储目标
seo-title: 云存储目标
description: Adobe实时CDP可以将您的细分作为数据文件发送到AmazonS3、AWSKinesis、Azure事件中心或SFTP云存储位置。
seo-description: Adobe实时CDP可以将您的细分作为数据文件发送到AmazonS3、AWSKinesis、Azure事件中心或SFTP云存储位置。
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# 云存储目标 {#cloud-storage-destinations}

Adobe实时CDP可以将细分作为数据文件提供给您的云存储位置。 这使您能够通过CSV或制表符分隔的文件将受众及其用户档案属性发送到您的内部系 [!DNL Amazon S3] 统和SFTP。 对于 [!DNL AWS Kinesis] 和 [!DNL Azure Event Hubs] 目标，数据以JSON格式从Experience Platform中流出。

![Adobe云存储目标](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

有关如何连接到云存储目标的信息，请参 [阅创建云存储目标的工作流](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)。

## 数据导出类型

**基于用户档案的导出** -您正在导出受众中各个人的详细信息。 个性化需要这些详细信息，包括属性、事件、细分会员资格等。

## 可用的云存储目标

* [AmazonS3目的地](/help/rtcdp/destinations/amazon-s3-destination.md)
* [SFTP目标](/help/rtcdp/destinations/sftp-destination.md)

## 可用的云存储流目标

* [AmazonKinesis目的地](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Azure事件集线器目标](/help/rtcdp/destinations/azure-event-hubs-destination.md)