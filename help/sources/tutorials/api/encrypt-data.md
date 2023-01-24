---
title: 加密数据摄取
description: Adobe Experience Platform允许您通过云存储批量源摄取加密文件。
hide: true
hidefromtoc: true
source-git-commit: 0457784b8aa97d55882b794077aecdbd2a9a612a
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---

# 加密数据摄取

Adobe Experience Platform允许您通过云存储批量源摄取加密文件。 通过加密的数据摄取，您可以利用非对称加密机制将批量数据安全地传输到Experience Platform。 目前，支持的非对称加密机制是PGP和GPG。

加密的数据获取流程如下所示：

1. [使用Experience PlatformAPI创建加密密钥对](#create-encryption-key-pair). 加密密钥对由私钥和公钥组成。 创建公钥后，您可以复制或下载公钥，以及其相应的公钥ID和到期时间。 在此过程中，私钥将通过Experience Platform存储在安全保管库中。
2. 使用公钥加密要摄取的数据文件。
3. 将加密文件放入云存储中。
4. 加密文件准备就绪后， [为云存储源创建源连接和数据流](#create-a-dataflow-for-encrypted-data). 在流创建步骤中，必须提供 `encryption` 参数并包含您的公共密钥ID。
5. Experience Platform从安全保管库中检索私钥，以在摄取时解密数据。

本文档提供了有关如何生成加密密钥对以加密数据，以及如何使用云存储源将加密数据引入Experience Platform的步骤。

## 快速入门

本教程要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
   * [云存储源](../api/collect/cloud-storage.md):创建数据流以将云存储源中的批处理数据引入Experience Platform。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 创建加密密钥对 {#create-encryption-key-pair}

将加密数据摄取到Experience Platform的第一步是，通过向 `/encryption/keys` 的端点 [!DNL Connectors] API。

**API格式**

```http
POST /data/foundation/connectors/encryption/keys
```

**请求**

以下请求使用PGP加密算法生成加密密钥对。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{PASSPHRASE}"
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `encryptionAlgorithm` | 您使用的加密算法类型。 支持的加密类型包括 `PGP` 和 `GPG`. |
| `params.passPhrase` | 密码短语为您的加密密钥提供了额外的保护层。 在创建时，Experience Platform将密码短语存储到与公钥不同的安全保管库中。 必须提供非空字符串作为密码短语。 |

**响应**

成功的响应会返回您的公钥、公钥ID和密钥的到期时间。 到期时间会自动设置为密钥生成日期后的180天。 当前无法配置到期时间。

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## 使用将云存储源连接到Experience Platform [!DNL Flow Service] API

在检索到加密密钥对后，您现在可以继续并为云存储源创建源连接，并将加密数据引入平台。

首先，必须创建基本连接才能针对Platform验证源。 要创建基本连接并验证源，请从下面的列表中选择要使用的源：

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure数据湖存储第2代](../api/create/cloud-storage/adls-gen2.md)
* [Azure文件存储](../api/create/cloud-storage/azure-file-storage.md)
* [数据登陆区](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google云存储](../api/create/cloud-storage/google.md)
* [Oracle对象存储](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

创建基本连接后，您必须按照教程中列出的步骤操作 [为云存储源创建源连接](../api/collect/cloud-storage.md) 为了创建源连接、目标连接和映射。

## 为加密数据创建数据流 {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>为了创建用于加密数据摄取的数据流，您必须具备以下条件：
>* [公钥ID](#create-encryption-key-pair)
>* [源连接ID](../api/collect/cloud-storage.md#source)
>* [Target连接ID](../api/collect/cloud-storage.md#target)
>* [映射ID](../api/collect/cloud-storage.md#mapping)


要创建数据流，请向POST请求 `/flows` 的端点 [!DNL Flow Service] API。 要摄取加密数据，您必须添加 `encryption` 的 `transformations` 属性并包含 `publicKeyId` 在之前的步骤中创建。

**API格式**

```http
POST /flows
```

**请求**

以下请求会创建一个数据流，以为云存储源摄取加密数据。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Customer Data",
      "description: "ACME encrypted data ingestion",
      "flowSpec": {
          "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "26b53912-1005-49f0-b539-12100559f0e2"
      ],
      "targetConnectionIds": [
        "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                  "mappingVersion": 0
              }
          },
          {
              "name": "Encryption",
              "params": {
                  "publicKeyId": 512e686e-543e-4354-bcba-e1403ddcc532
          }
  }
      ],
      "scheduleParams": {
          "startTime": "1597784298",
          "frequency": "once"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `flowSpec.id` | 与云存储源对应的流程规范ID。 |
| `sourceConnectionIds` | 源连接ID。 此ID表示数据从源传输到平台。 |
| `targetConnectionIds` | 目标连接ID。 此ID表示数据在传递到Platform后登陆的位置。 |
| `transformations[x].params.mappingId` | 映射ID。 |
| `transformations.name` | 摄取加密文件时，必须提供 `Encryption` 作为数据流的其他转换参数。 |
| `transformations[x].params.publicKeyId` | 您创建的公共密钥ID。 此ID是用于加密云存储数据的加密密钥对的一半。 |
| `scheduleParams.startTime` | 新纪元时间中数据流的开始时间。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括： `once`, `minute`, `hour`, `day`或 `week`. |
| `scheduleParams.interval` | 该间隔指定两个连续流运行之间的周期。 间隔的值应为非零整数。 将频率设置为时，不需要间隔 `once` 且应大于或等于 `15` 的其他频率值。 |

**响应**

成功的响应会返回ID(`id`)新创建的数据流。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 后续步骤

在本教程中，您为云存储数据创建了一个加密密钥对，并创建了一个数据流，以使用 [!DNL Flow Service API]. 有关数据流的完整性、错误和量度的状态更新，请阅读 [使用监控数据流 [!DNL Flow Service] API](./monitor.md).