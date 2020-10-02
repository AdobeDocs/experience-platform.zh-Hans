---
keywords: SFTP;sftp
title: SFTP目标
seo-title: SFTP目标
description: 创建到SFTP服务器的实时出站连接，以定期从Experience Platform导出分隔的数据文件。
seo-description: 创建到SFTP服务器的实时出站连接，以定期从Experience Platform导出分隔的数据文件。
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# SFTP目标

## 概述

创建到SFTP服务器的实时出站连接，以定期从Experience Platform导出分隔的数据文件。

## 导出类型 {#export-type}

**用户档案导出** -您正在导出区段的所有成员以及所需的模式字段(例如：电子邮件地址、电话号码、姓氏)，从目标激活工作流的“选择属性”屏幕 [中进行选择](/help/rtcdp/destinations/activate-destinations.md#select-attributes)。

![基于SFTP用户档案的导出类型](/help/rtcdp/destinations/assets/sftp-export-type.png)

## 连接目标 {#connect-destination}

有关 [如何连接到您 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)的云存储目标（包括SFTP）的说明，请参阅云存储目标工作流。

对于SFTP目标，在“身份验证”步骤的“创建目标”工作流中输入以 **下信** 息：

* **主持人**:SFTP存储位置的地址
* **用户名**:登录SFTP存储的用户名
* **密码**:登录SFTP存储的口令

## 导出的数据 {#exported-data}

对于SFTP目标，Adobe实时CDP会在您提供的存储位 `.txt` 置 `.csv` 创建制表符分隔或文件。 有关这些文件的详细信息，请参 [阅区段存储教程中的电子邮件营销目](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 标和云激活目标。