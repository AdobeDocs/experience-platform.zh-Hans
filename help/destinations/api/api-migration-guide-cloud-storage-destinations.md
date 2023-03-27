---
solution: Experience Platform
title: 云存储目标的API迁移指南
description: 了解在迁移到具有其他功能的新云存储目标卡时，激活云存储目标的工作流中所做的更改。
type: Tutorial
source-git-commit: 6ed78a96f099fb4552716ac4a598c43f4d65cf37
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 0%

---

# 云存储目标的API迁移指南

>[!IMPORTANT]
>
>* 本页面中描述的功能适用于购买了Real-Time CDP Prime和Ultimate软件包的客户。 有关更多信息，请联系您的Adobe代表。


## 迁移上下文 {#migration-context}

开始 [2022年10月](/help/release-notes/2022/october-2022.md#new-or-updated-destinations)，则在将文件导出为非Experience Platform时，可以使用新的文件导出功能访问增强的自定义功能：

* 其他 [文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* 能够通过 [新建映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* 能够选择 [文件类型](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) 的子项。
* 能够 [自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

下面列出的测试版云存储卡支持此功能：

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

请注意，当前在Experience PlatformUI中，您可以看到三个目标的两个并排目标卡。 如下所示 [!DNL Amazon S3] 旧版和新目标。 在所有情况下，卡片上都标有 **Beta** 是新的目标卡。

![并排视图中两个Amazon S3目标卡的图像。](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

虽然这些功能增强的目标最初是作为测试版提供的， *Adobe现在正在将所有Real-Time CDP客户转移到新的云存储目标*. 对于已在使用 [!DNL Amazon S3], [!DNL Azure Blob]或SFTP ，这意味着现有数据流将迁移到新信息卡。 有关迁移中特定更改的更多信息，请参阅。

## 本页面适用于的对象 {#who-this-applies-to}

如果您已在使用 [流量服务API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 要将配置文件导出到Amazon S3、Azure Blob或SFTP云存储目标，则此API迁移指南适用于您。

如果您的 [!DNL Amazon S3], [!DNL Azure Blob]，或Experience Platform中导出文件顶部的SFTP云存储位置，请注意，某些参数正在根据新卡的连接和流程规范以及映射步骤而发生更改。

例如，如果您使用脚本将目标数据流过滤到 [!DNL Amazon S3] 目标，基于 [!DNL Amazon S3] 目标位置，请注意连接规范将发生更改，因此您需要更新过滤器。

## 相关文档链接 {#relevant-documentation-links}

本节包含相关的API教程和参考文档，以了解将数据导出到云存储目标的增强功能。

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [将区段导出到云存储目标的API教程](/help/destinations/api/activate-segments-file-based-destinations.md)
* [目标流程服务API参考文档](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## 向后不兼容更改的摘要 {#summary-backwards-incompatible-changes}

迁移到新目标后，所有现有的数据流都将迁移到 [!DNL Amazon S3], [!DNL Azure Blob]，和SFTP目标现在将被分配新的target连接和基本连接。 配置文件映射步骤也会发生更改。 下面各个目标的部分概述了向后不兼容的更改。 另请查看 [目标术语表](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 有关下图中术语的详细信息。

![迁移指南概述图像](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### 对 [!DNL Amazon S3] 目标 {#changes-amazon-s3-destination}

API用户向后不兼容的更改已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| [!DNL Amazon S3] | 旧版 | 新建 |
|---------|----------|---------|
| 流量规范 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| 连接规范 | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

查看完整的旧版和新版基本连接以及目标连接示例 [!DNL Amazon S3] 中。 为创建基本连接所需的参数 [!DNL Amazon S3] 目标不会更改。

同样，创建目标连接所需的参数中也没有向后不兼容的更改。

>[!BEGINTABS]

>[!TAB 旧版基本连接和目标连接]

+++查看旧版 [!DNL base connection] 表示 [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "amazon-s3",
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"640418e2-0000-0200-0000-6359b9ef0000\"",
  "etag": "\"640418e2-0000-0200-0000-6359b9ef0000\""
}
```

+++

+++查看旧版 [!DNL target connection] 表示 [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "ee86d122-10d3-434b-81c7-7252e4d747a7",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "params": {
    "mode": "S3",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "etag": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "ee86d122-10d3-434b-81c7-7252e4d747a7",
      "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB 新的基本连接和目标连接]

+++查看新 [!DNL base connection] 表示 [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Amazon S3",
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"3708da21-0000-0200-0000-638940b10000\"",
  "etag": "\"3708da21-0000-0200-0000-638940b10000\""
}
```

+++

+++查看新 [!DNL target connection] 表示 [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12, 16-27"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "etag": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
      "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### 对 [!DNL Azure Blob] 目标 {#changes-azure-blob-destination}

API用户向后不兼容的更改已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| [!DNL Azure Blob] | 旧版 | 新建 |
|---------|----------|---------|
| 流量规范 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| 连接规范 | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

查看完整的旧版和新版基本连接以及目标连接示例 [!DNL Azure Blob] 中。 为Azure Blob目标创建基本连接所需的参数不会更改。

同样，创建目标连接所需的参数中也没有向后不兼容的更改。

>[!BEGINTABS]

>[!TAB 旧版基本连接和目标连接]

+++查看旧版 [!DNL base connection] 表示 [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "azure-blob",
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  }, 
  "version": "\"d000d23c-0000-0200-0000-6299051c0000\"",
  "etag": "\"d000d23c-0000-0200-0000-6299051c0000\""
}
```

+++

+++查看旧版 [!DNL target connection] 表示 [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "d10fcecf-9963-4062-820c-0f878be98805",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "params": {
    "mode": "AZURE_BLOB",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "etag": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d10fcecf-9963-4062-820c-0f878be98805",
      "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB 新的基本连接和目标连接]

+++查看新 [!DNL base connection] 表示 [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Azure Blob Storage",
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",      
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"4008a892-0000-0200-0000-6389890d0000\"",
  "etag": "\"4008a892-0000-0200-0000-6389890d0000\""
}
```

+++

+++查看新 [!DNL target connection] 表示 [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "1329d183-a3ee-4454-ab3f-e2388082bf29",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "etag": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "1329d183-a3ee-4454-ab3f-e2388082bf29",
      "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### 对SFTP目标进行向后不兼容的更改 {#changes-sftp-destination}

API用户向后不兼容的更改已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| SFTP | 旧版 | 新建 |
|---------|----------|---------|
| 流量规范 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 354d6aad-4754-46e4-a576-1b384561c440 |
| 连接规范 | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

除了上述更新的流程和连接规范外，创建SFTP基础连接时还需要更改参数。

* 以前，SFTP目标的基本连接需要 `host` 参数。 此参数现已重命名为 `domain`.
* 对于使用SSH密钥进行身份验证选项，基本连接中的身份验证参数需要 `port` 选项。 此参数现已弃用，不再需要。

在下面的选项卡中查看完整的旧版和新版SFTP基本连接以及目标连接示例，并突出显示更改的行。 为SFTP目标创建目标连接所需的参数不会更改。

>[!BEGINTABS]

>[!TAB 旧版基本连接和目标连接]

+++查看旧版 [!DNL base connection] （对于SFTP） — 密码身份验证

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "password": "<your-password>",
      "userName": "DPID12345",
      "host": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++查看旧版 [!DNL base connection] 表示 [!DNL SFTP - SSH key] 身份验证

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "sshKey": "<your-ssh-key>",
      "userName": "DPID12345",
      "port": 22
      "domain": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++查看旧版 [!DNL target connection] （对于SFTP）

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "params": {
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "etag": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
      "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB 新的基本连接和目标连接]

+++查看新 [!DNL base connection] 表示 [!DNL SFTP - password authentication]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "password": "<your-password>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++查看新 [!DNL base connection] 表示 [!DNL SFTP - SSH key] 身份验证

```json {line-numbers="true" start-line="1" highlight="5,12"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "sshKey": "<your-ssh-key>",
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++查看新 [!DNL target connection] （对于SFTP）

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "etag": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
      "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### 常见的向后不兼容的更改 [!DNL Amazon S3], [!DNL Azure Blob]和SFTP目标 {#changes-all-destinations}

所有三个目标中的配置文件选择器步骤都将替换为映射步骤，该步骤允许您根据需要重命名导出文件中的列标题。 请参阅下面的并排图像，左侧是旧属性选择器步骤，右侧是新映射步骤。

![迁移指南概述图像](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

请注意 `profileSelectors` 旧示例中的对象将替换为新 `profileMapping` 对象。

查找有关设置 `profileMapping` 对象 [将数据导出到云存储目标的API教程](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

>[!BEGINTABS]

>[!TAB 旧转换参数]

+++查看旧转换参数的示例

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "profileSelectors": {
    "selectors": [
      {
        "type": "JSON_PATH",
        "value": {
          "path": "CORE",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "CORE",
            "destination": "CORE",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "CORE",
            "destinationXdmPath": "CORE"
          },
          "identity": {
            "namespace": "CORE"
          }
        }
      },
      ...
      {
        "type": "JSON_PATH",
        "value": {
          "path": "segmentMembership.status",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "segmentMembership.status",
            "destination": "segmentMembership.status",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "segmentMembership.status",
            "destinationXdmPath": "segmentMembership.status"
          }
        }
      }
    ],
    "mandatoryFields": [
      "CORE",
      "person.name.lastName",
      "personalEmail.address"
    ],
    "primaryFields": [
      {
        "identityNamespace": "CORE",
        "fieldType": "IDENTITY"
      }
    ]
  }
}
```

+++

>[!TAB 新的转换参数]

+++查看迁移后转换参数的示例

请注意下面的配置示例中如何 `profileSelectors` 字段已被替换为 `profileMapping` 对象。

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "mandatoryFields": [
    "CORE",
    "person_name_lastName",
    "personalEmail_address"
  ],
  "primaryFields": [
    {
      "identityNamespace": "CORE",
      "fieldType": "IDENTITY"
    }
  ],
  "identityMapping": {
    "mappings": []
  },
  "profileMapping": {
    "mappingId": "40dfd952fe09498ba65145c7a5de3e07",
    "mappingVersion": 0
  },
  "attributeMapping": {}
}
```

+++

>[!ENDTABS]

## 迁移时间轴和操作项 {#timeline-and-action-items}

将旧数据流迁移到 [!DNL Amazon S3], [!DNL Azure Blob]，且SFTP目标将在贵组织准备好迁移后立即发生，并且迁移时间不得晚于 **2023年6月30日**.

当迁移日期临近时，您将收到来自Adobe的提醒电子邮件。 在准备过程中，请阅读下面的操作项目部分，以便为迁移做好准备。

### 操作项 {#action-items}

为迁移 [!DNL Amazon S3], [!DNL Azure Blob]，以及将SFTP云存储目标存储到新信息卡，请按照以下建议准备更新脚本和自动API调用。

1. 为任何现有的 [!DNL Amazon S3], [!DNL Azure Blob]，或SFTP云存储目标。 任何利用旧连接规范或流程规范的自动API调用或脚本都需要更新为新的连接规范或流程规范。
2. 在6月30日之前更新脚本时，请联系您的Adobe客户代表。
3. 例如， `targetConnectionSpecId` 可用作确定数据流是否已迁移到新目标卡的标记。 您可以使用 `if` 在 `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` 并确定您的数据流是否已迁移。 您可以在此页面上每个目标的特定部分中看到旧连接规范ID和新连接规范ID。
4. 您的Adobe客户团队将联系有关数据流何时迁移的更多信息。
5. 6月30日之后，所有数据流都将迁移。 现在，所有现有的数据流都将具有新的流实体（连接规范、流规范、基本连接和目标连接）。 对于使用旧版流实体的任何脚本或API调用，都将停止工作。

## 其他迁移注意事项 {#other-considerations}

请注意，在迁移期间或迁移后，对现有的导出计划没有影响。

## 后续步骤 {#next-steps}

通过阅读本页，您现在知道您是否需要采取任何措施来为云存储目标的迁移做好准备。 在设置基于API的工作流以将文件从Experience Platform导出到首选的云存储目标时，您还知道要引用哪些文档页面。 接下来，您可以查看 [将数据导出到云存储目标](/help/destinations/api/activate-segments-file-based-destinations.md).