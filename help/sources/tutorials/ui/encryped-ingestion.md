---
title: 在源UI Workspace中摄取加密数据
description: 了解如何在源UI工作区中摄取加密数据。
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 9f827c1ba97fba237c216fce9c2966bcc91fd05b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 30%

---

# 在源UI中摄取加密数据

阅读本指南，了解如何使用云存储源将加密数据摄取到Adobe Experience Platform中以存储批量数据。

## 先决条件

* 加密数据

## 提取加密数据 {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="文件是否加密？"
>abstract="如果您正在提取已加密的文件，请选择此切换选项。"

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="选择示例文件"
>abstract="为了创建映射，您必须在提取加密数据时提取示例文件。"

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="加密密钥ID"
>abstract="提供与用于加密源数据的加密密钥对应的加密密钥ID。"

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="签名验证密钥ID"
>abstract="提供与已签名加密的源数据对应的签名验证密钥ID。"

<!-- 
## Outline

Sections:

* Create public key
* Create customer key
* Create sources flow to ingest encrypted data
  * File ingestion
  * Folder ingestion
* Updated encrypted flow

* Select [!UICONTROL Key Pairs] from the header in the sources UI workspace.
  * You are taken to the [!UICONTROL Key Pairs] page:
    * Select **[!UICONTROL Encryption key]** for list of key pairs that you have created and managed.
    * Select **[!UICONTROL Customer key]** for a list of key pairs that your customers have created and managed.
* Key Pair functions:
  * Select **[!UICONTROL Key details]** to view key details.
  * Select **[!UICONTROL Delete]** to delete.
* Select [!UICONTROL Create key] to create either an encryption key or a customer key

## Questions and clarifications

* Public key vs. customer key
* Verify E2E:
  * Create keys (encryption key or customer key)
  * Use these keys to encrypt your data
  * Place your encrypted data in your cloud storage (Amazon S3 or Google Cloud Storage)
  * Ingest that encrypted data to Experience Platform by creating a source connection
    * Select the encrypted source data
    * Enable "Is the file encrypted"
    * Select/upload sample file for mapping
    * Use the encryption key name that corresponds with the key used to encrypt the source data
      * If the data was encrypted using customer key, provide the sign verification key.
  * Proceed with source connection creation flow -->
