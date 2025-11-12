---
title: Data Landing Zone Source
description: 了解如何将Data Landing Zone连接到Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>此页面特定于Experience Platform中的[!DNL Data Landing Zone] *源*&#x200B;连接器。 有关连接到[!DNL Data Landing Zone] *目标*&#x200B;连接器的信息，请参阅[[!DNL Data Landing Zone] 目标文档页面](/help/destinations/catalog/cloud-storage/data-landing-zone.md)。

[!DNL Data Landing Zone]是由Adobe Experience Platform设置的[!DNL Azure Blob]存储接口，允许您访问安全的基于云的文件存储设施，以将文件导入Experience Platform。 您有权访问每个沙盒一个[!DNL Data Landing Zone]容器，所有容器的总数据量以您的Experience Platform产品和服务许可证提供的总数据为限。 Experience Platform的所有客户都为每个沙盒配置一个[!DNL Data Landing Zone]容器。 您可以通过[!DNL Azure Storage Explorer]或命令行界面将文件读取和写入容器。

[!DNL Data Landing Zone]支持基于SAS的身份验证，其数据受标准[!DNL Azure Blob]存储安全机制的静态和传输保护。 基于SAS的身份验证允许您通过公共Internet连接安全地访问[!DNL Data Landing Zone]容器。 列入允许列表访问[!DNL Data Landing Zone]容器不需要更改网络，这意味着您不需要为网络配置任何或跨区域设置。 Experience Platform对上传到[!DNL Data Landing Zone]容器的所有文件和文件夹强制实施严格的七天过期时间。 所有文件和文件夹都会在七天后删除。

## 在Azure上为Experience Platform设置[!DNL Data Landing Zone]源 {#azure}

请按照以下步骤了解如何在Azure上为Experience Platform设置[!DNL Data Landing Zone]帐户。

>[!NOTE]
>
>如果要从[!DNL Data Landing Zone]访问[!DNL Azure Data Factory]，则必须使用Experience Platform提供的[!DNL Data Landing Zone]SAS凭据[为](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials)创建链接的服务。 创建链接的服务后，您可以通过选择容器路径而不是默认的根路径来浏览[!DNL Data Landing Zone]。

### 文件和目录的命名约束

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，它将自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 诸如`\uE000`之类的代码点虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，还不允许使用某些ASCII或Unicode字符，如控制字符（如`0x00`到`0x1F`、`\u0081`等）。 有关HTTP/1.1中Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

### 管理数据登陆区域的内容{#manage-the-contents-of-your-data-landing-zone}

