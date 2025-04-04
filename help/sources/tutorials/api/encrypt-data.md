---
title: 加密的数据摄取
description: 了解如何使用API通过云存储批处理源摄取加密文件。
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 3%

---

# 加密的数据摄取

您可以使用云存储批处理源将加密的数据文件摄取到Adobe Experience Platform。 通过加密的数据摄取，您可以利用非对称加密机制将批量数据安全地传输到Experience Platform。 目前，支持的不对称加密机制有PGP和GPG。

加密数据摄取过程如下：

1. [使用Experience Platform API创建加密密钥对](#create-encryption-key-pair)。 加密密钥对由私钥和公钥组成。 创建后，您可以复制或下载公钥及其对应的公钥ID和到期时间。 在此过程中，私钥将由Experience Platform存储在安全保险库中。 **注意：**&#x200B;响应中的公钥采用Base64编码，必须在使用之前进行解码。
2. 使用公钥加密要摄取的数据文件。
3. 将加密文件放入云存储中。
4. 加密文件准备就绪后，[为您的云存储源](#create-a-dataflow-for-encrypted-data)创建源连接和数据流。 在流创建步骤中，必须提供`encryption`参数并包含公钥ID。
5. Experience Platform会从安全保险库中检索私钥，以在摄取数据时解密数据。

>[!IMPORTANT]
>
>单个加密文件的最大大小为1 GB。 例如，您可以在单个数据流运行中摄取价值2 GB的数据，但该数据中的任何单个文件不能超过1 GB。

本文档提供了有关如何生成加密密钥对以加密您的数据，以及使用云存储源将该加密数据摄取到Experience Platform的步骤。

## 快速入门 {#get-started}

本教程要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
   * [云存储源](../api/collect/cloud-storage.md)：创建数据流以将批量数据从云存储源引入Experience Platform。
* [沙盒](../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../landing/api-guide.md)指南。

### 加密文件支持的文件扩展名 {#supported-file-extensions-for-encrypted-files}

加密文件支持的文件扩展名列表为：

* .csv
* .tsv
* .json
* .parquet
* .csv.gpg
* .tsv.gpg
* .json.gpg
* .parquet.gpg
* .csv.pgp
* .tsv.pgp
* .json.pgp
* .parquet.pgp
* .gpg
* .pgp

>[!NOTE]
>
>Adobe Experience Platform源中的加密文件摄取支持openPGP，而不支持PGP的任何特定专有版本。

## 创建加密密钥对 {#create-encryption-key-pair}

>[!IMPORTANT]
>
>加密密钥特定于给定的沙盒。 因此，如果您希望将加密数据摄取到组织内其他沙盒中，则必须创建新的加密密钥。

将加密数据摄取到Experience Platform的第一步是通过向[!DNL Connectors] API的`/encryption/keys`端点发出POST请求来创建您的加密密钥对。

**API格式**

```http
POST /data/foundation/connectors/encryption/keys
```

**请求**

+++查看示例请求

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
      "name": "acme-encryption",
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 加密密钥对的名称。 |
| `encryptionAlgorithm` | 正在使用的加密算法类型。 支持的加密类型为`PGP`和`GPG`。 |
| `params.passPhrase` | 密码短语为加密密钥提供了额外的保护层。 创建后，Experience Platform会将该密码短语存储在与公钥不同的安全保管库中。 您必须提供非空字符串作为密码短语。 |

+++

**响应**

+++查看示例响应

成功的响应将返回Base64编码的公共密钥、公共密钥ID以及密钥的过期时间。 到期时间自动设置为生成密钥日期后的180天。 到期时间当前不可配置。

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

| 属性 | 描述 |
| --- | --- |
| `publicKey` | 公钥用于对云存储中的数据进行加密。 此密钥与此步骤中创建的私钥相对应。 但是，私钥会立即发送到Experience Platform。 |
| `publicKeyId` | 公钥ID用于创建数据流并将加密的云存储数据摄取到Experience Platform。 |
| `expiryTime` | 到期时间定义加密密钥对的到期日期。 此日期自动设置为密钥生成日期后的180天，并以unix时间戳格式显示。 |

+++

### 检索加密密钥 {#retrieve-encryption-keys}

要检索组织中的所有加密密钥，请向`/encryption/keys`终结点=nt发出GET请求。

**API格式**

```http
GET /data/foundation/connectors/encryption/keys
```

**请求**

+++查看示例请求

以下请求将检索您组织中的所有加密密钥。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**响应**

+++查看示例响应

成功的响应将返回加密算法、名称、公共密钥、公共密钥ID、密钥类型以及相应的密钥到期时间。

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "name": "{NAME}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "keyType": "{KEY_TYPE}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### 按ID检索加密密钥 {#retrieve-encryption-keys-by-id}

要检索一组特定的加密密钥，请向`/encryption/keys`端点发出GET请求，并提供您的公共密钥ID作为标头参数。

**API格式**

```http
GET /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**请求**

+++查看示例请求

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**响应**

+++查看示例响应

成功的响应将返回加密算法、名称、公共密钥、公共密钥ID、密钥类型以及相应的密钥到期时间。

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "name": "{NAME}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "keyType": "{KEY_TYPE}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### 创建客户管理的密钥对 {#create-customer-managed-key-pair}

您可以选择创建签名验证密钥对，以对您的加密数据进行签名和摄取。

在此阶段，您必须生成自己的私钥和公钥组合，然后使用私钥对加密数据进行签名。 接下来，您必须在Base64中对公钥进行编码，然后将其共享到Experience Platform，以便Experience Platform验证您的签名。

### 将您的公钥共享到Experience Platform

要共享公钥，请在提供加密算法和Base64编码公钥的同时向`/customer-keys`端点发出POST请求。

**API格式**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**请求**

+++查看示例请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "name": "acme-sign-verification-keys"
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}},
      "params": {
          "passPhrase": {{PASS_PHRASE}}
      }
    }'
```

| 参数 | 描述 |
| --- | --- |
| `encryptionAlgorithm` | 正在使用的加密算法类型。 支持的加密类型为`PGP`和`GPG`。 |
| `publicKey` | 对应于客户管理的用于签署您的加密密钥的公共密钥。 此密钥必须为Base64编码。 |

+++

**响应**

+++查看示例响应

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| 属性 | 描述 |
| --- | --- |
| `publicKeyId` | 在与Experience Platform共享您的客户管理的密钥时，会返回此公钥ID。 在为签名和加密数据创建数据流时，您可以提供此公钥ID作为签名验证密钥ID。 |

+++

### 检索客户管理的密钥对

要检索您的客户托管密钥，请向`/customer-keys`端点发出GET请求。

**API格式**

```http
GET /data/foundation/connectors/encryption/customer-keys
```

**请求**

+++查看示例请求

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**响应**

+++查看示例响应

```json
[
    {
        "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
        "name": "{NAME}",
        "publicKeyId": "{PUBLIC_KEY_ID}",
        "publicKey": "{PUBLIC_KEY}",
        "keyType": "{KEY_TYPE}",
    }
]
```

+++

## 使用[!DNL Flow Service] API将您的云存储源连接到Experience Platform

在检索到加密密钥对后，您现在可以继续为云存储源创建源连接，并将加密数据导入Experience Platform。

首先，必须创建基本连接以针对Experience Platform验证源。 要创建基本连接并验证源，请从以下列表中选择要使用的源：

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure 文件存储](../api/create/cloud-storage/azure-file-storage.md)
* [数据登陆区](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google 云存储](../api/create/cloud-storage/google.md)
* [Oracle 对象存储](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

创建基本连接后，您必须按照教程中有关[为云存储源](../api/collect/cloud-storage.md)创建源连接的步骤进行操作，以便创建源连接、目标连接和映射。

## 为加密数据创建数据流 {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>要创建用于加密数据提取的数据流，您必须具备以下条件：
>
>* [公钥ID](#create-encryption-key-pair)
>* [Source连接ID](../api/collect/cloud-storage.md#source)
>* [目标连接ID](../api/collect/cloud-storage.md#target)
>* [映射ID](../api/collect/cloud-storage.md#mapping)

要创建数据流，请向[!DNL Flow Service] API的`/flows`端点发出POST请求。 要摄取加密数据，您必须将`encryption`部分添加到`transformations`属性中，并包含在先前步骤中创建的`publicKeyId`。

**API格式**

```http
POST /flows
```

>[!BEGINTABS]

>[!TAB 为加密的数据引入创建数据流]

**请求**

+++查看示例请求

以下请求会创建数据流以摄取云存储源的加密数据。

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
| `sourceConnectionIds` | 源连接ID。 此ID表示数据从源传输到Experience Platform的过程。 |
| `targetConnectionIds` | 目标连接ID 此ID表示数据在发送到Experience Platform后登陆的位置。 |
| `transformations[x].params.mappingId` | 映射ID。 |
| `transformations.name` | 摄取加密文件时，必须提供`Encryption`作为数据流的附加转换参数。 |
| `transformations[x].params.publicKeyId` | 您创建的公钥ID。 此ID是用来加密云存储数据的加密密钥对的一半。 |
| `scheduleParams.startTime` | 以纪元时间表示的数据流开始时间。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括： `once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 间隔指定两次连续流运行之间的周期。 间隔的值应为非零整数。 当频率设置为`once`时不需要间隔，其他频率值应大于或等于`15`。 |

+++

**响应**

+++查看示例响应

成功的响应返回已加密数据新创建的数据流的ID (`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!TAB 创建数据流以摄取加密和签名数据]

**请求**

+++查看示例请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data (with Sign Verification)",
    "description": "ACME Customer Data (with Sign Verification)",
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
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17",
                "signVerificationKeyId":"e31ae895-7896-469a-8e06-eb9207ddf1c2"
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
| `params.signVerificationKeyId` | 签名验证密钥ID与与Experience Platform共享Base64编码公钥后检索到的公钥ID相同。 |

+++

**响应**

+++查看示例响应

成功的响应返回已加密数据新创建的数据流的ID (`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!ENDTABS]

### 删除加密密钥 {#delete-encryption-keys}

要删除您的加密密钥，请向`/encryption/keys`端点发出DELETE请求，并提供您的公共密钥ID作为标头参数。

**API格式**

```http
DELETE /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**请求**

+++查看示例请求

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。

### 验证加密密钥 {#validate-encryption-keys}

要验证您的加密密钥，请向`/encryption/keys/validate/`端点发出GET请求，并提供要作为标头参数验证的公钥ID。

```http
GET /data/foundation/connectors/encryption/keys/validate/{PUBLIC_KEY_ID}
```

**请求**

+++查看示例请求

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/validate/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**响应**

成功的响应会返回确认ID有效或无效的消息。

>[!BEGINTABS]

>[!TAB 有效]

有效的公钥ID返回`Active`状态以及您的公钥ID。

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Active"
}
```

>[!TAB 无效]

无效的公钥ID返回状态`Expired`以及您的公钥ID。

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Expired"
}
```

>[!ENDTABS]


## 定期摄取的限制 {#restrictions-on-recurring-ingestion}

加密的数据摄取不支持在源中摄取循环或多级别文件夹。 所有加密文件必须包含在单个文件夹中。 不支持在单个源路径中包含多个文件夹的通配符。

以下是受支持的文件夹结构的示例，其中源路径为`/ACME-customers/*.csv.gpg`。

在此方案中，会将粗体格式的文件摄取到Experience Platform中。

* ACME客户
   * **文件1.csv.gpg**
   * File2.json.gpg
   * **文件3.csv.gpg**
   * File4.json
   * **文件5.csv.gpg**

以下是不受支持的文件夹结构的示例，其中源路径为`/ACME-customers/*`。

在此方案中，流运行将失败，并返回一则错误消息，指示无法从源复制数据。

* ACME客户
   * File1.csv.gpg
   * File2.json.gpg
   * 子文件夹1
      * File3.csv.gpg
      * File4.json.gpg
      * File5.csv.gpg
* ACME忠诚度
   * File6.csv.gpg


## 后续步骤

通过完成本教程，您已为云存储数据创建加密密钥对，并使用[!DNL Flow Service API]创建数据流以摄取加密数据。 有关数据流完整性、错误和量度的状态更新，请参阅[使用 [!DNL Flow Service] API](./monitor.md)监视数据流的指南。