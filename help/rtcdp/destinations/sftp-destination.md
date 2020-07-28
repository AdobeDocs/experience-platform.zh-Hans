---
title: SFTP目标
seo-title: SFTP目标
description: 创建到SFTP服务器的实时出站连接，以定期从Experience Platform导出分隔的数据文件。
seo-description: 创建到SFTP服务器的实时出站连接，以定期从Experience Platform导出分隔的数据文件。
translation-type: tm+mt
source-git-commit: c3fe5753fb23f99076f9c85b4e07af2d25a121a9
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# SFTP目标

## 概述

创建到SFTP服务器的实时出站连接，以定期从Experience Platform导出分隔的数据文件。

要导出数据，请完成以下步骤：

## 连接目标 {#connect-destination}

有关 [如何连接到您 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)的云存储目标（包括SFTP）的说明，请参阅云存储目标工作流。

对于SFTP目标，在“身份验证”步骤的“创建目标”工作流中输入以 **下信** 息：

* **主持人**: SFTP存储位置的地址
* **用户名**: 登录SFTP存储的用户名
* **密码**: 登录SFTP存储的口令