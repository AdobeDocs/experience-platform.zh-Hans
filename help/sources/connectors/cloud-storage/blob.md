---
title: Azure Blob Source连接器概述
description: 了解如何将您的Azure Blob帐户连接到Experience Platform
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: f659d78eebc1c5e74021f9a41a2a489389a6588e
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---

# [!DNL Azure Blob Storage]源

[!DNL Azure Blob Storage]是由[!DNL Microsoft Azure]提供的基于云的对象存储服务。 它旨在存储大量非结构化数据，如文本、图像、视频、备份和日志。 您可以使用[!DNL Azure Blob Storage]存储和管理大量非结构化数据，如文档、图像、视频和音频文件。 它非常适合于备份和归档数据、支持灾难恢复以及处理分析的大数据工作负载。

使用[!DNL Azure Blob Storage]源连接您的帐户并将数据从[!DNL Azure Blob Storage]摄取到Adobe Experience Platform。

## 先决条件 {#prerequisites}

在将[!DNL Azure Blob Storage]帐户连接到Experience Platform之前，请阅读以下部分以完成先决条件设置。

### IP地址允许列表

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[列入允许列表IP地址以连接到Experience Platform](../../ip-address-allow-list.md)的指南。

>[!IMPORTANT]
>
>[!DNL Azure Blob]源不支持与Experience Platform的同区域连接。 如果您的[!DNL Azure]实例与Experience Platform使用相同的网络区域，则无法建立与Experience Platform源的连接。 目前，仅支持跨区域连接。

### 文件和目录的命名约束

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，它将自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 诸如`\uE000`之类的代码点虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

### 向Experience Platform验证[!DNL Azure Blob Storage] {#authentication}

您可以使用以下身份验证类型将您的[!DNL Azure Blob Storage]帐户连接到Experience Platform：

- **帐户密钥身份验证**：使用存储帐户的访问密钥进行身份验证并连接到您的[!DNL Azure Blob Storage]帐户。
- **共享访问签名(SAS)**：使用SAS URI为您的[!DNL Azure Blob Storage]帐户中的资源提供委派的、有时间限制的访问。
- **基于服务主体的身份验证**：使用Azure Active Directory (AAD)服务主体（客户端ID和密码）对您的Azure Blob存储帐户进行安全身份验证。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

为以下凭据提供值，以使用帐户密钥身份验证将您的[!DNL Azure Blob Storage]帐户连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `connectionString` | 存储帐户的[!DNL Azure Blob Storage]连接字符串。 此字符串包含验证和连接到[!DNL Azure Blob Storage]实例所需的信息。 示例格式： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` |
| `container` | 存储数据文件的[!DNL Azure Blob Storage]容器的名称。 容器组织一组Blob，类似于文件系统中的目录。 |
| `folderPath` | 指定容器中文件所在的路径。 这是容器内的可选子目录路径（虚拟文件夹）。 如果保留为空，则使用容器的根。 |
| `connectionSpec.id` | 连接规范ID返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 [!DNL Azure Blob Storage]的连接规范ID为`4c10e202-c428-4796-9208-5f1f5732b1cf`。 **注意**：只有在通过[!DNL Flow Service] API连接时才需要此凭据。 |

若要了解有关如何将帐户密钥身份验证与[!DNL Azure Blob Storage]一起使用的更多信息，请阅读官方的[Microsoft Azure身份验证指南](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#account-key-authentication)。

>[!TAB 共享访问签名]

为以下凭据提供值，以使用共享访问签名将您的[!DNL Azure Blob Storage]帐户连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `SasURI` | 共享访问签名URI，您可以将其用作连接帐户的替代身份验证类型。 SAS URI模式为： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`。 有关详细信息，请参阅[!DNL Azure]共享访问签名URI[上的此](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)文档。 |
| `container` | 存储数据文件的[!DNL Azure Blob Storage]容器的名称。 容器组织一组Blob，类似于文件系统中的目录。 |
| `folderPath` | 指定容器中文件所在的路径。 这是容器内的可选子目录路径（虚拟文件夹）。 如果保留为空，则使用容器的根。 |
| `connectionSpec.id` | 连接规范ID返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 [!DNL Azure Blob Storage]的连接规范ID为`4c10e202-c428-4796-9208-5f1f5732b1cf`。 **注意**：只有在通过[!DNL Flow Service] API连接时才需要此凭据。 |

要了解有关如何将共享访问签名与[!DNL Azure Blob Storage]一起使用的更多信息，请阅读官方的[Microsoft Azure身份验证指南](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)。

>[!TAB 基于服务主体的身份验证]

为以下凭据提供值，以使用基于服务主体的身份验证将您的[!DNL Azure Blob Storage]帐户连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `serviceEndpoint` | [!DNL Azure Blob Storage]帐户的终结点URL。 通常采用以下格式： `https://{ACCOUNT_NAME}.blob.core.windows.net`。 |
| `accountKind` | [!DNL Azure Blob Storage]帐户的类型。 通用值包括`StorageV2`、`BlobStorage`或`Storage`。 |
| `servicePrincipalId` | 用于身份验证的Azure Active Directory (AAD)服务主体的客户端/应用程序ID。 |
| `servicePrincipalKey` | 与Azure服务主体关联的客户端密钥或密码。 |
| `tenant` | 注册服务主体的Azure Active Directory (AAD)租户ID。 |
| `container` | 存储数据文件的Azure Blob存储容器的名称。 |
| `folderPath` | 指定容器中文件所在的路径。 这是容器内的可选子目录路径（虚拟文件夹）。 如果保留为空，则使用容器的根。 |
| `connectionSpec.id` | 连接规范ID返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 Azure Blob存储的连接规范ID为`4c10e202-c428-4796-9208-5f1f5732b1cf`。 **注意**：只有在通过[!DNL Flow Service] API连接时才需要此凭据。 |

若要了解有关如何将基于服务主体的身份验证与[!DNL Azure Blob Storage]结合使用的详细信息，请阅读官方的[Microsoft Azure身份验证指南](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#service-principal-authentication)。

>[!ENDTABS]

## 将[!DNL Azure Blob Storage]连接到[!DNL Experience Platform]

以下文档提供了有关如何使用API或用户界面将Azure Blob连接到Adobe Experience Platform的信息：

### 使用API

- [连接 [!DNL Azure Blob Storage] 到Experience Platform](../../tutorials/api/create/cloud-storage/blob.md)
- [使用流量服务API浏览云存储源的数据结构和内容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [将 [!DNL Azure Blob Storage] 连接到Experience Platform](../../tutorials/ui/create/cloud-storage/blob.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
