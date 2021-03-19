---
keywords: 云存储目标；云存储
title: 云存储目标概述
description: Adobe Experience Platform可以将您的区段作为数据文件传送到Amazon S3、AWS Kinesis、Azure事件中心或SFTP云存储位置。
translation-type: tm+mt
source-git-commit: 4f636de9f0cac647793564ce37c6589d096b61f7
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# 云存储目标概述{#cloud-storage-destinations}

Adobe Experience Platform可以将您的细分作为数据文件提供给您的云存储位置。 这使您能够通过CSV或制表符分隔的文件（适用于[!DNL Amazon S3]、[!DNL Azure Blob]和SFTP），将受众及其用户档案属性发送到内部系统。 对于[!DNL Amazon Kinesis]和[!DNL Azure Event Hubs]目标，以JSON格式从Experience Platform中流出数据。

![Adobe云存储目标](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

有关如何连接到云存储目标的信息，请参阅[创建云存储目标的工作流](./workflow.md)。

## 数据导出类型

**基于用户档案的导出**  — 您正在导出有关受众中个人的详细信息。个性化需要这些详细信息，其中可以包括属性、事件、区段成员资格等。

## 可用的云存储目标

- [Amazon S3连接](./amazon-s3.md)
- [Azure Blob连接](./azure-blob.md)
- [SFTP连接](./sftp.md)

## 可用的云存储流目标

- [Amazon Kinesis连接](./amazon-kinesis.md)
- [Azure事件集线器连接](./azure-event-hubs.md)