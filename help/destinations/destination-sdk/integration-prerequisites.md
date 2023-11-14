---
description: 要使用Destination SDK功能，合作伙伴公司必须满足本文档中列出的先决条件。
title: 集成先决条件
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 集成先决条件

要使用Destination SDK功能，请确保您满足以下部分列出的技术和合作伙伴先决条件。

## 流目标的技术/API先决条件 {#streaming-prerequisites}

1. 您拥有Adobe Experience Platform的REST API端点，可向提供以下类型的数据：
   * 受众会员信息；
   * 个人资料身份信息；
   * （可选）用于配置文件扩充的其他属性。
2. REST API端点支持基本、持有者令牌或OAuth 2.0身份验证协议。
3. （可选）您有用于程序化元数据管理的受众创建/更新/删除API或API端点。

## 批处理目标的技术先决条件 {#batch-prerequisites}

1. 您的目标位置托管在 [!DNL Amazon S3]， [!DNL Azure Blob]， [!DNL Azure Data Lake Storage]， [!DNL SFTP]， [!DNL Google Cloud]或私人 [!DNL Data Landing Zone]，从中可接收从Experience Platform中导出的文件。
2. 您的目标平台可以通过以下方式以配置的格式摄取文件 [文件格式选项](functionality/destination-server/file-formatting.md) 用于批处理目标的Destination SDK。
3. （可选）您具有受众创建/检索/更新/删除([!DNL CRUD])用于程序化元数据管理的API或API端点。

## 合作关系先决条件 {#partnership-prerequisites}

如果您是希望使用Destination SDK的独立软件供应商(ISV)或系统集成商(SI)，请阅读 [获取访问权限部分](overview.md#get-access).
