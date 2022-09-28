---
description: 要使用Destination SDK，合作伙伴公司必须满足本文档中列出的先决条件。
title: 集成先决条件
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d7c9623619e989a59d72aba74903ffc0e64e7d3c
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 集成先决条件

要使用Destination SDK，请确保满足以下部分中列出的技术和合作伙伴先决条件。

## 流目标的技术/API先决条件 {#streaming-prerequisites}

1. 您拥有Adobe Experience Platform的REST API端点，可将以下类型的数据交付到：
   * 会员信息；
   * 用户档案身份信息；
   * （可选）用于扩充用户档案的其他属性。
2. 您的REST API端点支持API令牌载体身份验证或OAuth 2.0身份验证协议。
3. （可选）您具有用于程序化元数据管理的区段创建/更新/删除API或API端点。

## 批量目标的技术先决条件 {#batch-prerequisites}

1. 您的目标位置托管在 [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage]、SFTP、 [!DNL Google Cloud]，或私有 [!DNL Data Landing Zone]，您可以在其中接收导出的失Experience Platform文件。
2. 您的目标平台可以摄取通过 [文件格式选项](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) Destination SDK。
3. （可选）您具有用于程序化元数据管理的区段创建/检索/更新/删除(CRUD)API或API端点。

## 合作伙伴先决条件 {#partnership-prerequisites}

如果您是希望使用Destination SDK的独立软件供应商(ISV)或系统集成商(SI)，请阅读 [获取访问部分](./overview.md#get-access).
