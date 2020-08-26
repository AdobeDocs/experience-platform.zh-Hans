---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: AmazonS3目的地
seo-title: AmazonS3目的地
description: 创建到您的AmazonWeb服务(AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。
seo-description: 创建到您的AmazonWeb服务(AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。
translation-type: tm+mt
source-git-commit: 4c45da353b1deeb66b0dedb37450158f4bdc2a7c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# [!DNL Amazon S3] 目标

## 概述

创建到您的(AWS)S3存储的 [!DNL Amazon Web Services] 实时出站连接，以定期将制表符分隔的或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储桶中。

## 连接目标 {#connect-destination}

有关 [如何连接到您 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)的云存储目标（包括）的说明，请参阅云存储目标工作 [!DNL Amazon S3]流。

对于 [!DNL Amazon S3] 目标，在创建目标工作流中输入以下信息：

* **[!DNL Amazon S3]访问密钥[!DNL Amazon S3]和密钥**:在中 [!DNL Amazon S3]，生成 `access key - secret access key` 一对，以授予Adobe对帐户的实时CDP访 [!DNL Amazon S3] 问权。 在AmazonWeb服务文 [档中了解更多信息](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

>[!IMPORTANT]
>
>Adobe实时CDP需 `write` 要存储段对象的权限，以便交付导出文件。

## 导出的数据 {#exported-data}

对 [!DNL Amazon S3] 于目标，Adobe实时CDP会在您提供的存储位置创建制 `.txt` 表符 `.csv` 分隔的或文件。 有关这些文件的详细信息，请参 [阅区段存储教程中的电子邮件营销目](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 标和云激活目标。

<!--

Expect a new file to be created in your storage location every day. The file format is:

`amazon-s3_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->
