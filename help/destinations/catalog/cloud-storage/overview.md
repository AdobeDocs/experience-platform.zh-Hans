---
keywords: 云存储目标；云存储
title: 云存储目标概述
description: Adobe Experience Platform可以将您的细分作为数据文件传送到您的AmazonS3、AWSKinesis、Azure事件中心或SFTP云存储位置。
translation-type: tm+mt
source-git-commit: 48c5f6d6a45de5f7982543f7a43cb4ece8cf3a9f
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# 云存储目标概述{#cloud-storage-destinations}

Adobe Experience Platform可以将您的细分作为数据文件提供给您的云存储位置。 这使您能够通过CSV或制表符分隔的文件（用于[!DNL Amazon S3]和SFTP）将受众及其用户档案属性发送到您的内部系统。 对于[!DNL AWS Kinesis]和[!DNL Azure Event Hubs]目标，以JSON格式从Experience Platform中流出数据。

![Adobe云存储目标](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

有关如何连接到云存储目标的信息，请参阅[创建云存储目标的工作流](./workflow.md)。

## 数据导出类型

**基于用户档案的导出** -您正在导出有关受众中个人的详细信息。个性化需要这些详细信息，包括属性、事件、细分会员资格等。

## 可用的云存储目标

- [AmazonS3连接](./amazon-s3.md)
- [Azure Blob连接](./azure-blob.md)
- [SFTP连接](./sftp.md)

## 可用的云存储流目标

- [AmazonKinesis连接](./amazon-kinesis.md)
- [Azure事件集线器连接](./azure-event-hubs.md)