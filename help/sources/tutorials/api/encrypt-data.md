---
title: 加密数据摄取
description: Adobe Experience Platform允许您通过cloud storage批处理源摄取加密文件。
hide: true
hidefromtoc: true
source-git-commit: a1babf70a7a4e20f3e535741c95ac927597c9f48
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---

# 加密数据摄取

Adobe Experience Platform允许您通过cloud storage批处理源摄取加密文件。 通过加密的数据摄取，您可以利用非对称加密机制将批量数据安全地传输到Experience Platform。 目前，支持的不对称加密机制有PGP和GPG。

加密数据摄取过程如下：

1. [使用Experience PlatformAPI创建加密密钥对](#create-encryption-key-pair). 加密密钥对由私钥和公钥组成。 创建后，您可以复制或下载公钥及其对应的公钥ID和到期时间。 在此过程中，私钥将由Experience Platform存储在安全保险库中。 **注意：** 响应中的公钥采用Base64编码，必须在使用之前解密。
2. 使用公钥加密要摄取的数据文件。
3. 将加密文件放入云存储中。
4. 加密文件准备就绪后， [为云存储源创建源连接和数据流](#create-a-dataflow-for-encrypted-data). 在流创建步骤中，您必须提供 `encryption` 参数，并包含您的公钥ID。
5. Experience Platform从安全保险库中检索私钥，以在摄取数据时解密数据。

>[!IMPORTANT]
>
>单个加密文件的最大大小为100MB。 例如，您可以在单个数据流运行中摄取价值2GB的数据，但该数据中的任何单个文件不能超过100MB。

本文档提供了有关如何生成加密密钥对以加密数据的步骤，以及如何使用云存储源将加密的数据摄取到Experience Platform的步骤。

## 快速入门

本教程要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
   * [云存储源](../api/collect/cloud-storage.md)：创建数据流以将批量数据从云存储源引入Experience Platform。
* [沙盒](../../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 创建加密密钥对 {#create-encryption-key-pair}

将加密数据摄取到Experience Platform的第一步是通过向以下对象发出POST请求来创建加密密钥对： `/encryption/keys` 的端点 [!DNL Connectors] API。

**API格式**

```http
POST /data/foundation/connectors/encryption/keys
```

**请求**

以下请求使用PGP加密算法生成加密密钥对。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `encryptionAlgorithm` | 正在使用的加密算法类型。 支持的加密类型包括 `PGP` 和 `GPG`. |
| `params.passPhrase` | 密码为加密密钥提供了一层额外的保护。 创建后，Experience Platform将密码存储在与公钥不同的安全保管库中。 您必须提供非空字符串作为密码短语。 |

**响应**

成功响应将返回您的Base64编码公共密钥、公共密钥ID和密钥的过期时间。 到期时间自动设置为生成密钥日期后的180天。 到期时间当前不可配置。

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## 使用将云存储源连接到Experience Platform [!DNL Flow Service] API

在检索到加密密钥对后，您现在可以继续为云存储源创建源连接，并将加密数据带到Platform。

首先，您必须创建一个基本连接，以根据Platform验证您的源。 要创建基本连接并对源进行身份验证，请从以下列表中选择要使用的源：

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure文件存储](../api/create/cloud-storage/azure-file-storage.md)
* [数据登陆区](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google云存储](../api/create/cloud-storage/google.md)
* [oracle对象存储](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

创建基本连接后，您必须按照以下教程中概述的步骤操作： [为云存储源创建源连接](../api/collect/cloud-storage.md) 以创建源连接、目标连接和映射。

## 为加密数据创建数据流 {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>您必须具备以下条件，才能为加密的数据引入创建数据流：
>* [公钥ID](#create-encryption-key-pair)
>* [源连接ID](../api/collect/cloud-storage.md#source)
>* [目标连接ID](../api/collect/cloud-storage.md#target)
>* [映射Id](../api/collect/cloud-storage.md#mapping)


POST要创建数据流，请向 `/flows` 的端点 [!DNL Flow Service] API。 要摄取加密数据，您必须添加 `encryption` 部分到 `transformations` 属性并包括 `publicKeyId` 之前步骤创建的。

**API格式**

```http
POST /flows
```

**请求**

以下请求将创建一个数据流以摄取云存储源的加密数据。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `flowSpec.id` | 与云存储源对应的流规范ID。 |
| `sourceConnectionIds` | 源连接ID。 此ID表示数据从源传输到平台。 |
| `targetConnectionIds` | 目标连接ID 此ID表示将数据提交到Platform后数据登陆的位置。 |
| `transformations[x].params.mappingId` | 映射ID。 |
| `transformations.name` | 摄取加密文件时，必须提供 `Encryption` 作为数据流的附加转换参数。 |
| `transformations[x].params.publicKeyId` | 您创建的公钥ID。 此ID是用来加密云存储数据的加密密钥对的一半。 |
| `scheduleParams.startTime` | 数据流的开始时间（以Epoch时间表示）。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括： `once`， `minute`， `hour`， `day`，或 `week`. |
| `scheduleParams.interval` | 间隔指定两次连续流运行之间的周期。 间隔值应为非零整数。 当频率设置为时，不需要间隔 `once` 和应大于或等于 `15` 其他频率值。 |

**响应**

成功的响应会返回ID (`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 后续步骤

通过阅读本教程，您已为云存储数据创建了一个加密密钥对，并创建了数据流以使用摄取您的加密数据 [!DNL Flow Service API]. 有关数据流完整性、错误和量度的状态更新，请阅读以下指南： [使用监控数据流 [!DNL Flow Service] API](./monitor.md).