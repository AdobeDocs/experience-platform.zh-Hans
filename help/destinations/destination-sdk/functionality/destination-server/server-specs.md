---
description: 了解如何通过“/authoring/destination-servers”端点在Adobe Experience Platform Destination SDK中配置目标服务器规范。
title: 使用Destination SDK创建的目标的服务器规范
exl-id: 62202edb-a954-42ff-9772-863cea37a889
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 3%

---

# 使用Destination SDK创建的目标的服务器规范

目标服务器规范定义将从Adobe Experience Platform接收数据的目标平台的类型，以及平台与您的目标之间的通信参数。 例如：

* A [流式](#streaming-example) 目标服务器规范定义将从Platform接收HTTP消息的HTTP服务器端点。 要了解如何配置对端点的HTTP调用的格式，请阅读 [模板规范](templating-specs.md) 页面。
* An [Amazon S3](#s3-example) 目标服务器规范定义 [!DNL S3] Platform将导出文件的存储段名称和路径。
* An [SFTP](#sftp-example) 目标服务器规范定义Platform将导出文件的SFTP服务器的主机名、根目录、通信端口和加密类型。

要了解此组件在何处适合使用Destination SDK创建的集成，请参阅中的图表 [配置选项](../configuration-options.md) 文档或参阅以下目标配置概述页面：

* [使用Destination SDK配置流目标](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [使用Destination SDK配置基于文件的目标](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

您可以通过以下方式配置目标服务器规范 `/authoring/destination-servers` 端点。 有关详细的API调用示例，请参阅以下API参考页面，您可以在其中配置此页面中显示的组件。

* [创建目标服务器配置](../../authoring-api/destination-server/create-destination-server.md)
* [更新目标服务器配置](../../authoring-api/destination-server/update-destination-server.md)

此页显示Destination SDK支持的所有目标服务器类型及其所有配置参数。 在创建目标时，请将参数值替换为您自己的参数值。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 是 |

时间 [创建](../../authoring-api/destination-server/create-destination-server.md) 或 [正在更新](../../authoring-api/destination-server/update-destination-server.md) 目标服务器，请使用本页中介绍的其中一个服务器类型配置。 根据您的集成要求，请确保将这些示例中的示例参数值替换为您自己的示例参数值。

## 硬编码字段与模板化字段 {#templatized-fields}

通过Destination SDK创建目标服务器时，您可以通过将配置参数硬编码到配置中或使用模板化字段来定义配置参数值。 利用模板化的字段，可从Platform UI读取用户提供的值。

目标服务器参数有两个可配置的字段。 这些选项指示您使用的是硬编码值还是模板化值。

| 参数 | 类型 | 描述 |
|---|---|---|
| `templatingStrategy` | 字符串 | *必需.* 定义是否通过提供的硬编码值 `value` 字段或UI中用户可配置的值。 支持的值： <ul><li>`NONE`：当通过硬编码来硬编码参数值时，请使用此值 `value` 参数（请参阅下一行）。 示例:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`：如果您希望用户在UI中提供参数值，请使用此值。 示例：`"value": "{{customerData.bucket}}"`。 </li></ul> |
| `value` | 字符串 | *必需*. 定义参数值。 支持的值类型： <ul><li>**硬编码值**：使用硬编码值(例如 `"value": "my-storage-bucket"`)。 硬编码值时， `templatingStrategy` 应始终设置为 `NONE`.</li><li>**模板化值**：使用模板化的值(例如 `"value": "{{customerData.bucket}}"`)时，您需要用户在UI中提供参数值。 使用模板化值时， `templatingStrategy` 应始终设置为 `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### 何时使用硬编码字段与模板化字段

根据要创建的集成类型，硬编码字段和模板化字段在Destination SDK中具有各自的用途。

**无需用户输入即可连接到目标**

当用户 [连接到您的目标](../../../ui/connect-destination.md) 在Platform UI中，您可能希望在不输入目标连接进程的情况下对其进行处理。

为此，您可以在服务器规范中对目标平台连接参数进行硬编码。 在目标服务器配置中使用硬编码参数值时，无需用户输入即可处理Adobe Experience Platform与目标平台之间的连接。

在以下示例中，合作伙伴使用创建数据登陆区目标服务器 `path.value` 字段进行了硬编码。

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

因此，当用户浏览 [目标连接教程](../../../ui/connect-destination.md)，他们不会看到 [身份验证步骤](../../../ui/connect-destination.md#authenticate). 相反，身份验证由Platform处理，如下图所示。

![显示Platform与DLZ目标之间身份验证屏幕的Ui图像。](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**使用用户输入连接到目标**

当在Platform UI中根据特定用户输入（例如选择API端点或提供字段值）建立Platform与您的目标之间的连接时，您可以使用服务器规范中的模板化字段读取用户输入并连接到您的目标平台。

在下面的示例中，合作伙伴创建 [实时（流）](#streaming-example) 集成和 `url.value` 字段使用模板化参数 `{{customerData.region}}` 根据用户输入对API端点的一部分进行个性化。

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

要允许用户选择来自Platform UI的值，请 `region` 参数也必须在以下位置定义： [目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md) 作为客户数据字段，如下所示：

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

因此，当用户浏览 [目标连接教程](../../../ui/connect-destination.md)，用户必须先选择区域，然后才能连接到目标平台。 当它们连接到目标时，模板化字段 `{{customerData.region}}` 将替换为用户在UI中选择的值，如下图所示。

![显示具有区域选择器的目标连接屏幕的Ui图像。](../../assets/functionality/destination-server/server-spec-template-region.png)

## 实时（流）目标服务器 {#streaming-example}

使用此目标服务器类型，您可以通过HTTP请求将数据从Adobe Experience Platform导出到您的目标。 服务器配置包含有关接收消息的服务器（您侧的服务器）的信息。

此过程会将用户数据作为一系列HTTP消息传送到您的目标平台。 以下参数构成了HTTP服务器规格模板。

以下示例显示了实时（流）目标的目标服务器配置示例。

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | *必需.* 表示服务器的友好名称，仅对Adobe可见。 合作伙伴或客户看不到此名称。 示例：`Moviestar destination server`。 |
| `destinationServerType` | 字符串 | *必需.* 将此项设置为 `URL_BASED` 适用于流式传输目标。 |
| `templatingStrategy` | 字符串 | *必需.* <ul><li>使用 `PEBBLE_V1` 如果您在中使用模板化字段而不是硬编码值， `value` 字段。 如果您拥有如下端点，请使用此选项： `https://api.moviestar.com/data/{{customerData.region}}/items`，用户必须从Platform UI中选择端点区域。 </li><li> 使用 `NONE` 如果Adobe端不需要模板化转换，例如，如果您具有如下端点： `https://api.moviestar.com/data/items` </li></ul> |
| `value` | 字符串 | *必需.* 填写Experience Platform应连接到的API端点的地址。 |

{style="table-layout:auto"}

## [!DNL Amazon S3] 目标服务器 {#s3-example}

使用此目标服务器，您可以将包含Adobe Experience Platform数据的文件导出到Amazon S3存储空间。

以下示例显示了Amazon S3目标的目标服务器配置示例。

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标服务器的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 要将文件导出到 [!DNL Amazon S3] 存储桶，将此项设置为 `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字符串 | *必需*. 根据中使用的值类型设置此值 `bucket.value` 字段。<ul><li>如果您希望用户在Experience PlatformUI中输入自己的存储段名称，请将此值设置为 `PEBBLE_V1`. 在这种情况下，您必须将 `value` 字段以从中读取值 [客户数据字段](../destination-configuration/customer-data-fields.md) 由用户填写。 上述示例中显示了此用例。</li><li>如果您在集成中使用硬编码存储段名称，例如 `"bucket.value":"MyBucket"`，然后将此值设置为 `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | 字符串 | 的名称 [!DNL Amazon S3] 要由此目标使用的存储桶。 这可以是模板化字段，它将从 [客户数据字段](../destination-configuration/customer-data-fields.md) 填入（如上面的示例所示）或硬编码值，如 `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | 字符串 | *必需*. 根据中使用的值类型设置此值 `path.value` 字段。<ul><li>如果您希望用户在Experience PlatformUI中输入自己的路径，则将此值设置为 `PEBBLE_V1`. 在这种情况下，您必须将 `path.value` 字段以从中读取值 [客户数据字段](../destination-configuration/customer-data-fields.md) 由用户填写。 上述示例中显示了此用例。</li><li>如果您使用的是硬编码路径进行集成，例如 `"bucket.value":"/path/to/MyBucket"`，然后将此值设置为 `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | 字符串 | 的路径 [!DNL Amazon S3] 要由此目标使用的存储桶。 这可以是模板化字段，它将从 [客户数据字段](../destination-configuration/customer-data-fields.md) 填入（如上面的示例所示）或硬编码值，如 `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] 目标服务器 {#sftp-example}

使用此目标服务器，您可以将包含Adobe Experience Platform数据的文件导出到 [!DNL SFTP] 存储服务器。

以下示例显示了SFTP目标的目标服务器配置示例。

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标服务器的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 要将文件导出到 [!DNL SFTP] 目标，将此项设置为 `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | 字符串 | *必需*. 根据中使用的值类型设置此值 `rootDirectory.value` 字段。<ul><li>如果您希望用户在Experience PlatformUI中输入自己的根目录路径，请将此值设置为 `PEBBLE_V1`. 在这种情况下，您必须将 `rootDirectory.value` 字段以从中读取用户提供的值 [客户数据字段](../destination-configuration/customer-data-fields.md) 由用户填写。 上述示例中显示了此用例。</li><li>如果您使用硬编码的根目录路径进行集成，例如 `"rootDirectory.value":"Storage/MyDirectory"`，然后将此值设置为 `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | 字符串 | 将托管导出文件的目录的路径。 这可以是模板化字段，它将从 [客户数据字段](../destination-configuration/customer-data-fields.md) 填入（如上面的示例所示）或硬编码值，如 `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | 字符串 | *必需*. 根据中使用的值类型设置此值 `hostName.value` 字段。<ul><li>如果您希望用户在Experience PlatformUI中输入他们自己的主机名，请将此值设置为 `PEBBLE_V1`. 在这种情况下，您必须将 `hostName.value` 字段以从中读取用户提供的值 [客户数据字段](../destination-configuration/customer-data-fields.md) 由用户填写。 上述示例中显示了此用例。</li><li>如果您在集成中使用硬编码主机名，例如 `"hostName.value":"my.hostname.com"`，然后将此值设置为 `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | 字符串 | SFTP服务器的主机名。 这可以是模板化字段，它将从 [客户数据字段](../destination-configuration/customer-data-fields.md) 填入（如上面的示例所示）或硬编码值，如 `"hostName.value":"my.hostname.com"`. |
| `port` | 整数 | SFTP文件服务器端口。 |
| `encryptionMode` | 字符串 | 指示是否使用文件加密。 支持的值： <ul><li>PGP</li><li>None</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS])目标服务器 {#adls-example}

使用此目标服务器，您可以将包含Adobe Experience Platform数据的文件导出到 [!DNL Azure Data Lake Storage] 帐户。

以下示例显示了 [!DNL Azure Data Lake Storage] 目标。

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对象 [!DNL Azure Data Lake Storage] 目标，将其设置为 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字符串 | *必需*. 根据中使用的值类型设置此值 `path.value` 字段。<ul><li>如果您希望用户输入他们的 [!DNL ADLS] Experience PlatformUI中的文件夹路径，将此值设置为 `PEBBLE_V1`. 在这种情况下，您必须将 `path.value` 字段以从中读取值 [客户数据字段](../destination-configuration/customer-data-fields.md) 由用户填写。 上述示例中显示了此用例。</li><li>如果您使用的是硬编码路径进行集成，例如 `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`，然后将此值设置为 `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | 字符串 | 您的路径 [!DNL ADLS] 存储文件夹。 这可以是模板化字段，它将从 [客户数据字段](../destination-configuration/customer-data-fields.md) 填入（如上面的示例所示）或硬编码值，如 `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] 目标服务器 {#blob-example}

使用此目标服务器，您可以将包含Adobe Experience Platform数据的文件导出到 [!DNL Azure Blob Storage] 容器。

以下示例显示了 [!DNL Azure Blob Storage] 目标。

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对象 [!DNL Azure Blob Storage] 目标，将其设置为 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字符串 | *必需*. 根据中使用的值类型设置此值 `path.value` 字段。<ul><li>如果您希望用户输入他们自己的 [!DNL Azure Blob] [存储帐户URI](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) 在Experience PlatformUI中，将此值设置为 `PEBBLE_V1`. 在这种情况下，您必须将 `path.value` 字段以从中读取值 [客户数据字段](../destination-configuration/customer-data-fields.md) 由用户填写。 上述示例中显示了此用例。</li><li>如果您使用的是硬编码路径进行集成，例如 `"path.value": "https://myaccount.blob.core.windows.net/"`，然后将此值设置为 `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | 字符串 | 您的路径 [!DNL Azure Blob] 存储。 这可以是模板化字段，它将从 [客户数据字段](../destination-configuration/customer-data-fields.md) 填入（如上面的示例所示）或硬编码值，如 `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字符串 | *必需*. 根据中使用的值类型设置此值 `container.value` 字段。<ul><li>如果您希望用户输入他们自己的 [!DNL Azure Blob] [容器名称](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) 在Experience PlatformUI中，将此值设置为 `PEBBLE_V1`. 在这种情况下，您必须将 `container.value` 字段以从中读取值 [客户数据字段](../destination-configuration/customer-data-fields.md) 由用户填写。 上述示例中显示了此用例。</li><li>如果您在集成中使用硬编码的容器名称，例如 `"path.value: myContainer"`，然后将此值设置为 `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | 字符串 | 要用于此目标的Azure Blob存储容器的名称。 这可以是模板化字段，它将从 [客户数据字段](../destination-configuration/customer-data-fields.md) 填入（如上面的示例所示）或硬编码值，如 `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ])目标服务器 {#dlz-example}

使用此目标服务器，您可以将包含Platform数据的文件导出到 [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) 存储。

以下示例显示了 [!DNL Data Landing Zone] ([!DNL DLZ])目标。

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对象 [!DNL Data Landing Zone] 目标，将其设置为 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 字符串 | *必需*. 根据中使用的值类型设置此值 `path.value` 字段。<ul><li>如果您希望用户输入他们自己的 [!DNL Data Landing Zone] account在Experience PlatformUI中，将此值设置为 `PEBBLE_V1`. 在这种情况下，您必须将 `path.value` 字段以从中读取值 [客户数据字段](../destination-configuration/customer-data-fields.md) 由用户填写。 上述示例中显示了此用例。</li><li>如果您使用的是硬编码路径进行集成，例如 `"path.value": "https://myaccount.blob.core.windows.net/"`，然后将此值设置为 `NONE`. |
| `fileBasedDlzDestination.path.value` | 字符串 | 将托管导出文件的目标文件夹的路径。 |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] 目标服务器 {#gcs-example}

使用此目标服务器，您可以将包含Platform数据的文件导出到 [!DNL Google Cloud Storage] 帐户。

以下示例显示了 [!DNL Google Cloud Storage] 目标。

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目标连接的名称。 |
| `destinationServerType` | 字符串 | 根据目标平台设置此值。 对象 [!DNL Google Cloud Storage] 目标，将其设置为 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字符串 | *必需*. 根据中使用的值类型设置此值 `bucket.value` 字段。<ul><li>如果您希望用户输入他们自己的 [!DNL Google Cloud Storage] 在Experience PlatformUI中存储段名称，将此值设置为 `PEBBLE_V1`. 在这种情况下，您必须将 `bucket.value` 字段以从中读取值 [客户数据字段](../destination-configuration/customer-data-fields.md) 由用户填写。 上述示例中显示了此用例。</li><li>如果您在集成中使用硬编码存储段名称，例如 `"bucket.value": "my-bucket"`，然后将此值设置为 `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字符串 | 的名称 [!DNL Google Cloud Storage] 要由此目标使用的存储桶。 这可以是模板化字段，它将从 [客户数据字段](../destination-configuration/customer-data-fields.md) 填入（如上面的示例所示）或硬编码值，如 `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字符串 | *必需*. 根据中使用的值类型设置此值 `path.value` 字段。<ul><li>如果您希望用户输入他们自己的 [!DNL Google Cloud Storage] Experience PlatformUI中的存储段路径，请将此值设置为 `PEBBLE_V1`. 在这种情况下，您必须将 `path.value` 字段以从中读取值 [客户数据字段](../destination-configuration/customer-data-fields.md) 由用户填写。 上述示例中显示了此用例。</li><li>如果您使用的是硬编码路径进行集成，例如 `"path.value": "/path/to/my-bucket"`，然后将此值设置为 `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字符串 | 的路径 [!DNL Google Cloud Storage] 此目标使用的文件夹。 这可以是模板化字段，它将从 [客户数据字段](../destination-configuration/customer-data-fields.md) 填入（如上面的示例所示）或硬编码值，如 `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

阅读本文后，您应该更好地了解什么是目标服务器规范，以及如何对其进行配置。

要了解有关其他目标服务器组件的更多信息，请参阅以下文章：

* [模板规范](templating-specs.md)
* [消息格式](message-format.md)
* [文件格式配置](file-formatting.md)
