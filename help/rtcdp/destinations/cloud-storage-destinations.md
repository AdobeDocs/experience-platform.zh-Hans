---
title: 云存储目标
seo-title: 云存储目标
description: Adobe实时CDP可以将您的细分作为数据文件传送到您的Amazon S3、AWS Kinesis、Azure事件中心或SFTP云存储位置。
seo-description: Adobe实时CDP可以将您的细分作为数据文件传送到您的Amazon S3、AWS Kinesis、Azure事件中心或SFTP云存储位置。
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# 云存储目标 {#cloud-storage-destinations}

Adobe实时CDP可以将您的细分作为数据文件提供给您的云存储位置。 这使您能够通过CSV或制表符分隔的文件，将受众及其用户档案属性发送到您的内部系统，这些文件适用于Amazon S3和SFTP。 对于AWS Kinesis和Azure事件中心目标，数据以JSON格式从Experience Platform中流化。

![Adobe Cloud存储目标](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

有关如何连接到云存储目标的信息，请参 [阅创建云存储目标的工作流](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)。

## 数据导出类型

**基于用户档案的导出** -您正在导出受众中各个人的详细信息。 个性化需要这些详细信息，包括属性、事件、细分会员资格等。

## 可用的云存储目标

* [Amazon S3目标](/help/rtcdp/destinations/amazon-s3-destination.md)
* [SFTP目标](/help/rtcdp/destinations/sftp-destination.md)

## 可用的云存储流目标

* [Amazon Kinesis目标](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Azure EventHubs目标](/help/rtcdp/destinations/azure-event-hubs-destination.md)