---
keywords: Amazon S3;S3目标；s3;Amazon s3
title: Amazon S3连接
description: 创建到Amazon Web Services(AWS)S3存储的实时出站连接，以定期将CSV数据文件从Adobe Experience Platform导出到您自己的S3存储段中。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: bf46f4e6549fcbd975a9f0a6034040ed2e9b34e6
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# [!DNL Amazon S3] 连接 {#s3-connection}

## 概述 {#overview}

创建到的实时出站连接 [!DNL Amazon Web Services] (AWS)S3存储，可将CSV数据文件从Adobe Experience Platform定期导出到您自己的S3存储段中。

## 导出类型 {#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，从 [目标激活工作流](../../ui/activate-segment-streaming-destinations.md#mapping).

![Amazon S3基于配置文件的导出类型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 连接到目标 {#connect}

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA公钥"
>abstract="或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须编写为Base64编码字符串。"
>text="Learn more in documentation"

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!DNL Amazon S3]访问密钥** 和 **[!DNL Amazon S3]密钥**:在 [!DNL Amazon S3]，生成 `access key - secret access key` 对，以授予对 [!DNL Amazon S3] 帐户。 在 [Amazon Web Services文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 存储段名称]**:输入 [!DNL Amazon S3] 存储段供此目标使用。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。

或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为 [!DNL Base64] 编码字符串。

>[!TIP]
>
>在连接目标工作流中，您可以为每个导出的区段文件在Amazon S3存储中创建自定义文件夹。 读取 [使用宏在存储位置中创建文件夹](overview.md#use-macros) 中。

### 必需 [!DNL Amazon S3] 权限 {#required-s3-permission}

要成功将数据连接并导出到 [!DNL Amazon S3] 存储位置，为创建Identity and Access Management(IAM)用户 [!DNL Platform] in [!DNL Amazon S3] 并为以下操作分配权限：

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

## 将区段激活到此目标 {#activate}

请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

对于 [!DNL Amazon S3] 目标， [!DNL Platform] 创建 `.csv` 文件。 有关文件的更多信息，请参阅 [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 区段激活教程中的。
