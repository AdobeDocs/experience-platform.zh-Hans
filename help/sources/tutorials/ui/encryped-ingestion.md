---
title: 在源UI Workspace中摄取加密数据
description: 了解如何在源UI工作区中摄取加密数据。
badge: Beta 版
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: b4545943abbb68d36a64935feb4466d075331504
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 7%

---

# 在源UI中摄取加密数据

>[!AVAILABILITY]
>
>对源UI中加密数据摄取的支持处于测试阶段，您的组织可能无法获得这些支持。 该功能和文档可能会发生更改。

您可以使用云存储批处理源将加密的数据文件和文件夹摄取到Adobe Experience Platform。 通过加密的数据摄取，您可以利用非对称加密机制将批量数据安全地传输到Experience Platform中。 目前，支持的不对称加密机制有PGP和GPG。

此功能可用于以下源：

* [Amazon S3]
* [Azure Blob]
* [Azure Data Lake Storage Gen2]
* [Azure文件存储]
* [数据登陆区]
* [FTP]
* [Google云存储]
* [HDFS]
* [Oracle对象存储]
* [SFTP]

阅读本指南，了解如何使用UI通过云存储批处理源摄取加密数据。

## 快速入门

在UI中使用加密的数据摄取之前，了解以下Experience Platform功能和概念会很有帮助：

* [源](../../home.md)：在Experience Platform中使用源从Adobe应用程序或第三方数据源中摄取数据。
* [数据流](../../../dataflows/home.md)：数据流是跨Experience Platform移动数据的数据作业的表示形式。 您可以使用源工作区创建数据流，以将数据从给定源摄取到Experience Platform。
* [沙盒](../../../sandboxes/home.md)：使用Experience Platform中的沙盒在Experience Platform实例之间创建虚拟分区，并创建专用于开发或生产的环境。

### 高级大纲

1. 使用Experience PlatformUI中的源工作区创建加密密钥对。 或者，您也可以创建签名验证密钥对，为加密数据提供额外的安全层。
2. 使用公钥加密数据。
3. 将加密数据放入云存储提供商中。 在此步骤中，还必须确保您有一个示例文件，该文件可用作参考，以将源数据映射到体验数据模型(XDM)架构。
4. 通过创建源连接将加密数据摄取到Experience Platform。
5. 在创建源连接时，提供与用于加密数据的公钥对应的密钥ID。 如果您还使用签名验证密钥对机制，则还必须提供与加密数据对应的签名验证密钥ID。
6. 继续数据流创建步骤。

## 创建加密密钥对 {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="加密密钥ID"
>abstract="提供与用于加密源数据的加密密钥对应的加密密钥ID。"

* 在Platform UI中，导航到源工作区，然后从顶部标题中选择[!UICONTROL 键对]。
* 此时您会进入一个页面，该页面显示组织中现有加密密钥对的列表。 本页提供有关给定密钥的标题、ID、类型、加密算法、到期和状态的信息。 要创建新的密钥对，请选择&#x200B;**[!UICONTROL 创建密钥]**。
* 接下来，选择要创建的键类型。 要创建加密密钥，请选择&#x200B;**[!UICONTROL 加密密钥]**，然后提供加密密钥的标题和密码。 密码是加密密钥的附加保护层。 创建后，Experience Platform将该密码短语存储在与公钥不同的安全电子仓库中。 您必须提供非空字符串作为密码短语。

### 创建签名验证密钥 {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="签名验证密钥ID"
>abstract="提供与已签名加密的源数据对应的签名验证密钥ID。"

## 提取加密数据 {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="文件是否加密？"
>abstract="如果您正在提取已加密的文件，请选择此切换选项。"

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="选择示例文件"
>abstract="为了创建映射，您必须在提取加密数据时提取示例文件。"


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
