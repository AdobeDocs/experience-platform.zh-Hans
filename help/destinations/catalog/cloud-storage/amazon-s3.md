---
keywords: AmazonS3;S3目标；s3;amazon s3
title: AmazonS3目的地
seo-title: AmazonS3目的地
description: 创建到您的AmazonWeb服务(AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。
seo-description: 创建到您的AmazonWeb服务(AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Amazon S3] 目标

## 概述

创建到您的[!DNL Amazon Web Services](AWS)S3存储的实时出站连接，定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。

## 导出类型{#export-type}

**基于用户档案** -您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中进行选择](../../ui/activate-destinations.md#select-attributes)。

![AmazonS3用户档案出口型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 连接目标{#connect-destination}

有关如何连接到您的云存储目标（包括[!DNL Amazon S3]）的说明，请参阅[云存储目标工作流](./workflow.md)。

对于[!DNL Amazon S3]目标，在创建目标工作流中输入以下信息：

* **[!DNL Amazon S3]访问密钥 [!DNL Amazon S3] 和密钥**:在中 [!DNL Amazon S3]，生成一 `access key - secret access key` 对以授予Platform对您帐户的 [!DNL Amazon S3] 访问权限。请阅读[AmazonWeb服务文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)了解更多信息。

>[!IMPORTANT]
>
>平台需要对将要传送导出文件的存储段对象具有`write`权限。

## 导出的数据{#exported-data}

对于[!DNL Amazon S3]目标，平台会在您提供的存储位置创建制表符分隔的`.txt`或`.csv`文件。 有关这些文件的详细信息，请参阅区段存储教程中的[电子邮件营销目标和云激活目标](../../ui/activate-destinations.md#esp-and-cloud-storage)。
