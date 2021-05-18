---
keywords: Amazon S3;S3目标；s3;amazon s3
title: Amazon S3连接
description: 创建到Amazon Web Services(AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 70be44e919070df910d618af4507b600ad51123c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# [!DNL Amazon S3] 连接  {#s3-connection}

## 概述 {#overview}

创建到[!DNL Amazon Web Services](AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。

## 导出类型{#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-destinations.md#select-attributes)。

![Amazon S3基于用户档案的导出类型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 连接目标{#connect-destination}

有关如何连接到您的云存储目标（包括[!DNL Amazon S3]）的说明，请参阅[云存储目标工作流](./workflow.md)。

对于[!DNL Amazon S3]目标，在创建目标工作流中输入以下信息：

* **[!DNL Amazon S3]访问密钥 [!DNL Amazon S3] 和密钥**:在中 [!DNL Amazon S3]，生成一 `access key - secret access key` 对以授予对您帐户的平台 [!DNL Amazon S3] 访问权。请阅读[Amazon Web服务文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)了解更多信息。

>[!TIP]
>
>在连接目标工作流中，您可以根据导出的段文件在Amazon S3存储中创建自定义文件夹。 有关说明，请阅读[使用宏在存储位置](./workflow.md#use-macros)中创建文件夹。

## 所需的[!DNL Amazon S3]权限{#required-s3-permission}

要成功将数据连接并导出到您的[!DNL Amazon S3]存储位置，请在[!DNL Amazon S3]中为[!DNL Platform]创建一个Identity and Access Management(IAM)用户，并为以下操作分配权限：

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`


<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->


## 导出的数据{#exported-data}

对于[!DNL Amazon S3]目标，[!DNL Platform]会在您提供的存储位置创建制表符分隔的`.csv`文件。 有关这些文件的详细信息，请参阅区段存储教程中的[电子邮件营销目标和云激活目标](../../ui/activate-destinations.md#esp-and-cloud-storage)。