您可以使用[[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/)管理[!DNL Data Landing Zone]容器的内容。

在[!DNL Azure Storage Explorer] UI的左侧导航中选择连接图标。 出现&#x200B;**选择资源**&#x200B;窗口，为您提供连接选项。 选择&#x200B;**[!DNL Blob container]**&#x200B;以连接到[!DNL Data Landing Zone]。

![Azure Explorer上的选择资源工作区。](../../images/tutorials/create/dlz/select-resource.png)

接下来，选择&#x200B;**共享访问签名URL (SAS)**&#x200B;作为连接方法，然后选择&#x200B;**下一步**。

![Azure Explorer上的选择连接方法，已选择共享访问签名。](../../images/tutorials/create/dlz/select-connection-method.png)

选择连接方法后，必须提供与&#x200B;**容器对应的**&#x200B;显示名称&#x200B;**[!DNL Blob]和**&#x200B;容器SAS URL[!DNL Data Landing Zone]。

>[!TIP]
>
>您可以从Experience Platform UI中的源目录中检索[!DNL Data Landing Zone]凭据。

提供您的[!DNL Data Landing Zone] SAS URL，然后选择&#x200B;**下一步**

![输入显示名称和SAS URL的Azure Explorer上的连接信息工作区。](../../images/tutorials/create/dlz/enter-connection-info.png)

此时将显示&#x200B;**摘要**&#x200B;窗口，其中提供了设置的概述，包括有关[!DNL Blob]端点和权限的信息。 准备就绪后，选择&#x200B;**连接**。

![重新获取资源连接设置的Azure资源管理器摘要工作区。](../../images/tutorials/create/dlz/summary.png)

成功连接将更新包含[!DNL Azure Storage Explorer]容器的[!DNL Data Landing Zone]用户界面。

![Azure Explorer上的数据登陆区域导航工作区。](../../images/tutorials/create/dlz/dlz-user-container.png)

在将[!DNL Data Landing Zone]容器连接到[!DNL Azure Storage Explorer]后，您现在可以开始将文件上传到[!DNL Data Landing Zone]容器。 要上载，请选择&#x200B;**上载**，然后选择&#x200B;**上载文件**。

![Azure Explorer的上传文件工作区。](../../images/tutorials/create/dlz/upload.png)

选择要上载的文件后，您必须确定要将它上载为的[!DNL Blob]类型以及所需的目标目录。 完成后，选择&#x200B;**上传**。

| [!DNL Blob]类型 | 描述 |
| --- | --- |
| 块[!DNL Blob] | 块[!DNL Blobs]已针对以高效方式上载大量数据而优化。 块[!DNL Blobs]是[!DNL Data Landing Zone]的默认选项。 |
| 附加[!DNL Blob] | 已针对将数据附加到文件末尾而优化附加[!DNL Blobs]。 |

![显示所选文件、Blob类型和目标类别的Azure资源管理器的“上载文件”窗口。](../../images/tutorials/create/dlz/upload-files.png)

### 使用命令行界面将文件上载到[!DNL Data Landing Zone]

您还可以使用设备的命令行界面并访问上传文件到[!DNL Data Landing Zone]。

### 使用Bash上载文件

以下示例使用Bash和cURL通过[!DNL Data Landing Zone] REST API将文件上传到[!DNL Azure Blob Storage]：

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
>虽然下面的示例使用完整的SAS URI连接到[!DNL Azure Blob]容器，但您可以使用其他方法和操作进行身份验证。 有关详细信息，请参阅Python v12 SDK[[!DNL Microsoft] 上的此](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python)文档。

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
>当下面的示例使用`copy`命令时，您可以使用其他命令和选项使用[!DNL Data Landing Zone]将文件上载到[!DNL AzCopy]。 有关详细信息，请参阅此[[!DNL Microsoft AzCopy] 文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json)。

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## 在Amazon Web Services上为Experience Platform设置[!DNL Data Landing Zone]源 {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)。

请按照以下步骤了解如何在Amazon Web Services (AWS)上为Experience Platform设置[!DNL Data Landing Zone]帐户。

### 列入允许列表在AWS上连接的IP地址

将源连接到AWS上的Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读[将IP地址列入允许列表到AWS](../../ip-address-allow-list.md)上的Experience Platform的指南。

### 设置AWS CLI并执行操作

- 请阅读有关[安装或更新到AWS CLI最新版本的指南](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)。

### 使用临时凭据配置AWS CLI

使用AWS `configure`命令设置带有访问密钥和会话令牌的CLI。

```shell
aws configure
```

出现提示时，输入以下值：

- AWS访问密钥ID： `{YOUR_ACCESS_KEY_ID}`
- AWS访问密钥： `{YOUR_SECRET_ACCESS_KEY}`
- 默认区域名称： `{YOUR_REGION}`（例如，`us-west-2`）
- 默认输出格式： `json`

接下来，设置会话令牌：

```shell
aws configure set aws_session_token your-session-token
```

### 处理[!DNL Amazon S3]上的文件

>[!BEGINTABS]

>[!TAB 将文件上传到Amazon S3]

模板：

```shell
aws s3 cp local-file-path s3://bucketName/dlzFolder/remote-file-Name
```

示例：

```shell
aws s3 cp example.txt s3://bucketName/dlzFolder/example.txt
```


>[!TAB 从Amazon S3]下载文件

模板：

```shell
aws s3 cp s3://bucketName/dlzFolder/remote-file local-file-path
```

示例：

```shell
aws s3 cp s3://bucketName/dlzFolder/example.txt example.txt
```

>[!ENDTABS]

### 使用您的[!DNL Data Landing Zone]凭据登录到AWS控制台

#### 提取您的凭据

首先，您必须获得以下内容：

- `awsAccessKeyId`
- `awsSecretAccessKey`
- `awsSessionToken`

#### 生成登录令牌

接下来，使用提取的凭据创建会话，并使用AWS联合端点生成登录令牌：

```py
import json
import requests
 
# Example DLZ response with credentials
response_json = '''{
    "credentials": {
        "awsAccessKeyId": "your-access-key",
        "awsSecretAccessKey": "your-secret-key",
        "awsSessionToken": "your-session-token"
    }
}'''
 
# Parse credentials
response_data = json.loads(response_json)
aws_access_key_id = response_data['credentials']['awsAccessKeyId']
aws_secret_access_key = response_data['credentials']['awsSecretAccessKey']
aws_session_token = response_data['credentials']['awsSessionToken']
 
# Create session dictionary
session = {
    'sessionId': aws_access_key_id,
    'sessionKey': aws_secret_access_key,
    'sessionToken': aws_session_token
}
 
# Generate the sign-in token
signin_token_url = "https://signin.aws.amazon.com/federation"
signin_token_payload = {
    "Action": "getSigninToken",
    "Session": json.dumps(session)
}
signin_token_response = requests.post(signin_token_url, data=signin_token_payload)
signin_token = signin_token_response.json()['SigninToken']
```

#### 构建AWS控制台登录URL

一旦您拥有登录令牌，即可在AWS控制台中构建用于将您记录并直接指向所需[!DNL Amazon S3]存储段的URL。

```py
from urllib.parse import quote
 
# Define the S3 bucket and folder path you want to access
bucket_name = "your-bucket-name"
bucket_path = "your-bucket-folder"
 
# Construct the destination URL
destination_url = f"https://s3.console.aws.amazon.com/s3/buckets/{bucket_name}?prefix={bucket_path}/&tab=objects"
 
# Create the final sign-in URL
signin_url = f"https://signin.aws.amazon.com/federation?Action=login&Issuer=YourAppName&Destination={quote(destination_url)}&SigninToken={signin_token}"
 
print(f"Sign-in URL: {signin_url}")
```

#### 访问AWS Console

最后，导航到生成的URL，以使用您的[!DNL Data Landing Zone]凭据直接登录AWS控制台，从而提供对[!DNL Amazon S3]存储段内特定文件夹的访问权限。 登录URL会将您直接转到该文件夹，确保您只能看到和管理允许的数据。

## 将[!DNL Data Landing Zone]连接到Experience Platform

>[!IMPORTANT]
>
>- 若要连接到源，您需要&#x200B;**[!UICONTROL View Sources]**&#x200B;和&#x200B;**[!UICONTROL Manage Sources]**&#x200B;访问控制权限。 有关详细信息，请阅读[访问控制概述](../../../access-control/home.md)或联系您的产品管理员以获取所需的权限。
>
>- 使用[!DNL Data Landing Zone]连接到Experience Platform时，当前不支持专用链接。 唯一支持访问的方法是[此处](#manage-the-contents-of-your-data-landing-zone)列出的方法。

以下文档提供了有关如何使用API或用户界面将数据从[!DNL Data Landing Zone]容器引入Adobe Experience Platform的信息。

### 使用API

- [使用流服务API创建 [!DNL Data Landing Zone] 源连接](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [使用UI连接 [!DNL Data Landing Zone] 到Experience Platform](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)

