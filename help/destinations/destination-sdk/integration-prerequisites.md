---
description: 要使用Destination SDK，合作伙伴公司必须满足本文档中列出的先决条件。
title: 集成先决条件
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 集成先决条件

要使用Destination SDK，请确保您满足以下部分列出的技术和合作伙伴先决条件。

## 流目标的技术/API先决条件 {#streaming-prerequisites}

1. 您拥有[!DNL Adobe Experience Platform]的REST API终结点，可将以下类型的数据传送到：
   * 受众会员信息；
   * 个人资料身份信息；
   * （可选）用于配置文件扩充的其他属性。
2. REST API端点支持基本、持有者令牌或OAuth 2.0身份验证协议。
3. （可选）您有用于程序化元数据管理的受众创建/更新/删除API或API端点。

## 批处理目标的技术先决条件 {#batch-prerequisites}

1. 您的目标位置托管在[!DNL Amazon S3]、[!DNL Azure Blob]、[!DNL Azure Data Lake Storage]、[!DNL SFTP]、[!DNL Google Cloud]或私有[!DNL Data Landing Zone]上，您可以在其中接收从Experience Platform导出的文件。
2. 目标平台可以采用Destination SDK中通过[文件格式选项](functionality/destination-server/file-formatting.md)配置的格式来摄取文件，以用于批处理目标。
3. （可选）您具有用于程序化元数据管理的受众创建/检索/更新/删除([!DNL CRUD]) API或API端点。

## 合作关系先决条件 {#partnership-prerequisites}

如果您是希望使用Destination SDK的独立软件供应商(ISV)或系统集成商(SI)，请在[获取访问权限](overview.md#get-access)部分阅读ISV和SI的合作伙伴要求。
