---
keywords: SFTP;sftp
title: SFTP连接
description: 创建到SFTP服务器的实时出站连接，以定期从Adobe Experience Platform导出分隔的数据文件。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: a21abb44bb9cbe6fefa0ff70a1ff19e31cc0c7de
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# SFTP连接

## 概述 {#overview}

创建到SFTP服务器的实时出站连接，以定期从Adobe Experience Platform导出分隔的数据文件。

>[!IMPORTANT]
>
> 虽然Adobe支持向SFTP服务器导出存储，但建议的用于导出数据的云位置是[!DNL Amazon S3]和[!DNL Azure Blob]。

## 导出类型{#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-destinations.md#select-attributes)。

![基于SFTP用户档案的导出类型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 连接目标{#connect-destination}

有关如何连接到您的云存储目标（包括SFTP）的说明，请参阅[云存储目标工作流](./workflow.md)。

对于SFTP目标，请在&#x200B;**身份验证**&#x200B;步骤的创建目标工作流中输入以下信息：

* **主持人**:SFTP存储位置的地址
* **用户名**:登录SFTP存储位置的用户名
* **密码**:登录SFTP存储位置的密码

## 导出的数据{#exported-data}

对于[!DNL SFTP]目标，平台会在您提供的存储位置创建制表符分隔的`.csv`文件。 有关这些文件的详细信息，请参阅区段存储教程中的[电子邮件营销目标和云激活目标](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## IP地址允许列表

如果您需要向允许列表添加AdobeIP，请参阅云存储目标](./ip-address-allow-list.md)的[ IP地址允许列表。
