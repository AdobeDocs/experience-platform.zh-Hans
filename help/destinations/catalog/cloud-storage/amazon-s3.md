---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: AmazonS3目的地
seo-title: AmazonS3目的地
description: 创建到您的AmazonWeb服务(AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。
seo-description: 创建到您的AmazonWeb服务(AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# [!DNL Amazon S3] 目标

## 概述

创建到您的(AWS)S3存储的 [!DNL Amazon Web Services] 实时出站连接，以定期将制表符分隔的或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。

## 导出类型 {#export-type}

**基于用户档案** -您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中进行选择](../../ui/activate-destinations.md#select-attributes)。

![AmazonS3用户档案出口型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 连接目标 {#connect-destination}

有关 [如何连接到您 ](./workflow.md) 的云存储目标（包括）的说明，请参阅云存储目标工作流 [!DNL Amazon S3]程。

对于 [!DNL Amazon S3] 目标，在创建目标工作流中输入以下信息：

* **[!DNL Amazon S3]访问密钥 [!DNL Amazon S3] 和密钥**:在中 [!DNL Amazon S3]，生成 `access key - secret access key` 一对以授予对您帐户的实时CDP访 [!DNL Amazon S3] 问权。 在AmazonWeb服务文 [档中了解更多信息](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

>[!IMPORTANT]
>
>实时CDP需要对 `write` 存储段对象的权限，在该对象中将传送导出文件。

## 导出的数据 {#exported-data}

对 [!DNL Amazon S3] 于目标，实时CDP会在您提供的存储位置 `.txt` 创建制 `.csv` 表符分隔的或文件。 有关这些文件的详细信息，请参 [阅区段存储教程中的电子邮件营销目](../../ui/activate-destinations.md#esp-and-cloud-storage) 标和云激活目标。
