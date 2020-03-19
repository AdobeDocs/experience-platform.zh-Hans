---
title: Amazon S3目标
seo-title: Amazon S3目标
description: 创建到Amazon Web Services(AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储段中。
seo-description: 创建到Amazon Web Services(AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储段中。
translation-type: tm+mt
source-git-commit: acd3865be4994a478048d317060c55b7e0d9914c

---


# Amazon S3目标

## 概述

创建到Amazon Web Services(AWS)S3存储的实时出站连接，以定期将制表符分隔或CSV数据文件从Adobe Experience Platform导出到您自己的S3存储段中。

## 连接目标 {#connect-destination}

有关如 [何连接到您的云存 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)储目标（包括Amazon S3）的说明，请参阅云存储目标工作流程。

对于Amazon S3目标，在创建目标工作流中输入以下信息：

* **Amazon S3访问密钥和Amazon S3密钥**:在Amazon S3中，生成访问密钥——秘密访问密钥对，以授予Adobe对Amazon S3帐户的实时CDP访问权；
* **Amazon S3路径**:这是Amazon S3存储桶中Adobe实时CDP传送导出文件的位置。


>[!IMPORTANT]
>
>Adobe实时CDP需要对将要 `write` 在其中传送导出文件的存储段对象具有权限。
