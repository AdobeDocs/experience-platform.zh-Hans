---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 数据登陆区源
topic-legacy: overview
description: 了解如何将数据登陆区连接到Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 2a403be9a90d919aba2114f14c3cf64707b814b9
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform配置的存储界面，允许您访问基于云的安全文件存储工具，以将文件导入平台。 您有权访问 [!DNL Data Landing Zone] 容器，且所有容器中的数据总量仅限于随Platform产品和服务许可证提供的总数据量。 平台及其应用程序服务(例如 [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]和 [!DNL Real-time Customer Data Platform] 已配置一个 [!DNL Data Landing Zone] 每个沙盒的容器。 您可以通过 [!DNL Azure Storage Explorer] 或命令行界面。

[!DNL Data Landing Zone] 支持基于SAS的身份验证，其数据受标准保护 [!DNL Azure Blob] 储存安全机制在存放和运输中。 基于SAS的身份验证使您能够安全地访问 [!DNL Data Landing Zone] 容器。 您无需进行网络更改即可访问 [!DNL Data Landing Zone] 容器，这意味着您无需为网络配置任何允许列表或跨区域设置。 平台对上传到 [!DNL Data Landing Zone] 容器。 七天后会删除所有文件。

## 文件和目录的命名限制

以下是在命名云存储文件或目录时必须考虑的限制列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)。 如果提供，则会自动将其删除。
- 以下保留的URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 代码点，如 `\uE000`，但在NTFS文件名中有效，是无效的Unicode字符。 此外，某些ASCII或Unicode字符，如控制字符(例如 `0x00` to `0x1F`, `\u0081`等)，也不允许使用。 有关HTTP/1.1中控制Unicode字符串的规则，请参阅 [RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CLOK$、点(.)字符和两个点(.)字符。

## 管理 [!DNL Data Landing Zone]

您可以使用 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) 管理 [!DNL Data Landing Zone] 容器。

在 [!DNL Azure Storage Explorer] UI中，在左侧导航中选择连接图标。 的 **选择资源** 窗口，为您提供连接到的选项。 选择 **[!DNL Blob container]** 连接到 [!DNL Data Landing Zone].

![选择资源](../../images/tutorials/create/dlz/select-resource.png)

接下来，选择 **共享访问签名URL(SAS)** 作为连接方法，然后选择 **下一个**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

选择连接方法后，您必须接下来提供 **显示名称** 和 **[!DNL Blob]容器SAS URL** 与 [!DNL Data Landing Zone] 容器。

>[!TIP]
>
>您可以检索 [!DNL Data Landing Zone] 来自平台UI中源目录的凭据。

提供 [!DNL Data Landing Zone] SAS URL，然后选择 **下一个**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

的 **概要** 窗口，为您提供设置的概述，包括有关 [!DNL Blob] 端点和权限。 准备就绪后，选择 **连接**.

![摘要](../../images/tutorials/create/dlz/summary.png)

成功的连接会更新您的 [!DNL Azure Storage Explorer] UI [!DNL Data Landing Zone] 容器。

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

使用 [!DNL Data Landing Zone] 连接到的容器 [!DNL Azure Storage Explorer]，您现在可以开始将文件上传到 [!DNL Data Landing Zone] 容器。 要上传，请选择 **上传** 然后选择 **上传文件**.

![上传](../../images/tutorials/create/dlz/upload.png)

选择要上传的文件后，必须识别 [!DNL Blob] 键入要将其上载为的目标目录。 完成后，选择 **上传**.

| [!DNL Blob] 类型 | 描述 |
| --- | --- |
| 块 [!DNL Blob] | 块 [!DNL Blobs] 已进行优化，以便高效上传大量数据。 块 [!DNL Blobs] 是的默认选项 [!DNL Data Landing Zone]. |
| 附加 [!DNL Blob] | 附加 [!DNL Blobs] 优化了以将数据附加到文件末尾。 |

![上载文件](../../images/tutorials/create/dlz/upload-files.png)

## 将文件上传到 [!DNL Data Landing Zone] 使用命令行界面

您还可以使用设备的命令行界面，并将上传文件访问 [!DNL Data Landing Zone].

### 使用Bash上传文件

以下示例使用Bash和cURL将文件上传到 [!DNL Data Landing Zone] 和 [!DNL Azure Blob Storage] REST API:

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### 使用Python上传文件

以下示例使用 [!DNL Microsoft's] Python v12 SDK将文件上传到 [!DNL Data Landing Zone]:

>[!TIP]
>
>而以下示例使用完整的SAS URI连接到 [!DNL Azure Blob] 容器，则可以使用其他方法和操作进行身份验证。 请参阅 [[!DNL Microsoft] 关于Python v12 SDK的文档](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) 以了解更多信息。

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### 使用 [!DNL AzCopy]

以下示例使用 [!DNL Microsoft's] [!DNL AzCopy] 将文件上传到实用程序 [!DNL Data Landing Zone]:

>[!TIP]
>
>以下示例使用 `copy` 命令，可以使用其他命令和选项将文件上传到 [!DNL Data Landing Zone]，使用 [!DNL AzCopy]. 请参阅 [[!DNL Microsoft AzCopy] 文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) 以了解更多信息。

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## 连接 [!DNL Data Landing Zone] to [!DNL Platform]

以下文档提供了有关如何从 [!DNL Data Landing Zone] 容器到Adobe Experience Platform。

### 使用API

- [创建 [!DNL Data Landing Zone] 源连接（使用流量服务API）](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [连接 [!DNL Data Landing Zone] 到使用UI的平台](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
