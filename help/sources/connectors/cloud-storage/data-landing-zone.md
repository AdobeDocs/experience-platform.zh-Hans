---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 数据登陆区源
description: 了解如何将Data Landing Zone连接到Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: c2cc734d4a5c86fecbd0dabdfe63c896f0fe0f54
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>此页面特定于 [!DNL Data Landing Zone] *源* Experience Platform中的连接器。 有关连接到 [!DNL Data Landing Zone] *目标* 连接器，请参阅 [[!DNL Data Landing Zone] 目标文档页面](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform配置的存储界面，允许您访问安全的基于云的文件存储设施，将文件引入平台。 您有权访问一个 [!DNL Data Landing Zone] 容器数，所有容器的总数据量以您的Platform产品和服务许可证提供的总数据为限。 Platform及其应用程序服务的所有客户，例如 [!DNL Customer Journey Analytics]， [!DNL Journey Orchestration]， [!DNL Intelligent Services]、和 [!DNL Adobe Real-Time Customer Data Platform] 已配置一个 [!DNL Data Landing Zone] 每个沙盒的容器。 您可以通过读取文件并将文件写入容器 [!DNL Azure Storage Explorer] 或命令行界面。

[!DNL Data Landing Zone] 支持基于SAS的身份验证，其数据受标准保护 [!DNL Azure Blob] 存放安全机制处于闲置状态和在途中。 基于SAS的身份验证允许您安全地访问 [!DNL Data Landing Zone] 通过公共Internet连接实现的容器。 您无需更改网络即可访问 [!DNL Data Landing Zone] 容器，这意味着您无需为网络配置任何允许列表或跨区域设置。 Platform对上传到的所有文件实施严格的七天过期时间 [!DNL Data Landing Zone] 容器。 所有文件都会在七天后删除。

## 文件和目录的命名约束

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)。 如果提供，它将被自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 代码点如下 `\uE000`虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，还有一些ASCII或Unicode字符，如控制字符(如 `0x00` 到 `0x1F`， `\u0081`，等等)，也是不允许的。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅 [RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)，以及两个点字符(...)。

## 管理数据登陆区域的内容{#manage-the-contents-of-your-data-landing-zone}

您可以使用 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) 管理您的内容 [!DNL Data Landing Zone] 容器。

在 [!DNL Azure Storage Explorer] 在UI中，选择左侧导航中的连接图标。 此 **选择资源** 窗口出现，为您提供连接选项。 选择 **[!DNL Blob container]** 以连接到 [!DNL Data Landing Zone].

![选择资源](../../images/tutorials/create/dlz/select-resource.png)

接下来，选择 **共享访问签名URL (SAS)** 作为连接方法，然后选择 **下一个**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

选择连接方法后，必须提供 **显示名称** 和 **[!DNL Blob]容器SAS URL** 与您的 [!DNL Data Landing Zone] 容器。

>[!TIP]
>
>您可以检索 [!DNL Data Landing Zone] 来自Platform UI中源目录的凭据。

提供您的 [!DNL Data Landing Zone] SAS URL，然后选择 **下一个**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

此 **摘要** 窗口，为您提供设置的概述，包括有关您的设置的信息 [!DNL Blob] 端点和权限。 准备就绪后，选择 **Connect**.

![摘要](../../images/tutorials/create/dlz/summary.png)

成功的连接更新了您的 [!DNL Azure Storage Explorer] 包含您的UI [!DNL Data Landing Zone] 容器。

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

通过您的 [!DNL Data Landing Zone] 容器已连接到 [!DNL Azure Storage Explorer]，您现在可以开始将文件上传到 [!DNL Data Landing Zone] 容器。 要上传，请选择 **上传** 然后选择 **上传文件**.

![上传](../../images/tutorials/create/dlz/upload.png)

选择要上传的文件后，您必须识别 [!DNL Blob] 键入要上载为的目标目录和所需的目标目录。 完成后，选择 **上传**.

| [!DNL Blob] 类型 | 描述 |
| --- | --- |
| 块 [!DNL Blob] | 块 [!DNL Blobs] 已针对以高效方式上传大量数据进行了优化。 块 [!DNL Blobs] 是的默认选项 [!DNL Data Landing Zone]. |
| 附加 [!DNL Blob] | 附加 [!DNL Blobs] 已针对将数据附加到文件末尾进行了优化。 |

![upload-file](../../images/tutorials/create/dlz/upload-files.png)

## 将文件上传到 [!DNL Data Landing Zone] 使用命令行界面

您还可以使用设备的命令行界面并将上传文件访问到 [!DNL Data Landing Zone].

### 使用Bash上传文件

以下示例使用Bash和cURL将文件上传到 [!DNL Data Landing Zone] 使用 [!DNL Azure Blob Storage] REST API：

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

以下示例使用 [!DNL Microsoft's] Python v12 SDK将文件上传到 [!DNL Data Landing Zone]：

>[!TIP]
>
>虽然下面的示例使用完整的SAS URI连接到 [!DNL Azure Blob] 容器，则可以使用其他方法和操作进行身份验证。 查看此 [[!DNL Microsoft] Python v12 SDK上的文档](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) 了解更多信息。

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

### 上传文件，使用 [!DNL AzCopy]

以下示例使用 [!DNL Microsoft's] [!DNL AzCopy] 将文件上传到的实用程序 [!DNL Data Landing Zone]：

>[!TIP]
>
>虽然下面的示例使用的是 `copy` 命令，则可以使用其他命令和选项将文件上传到 [!DNL Data Landing Zone]，使用 [!DNL AzCopy]. 查看此 [[!DNL Microsoft AzCopy] 文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) 了解更多信息。

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Connect [!DNL Data Landing Zone] 到 [!DNL Platform]

以下文档提供了有关如何从获取数据的信息 [!DNL Data Landing Zone] 使用API或用户界面发送到Adobe Experience Platform的容器。

### 使用API

- [创建 [!DNL Data Landing Zone] 使用流服务API的源连接](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [Connect [!DNL Data Landing Zone] 使用UI到Platform](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>当前不支持使用连接到Experience Platform的专用链接 [!DNL Data Landing Zone]. 仅支持以下访问方法 [此处](#manage-the-contents-of-your-data-landing-zone).

