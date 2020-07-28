---
title: AmazonS3目的地
seo-title: AmazonS3目的地
description: 创建到您的AmazonWeb服务(AWS)S3存储的实时出站连接，定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储段。
seo-description: 创建到您的AmazonWeb服务(AWS)S3存储的实时出站连接，定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储段。
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# [!DNL Amazon S3] 目标

## 概述

创建到您的(AWS)S3存储的 [!DNL Amazon Web Services] 实时出站连接，以定期将制表符分隔的或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。

## 连接目标 {#connect-destination}

有关 [如何连接到您 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)的云存储目标（包括）的说明，请参阅云存储目标工作 [!DNL Amazon S3]流。

对于 [!DNL Amazon S3] 目标，在创建目标工作流中输入以下信息：

* **[!DNL Amazon S3]访问密钥[!DNL Amazon S3]和密钥&#x200B;**: 在中[!DNL Amazon S3]，生成一个访问密钥——秘密访问密钥对，以授予Adobe对您帐户的实时CDP访[!DNL Amazon S3]问权。



>[!IMPORTANT]
>
>Adobe实时CDP需 `write` 要存储段对象的权限，以便交付导出文件。
