---
keywords: 云存储目标；云存储
title: 云存储目标概述
description: Adobe Experience Platform可以将区段作为数据文件发送到Amazon S3、AWS Kinesis、Azure事件中心或SFTP云存储位置。
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 818c9a6f5cd39db1405827b657872b99254ad1e5
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# 云存储目标概述 {#cloud-storage-destinations}

## 概述 {#overview}

Adobe Experience Platform可以将您的区段作为数据文件传送到您的云存储位置。 这允许您通过CSV文件，将受众及其配置文件属性发送到您的内部系统 [!DNL Amazon S3], [!DNL Azure Blob] 和SFTP。 对于 [!DNL Amazon Kinesis] 和 [!DNL Azure Event Hubs] 目标中，数据会在中流出Experience Platform [!DNL JSON] 格式。

![Adobe云存储目标](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## 支持的云存储目标 {#supported-destinations}

Adobe Experience Platform支持以下云存储目标：

* [Amazon Kinesis连接](amazon-kinesis.md)
* [Amazon S3连接](amazon-s3.md)
* [Azure Blob连接](azure-blob.md)
* [Azure事件中心连接](azure-event-hubs.md)
* [SFTP连接](sftp.md)

## 连接到新的云存储目标 {#connect-destination}

要将区段发送到营销活动的云存储目标，平台必须先连接到该目标。 请参阅 [目标创建教程](../../ui/connect-destination.md) 以了解有关设置新目标的详细信息。


## 使用宏在存储位置中创建文件夹 {#use-macros}

>[!NOTE]
>
> 此部分中描述的功能当前可用于 [Amazon S3](amazon-s3.md) 仅限目标。

要在存储位置为每个区段文件创建自定义文件夹，可以在文件夹路径输入字段中使用宏。 在输入字段的末尾插入宏，如下所示。

![如何使用宏在存储中创建文件夹](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

以下示例引用了一个示例区段 `Luxury Audience` ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**宏1:`%SEGMENT_NAME%`**

输入： `acme/campaigns/2021/%SEGMENT_NAME%`
存储位置中的文件夹路径： `acme/campaigns/2021/Luxury Audience`

**宏2:`%SEGMENT_ID%`**

输入： `acme/campaigns/2021/%SEGMENT_ID%`
存储位置中的文件夹路径： `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**宏3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

输入： `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
存储位置中的文件夹路径： `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## 数据导出类型 {#export-type}

云存储目标支持 **基于用户档案的导出**. 这意味着您正在导出受众中个人的详细信息。 个性化需要提供这些详细信息，这些详细信息可以包括属性、事件、区段成员关系等。