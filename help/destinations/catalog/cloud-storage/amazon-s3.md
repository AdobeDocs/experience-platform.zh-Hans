---
keywords: Amazon S3;S3目标；s3;Amazon s3
title: Amazon S3连接
description: 创建到Amazon Web Services(AWS)S3存储的实时出站连接，以定期将以制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储段中。
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 8d1594aeb1d6671eec187643245d940ed3ff74cd
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# [!DNL Amazon S3] 连接 {#s3-connection}

## 概述 {#overview}

创建到[!DNL Amazon Web Services](AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储段中。

## 导出类型 {#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-destinations.md#select-attributes)。

![Amazon S3基于配置文件的导出类型](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!DNL Amazon S3]访问** 密钥 **[!DNL Amazon S3]和密钥**:在中 [!DNL Amazon S3]，生成一 `access key - secret access key` 对以授予Platform对您帐户的访 [!DNL Amazon S3] 问权限。请参阅[Amazon Web服务文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)，以了解更多信息。
* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 存储段名称]**:输入此目标 [!DNL Amazon S3] 使用的存储段名称。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。

或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为[!DNL Base64]编码字符串。

>[!TIP]
>
>在连接目标工作流中，您可以为每个导出的区段文件在Amazon S3存储中创建自定义文件夹。 有关说明，请阅读[使用宏在存储位置](overview.md#use-macros)中创建文件夹。

### 所需的[!DNL Amazon S3]权限 {#required-s3-permission}

要成功将数据连接并导出到您的[!DNL Amazon S3]存储位置，请在[!DNL Amazon S3]中为[!DNL Platform]创建身份和访问管理(IAM)用户，并为以下操作分配权限：

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

有关将受众区段激活到目标的说明，请参阅[将配置文件和区段激活到目标](../../ui/activate-destinations.md)。

## 导出的数据 {#exported-data}

对于[!DNL Amazon S3]目标， [!DNL Platform]会在您提供的存储位置创建以制表符分隔的`.csv`文件。 有关这些文件的更多信息，请参阅区段激活教程中的[电子邮件营销目标和云存储目标](../../ui/activate-destinations.md#esp-and-cloud-storage) 。
