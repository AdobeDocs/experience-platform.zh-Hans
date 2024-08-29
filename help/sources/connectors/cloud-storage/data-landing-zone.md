---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Data Landing Zone Source
description: 了解如何将Data Landing Zone连接到Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecef17ed454c7b1f30543278bba6b0e3b70399da
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>此页面特定于Experience Platform中的[!DNL Data Landing Zone] *源*&#x200B;连接器。 有关连接到[!DNL Data Landing Zone] *目标*&#x200B;连接器的信息，请参阅[[!DNL Data Landing Zone] 目标文档页面](/help/destinations/catalog/cloud-storage/data-landing-zone.md)。

[!DNL Data Landing Zone]是由Adobe Experience Platform设置的[!DNL Azure Blob]存储接口，允许您访问安全、基于云的文件存储设施，以将文件导入Platform。 您有权访问每个沙盒一个[!DNL Data Landing Zone]容器，所有容器的总数据量以您的Platform产品和服务许可证提供的总数据为限。 所有Experience Platform客户都为每个沙盒配置一个[!DNL Data Landing Zone]容器。 您可以通过[!DNL Azure Storage Explorer]或命令行界面将文件读取和写入容器。

[!DNL Data Landing Zone]支持基于SAS的身份验证，其数据受标准[!DNL Azure Blob]存储安全机制的静态和传输保护。 基于SAS的身份验证允许您通过公共Internet连接安全地访问[!DNL Data Landing Zone]容器。 访问[!DNL Data Landing Zone]容器不需要更改网络，这意味着您不需要为网络配置任何允许列表或跨区域设置。 Experience Platform对上传到[!DNL Data Landing Zone]容器的所有文件和文件夹强制实施严格的七天过期时间。 所有文件和文件夹都会在七天后删除。

>[!NOTE]
>
>如果要从[!DNL Azure Data Factory]访问[!DNL Data Landing Zone]，则必须使用Experience Platform提供的[SAS凭据](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials)为[!DNL Data Landing Zone]创建链接的服务。 创建链接的服务后，您可以通过选择容器路径而不是默认的根路径来浏览[!DNL Data Landing Zone]。

## 文件和目录的命名约束

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，它将自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 诸如`\uE000`之类的代码点虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，还不允许使用某些ASCII或Unicode字符，如控制字符（如`0x00`到`0x1F`、`\u0081`等）。 有关HTTP/1.1中Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

## 管理数据登陆区域的内容{#manage-the-contents-of-your-data-landing-zone}

您可以使用[[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/)管理[!DNL Data Landing Zone]容器的内容。

在[!DNL Azure Storage Explorer] UI的左侧导航中选择连接图标。 出现&#x200B;**选择资源**&#x200B;窗口，为您提供连接选项。 选择&#x200B;**[!DNL Blob container]**&#x200B;以连接到[!DNL Data Landing Zone]。

![select-resource](../../images/tutorials/create/dlz/select-resource.png)

接下来，选择&#x200B;**共享访问签名URL (SAS)**&#x200B;作为连接方法，然后选择&#x200B;**下一步**。

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

选择连接方法后，必须提供与[!DNL Data Landing Zone]容器对应的&#x200B;**显示名称**&#x200B;和&#x200B;**[!DNL Blob]容器SAS URL**。

>[!TIP]
>
>您可以从平台UI中的源目录中检索[!DNL Data Landing Zone]凭据。

提供您的[!DNL Data Landing Zone] SAS URL，然后选择&#x200B;**下一步**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

此时将显示&#x200B;**摘要**&#x200B;窗口，其中提供了设置的概述，包括有关[!DNL Blob]端点和权限的信息。 准备就绪后，选择&#x200B;**连接**。

![摘要](../../images/tutorials/create/dlz/summary.png)

成功连接将更新包含[!DNL Data Landing Zone]容器的[!DNL Azure Storage Explorer]用户界面。

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

在将[!DNL Data Landing Zone]容器连接到[!DNL Azure Storage Explorer]后，您现在可以开始将文件上传到[!DNL Data Landing Zone]容器。 要上载，请选择&#x200B;**上载**，然后选择&#x200B;**上载文件**。

![上传](../../images/tutorials/create/dlz/upload.png)

选择要上载的文件后，您必须确定要将它上载为的[!DNL Blob]类型以及所需的目标目录。 完成后，选择&#x200B;**上传**。

| [!DNL Blob]类型 | 描述 |
| --- | --- |
| 块[!DNL Blob] | 块[!DNL Blobs]已针对以高效方式上载大量数据而优化。 块[!DNL Blobs]是[!DNL Data Landing Zone]的默认选项。 |
| 附加[!DNL Blob] | 已针对将数据附加到文件末尾而优化附加[!DNL Blobs]。 |

![上载文件](../../images/tutorials/create/dlz/upload-files.png)

## 使用命令行界面将文件上载到[!DNL Data Landing Zone]

您还可以使用设备的命令行界面并访问上传文件到[!DNL Data Landing Zone]。

### 使用Bash上载文件

以下示例使用Bash和cURL通过[!DNL Azure Blob Storage] REST API将文件上传到[!DNL Data Landing Zone]：

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

以下示例使用[!DNL Microsoft's] Python v12 SDK将文件上传到[!DNL Data Landing Zone]：

>[!TIP]
>
>虽然下面的示例使用完整的SAS URI连接到[!DNL Azure Blob]容器，但您可以使用其他方法和操作进行身份验证。 有关详细信息，请参阅Python v12 SDK](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python)上的此[[!DNL Microsoft] 文档。

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

### 使用[!DNL AzCopy]上载文件

以下示例使用[!DNL Microsoft's] [!DNL AzCopy]实用工具将文件上传到[!DNL Data Landing Zone]：

>[!TIP]
>
>当下面的示例使用`copy`命令时，您可以使用其他命令和选项使用[!DNL AzCopy]将文件上载到[!DNL Data Landing Zone]。 有关详细信息，请参阅此[[!DNL Microsoft AzCopy] 文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json)。

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## 将[!DNL Data Landing Zone]连接到[!DNL Platform]

以下文档提供了有关如何使用API或用户界面将数据从[!DNL Data Landing Zone]容器引入Adobe Experience Platform的信息。

### 使用API

- [使用流服务API创建 [!DNL Data Landing Zone] 源连接](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [使用UI连接 [!DNL Data Landing Zone] 到平台](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>使用[!DNL Data Landing Zone]连接到Experience Platform时，当前不支持专用链接。 唯一支持访问的方法是[此处](#manage-the-contents-of-your-data-landing-zone)列出的方法。

