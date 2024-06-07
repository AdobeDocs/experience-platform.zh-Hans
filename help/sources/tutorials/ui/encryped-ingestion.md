---
title: 在源UI工作区中摄取加密数据
description: 了解如何在源UI工作区中摄取加密数据。
hide: true
hidefromtoc: true
source-git-commit: f2a0a9b84dfd3c1d32c8049148d38ef4d2ec822e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 7%

---

# 在源UI中摄取加密数据

阅读本指南，了解如何使用云存储源将加密数据摄取到Adobe Experience Platform中以存储批量数据。

## 先决条件

* 加密数据

## 摄取加密数据 {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="文件是否加密？"
>abstract="如果正在引入已加密的文件，请选择此切换开关。"


>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="选择示例文件"
>abstract="摄取加密数据时必须摄取样例文件，才能创建映射。"

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_createCustomKey"
>title="创建自定义键"
>abstract="您可以选择创建签名验证密钥对，并为加密数据创建自定义密钥。"