---
keywords: SFTP;SFTP
title: SFTP连接
description: 创建与SFTP服务器的实时出站连接，以定期从Adobe Experience Platform导出分隔数据文件。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: b7392596c7ed96032dc8ad6bb8e423640f562394
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# SFTP连接

## 概述 {#overview}

创建与SFTP服务器的实时出站连接，以定期从Adobe Experience Platform导出分隔数据文件。

>[!IMPORTANT]
>
> 虽然Adobe支持向SFTP服务器导出数据，但建议的用于导出数据的云存储位置为[!DNL Amazon S3]和[!DNL Azure Blob]。

## 导出类型 {#export-type}

**基于用户档案**  — 您正在导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中选择](../../ui/activate-batch-profile-destinations.md)。

![基于SFTP配置文件的导出类型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **主机**:SFTP存储位置的地址
* **用户名**:登录SFTP存储位置的用户名
* **密码**:登录SFTP存储位置的密码
* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。

或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为[!DNL Base64]编码字符串。

## 导出的数据 {#exported-data}

对于[!DNL SFTP]目标，Platform会在您提供的存储位置中创建一个以制表符分隔的`.csv`文件。 有关这些文件的更多信息，请参阅区段激活教程中的[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md) 。

## IP地址允许列表

如果需要向允许列表添加AdobeIP，请参阅云存储目标的[IP地址允许列表](ip-address-allow-list.md) 。
