---
solution: Experience Platform
title: 使用流服务API将受众激活到基于文件的目标
description: 了解如何使用流服务API将包含合格配置文件的文件导出到云存储目标。
type: Tutorial
exl-id: 62028c7a-3ea9-4004-adb7-5e27bbe904fc
source-git-commit: df7b9bb0c5dc4348e8be7a0ea93296e24bc0fb1d
workflow-type: tm+mt
source-wordcount: '4760'
ht-degree: 3%

---

# 使用流服务API将受众激活到基于文件的目标

使用增强的文件导出功能，可在导出文件时访问增强的自定义功能Experience Platform：

* 额外的[文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。
* 可通过[改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)在您导出的文件中设置自定义文件头。
* 能够选择 [文件类型](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) 导出文件的属性。
* [能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

以下列出的六个云存储卡支持此功能：

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

本文说明了使用 [流服务API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 以将符合条件的配置文件从Adobe Experience Platform导出到上面链接的其中一个云存储位置。

>[!TIP]
>
>您还可以使用Experience Platform用户界面将用户档案导出到云存储目标。 阅读 [激活基于文件的目标教程](/help/destinations/ui/activate-batch-profile-destinations.md) 以了解更多信息。

<!--

## API users migration {#api-migration}

If you were already using the Flow Service API to export profiles to the Amazon S3, Azure Blob, or SFTP cloud storage destinations, read the [API migration guide](/help/destinations/api/api-migration-guide-cloud-storage-destinations.md) for necessary migration steps as Adobe transitions users from the legacy destinations to the new destinations. 

-->

## 快速入门 {#get-started}

![用于激活受众的步骤，其中突出显示用户正在执行的当前步骤](/help/destinations/assets/api/file-based-segment-export/segment-export-overview.png)

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md)： [!DNL Adobe Experience Platform Segmentation Service] 允许您在中构建受众并生成受众 [!DNL Adobe Experience Platform] 来自您的 [!DNL Real-Time Customer Profile] 数据。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便将数据激活到Platform中基于文件的目标。

### 所需的权限 {#permissions}

要导出用户档案，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

### 正在读取示例 API 调用 {#reading-sample-api-calls}

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关文档中用于示例API调用的惯例的信息，请参阅 [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集必需标题和可选标题的值 {#gather-values-headers}

为了调用 [!DNL Platform] API，您必须先完成 [Experience Platform身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

中的资源 [!DNL Experience Platform] 可以隔离到特定的虚拟沙箱。 在请求中 [!DNL Platform] API中，您可以指定将在其中执行操作的沙盒的名称和ID。 这些是可选参数。

* x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Experience Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

包含有效负载的所有请求(`POST`， `PUT`， `PATCH`)需要额外的媒体类型标头：

* 内容类型： `application/json`

### API参考文档 {#api-reference-documentation}

您可以在本教程中找到所有API操作的随附参考文档。 请参阅 [Adobe Developer网站上的流服务 — 目标API文档](https://developer.adobe.com/experience-platform-apis/references/destinations/). 我们建议您并行使用此教程和API参考文档。

### 术语表 {#glossary}

有关在此API教程中遇到的术语的描述，请参阅 [词汇表部分](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) API参考文档的URL名称。

## 选择要从中导出受众的目标 {#select-destination}

![用于激活受众的步骤，其中突出显示用户正在执行的当前步骤](/help/destinations/assets/api/file-based-segment-export/step1.png)

在开始导出用户档案的工作流之前，请确定要将受众导出到的目标的连接规范和流量规范ID。 请参考下表。

| 目标 | 连接规范 | 流量规范 |
---------|----------|---------|
| Amazon S3 | `4fce964d-3f37-408f-9778-e597338a21ee` | `1a0514a6-33d4-4c7f-aff8-594799c47549` |
| Azure Blob Storage | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `752d422f-b16f-4f0d-b1c6-26e448e3b388` |
| Azure Data Lake Gen 2(ADLS Gen2) | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| 数据登陆区(DLZ) | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| Google 云存储 | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `fd36aaa4-bf2b-43fb-9387-43785eeeb799` |

{style="table-layout:auto"}

在本教程的后续步骤中，您需要这些ID来构建各种流服务实体。 您还需要引用连接规范本身的某些部分来设置某些实体，以便从流服务API中检索连接规范。 请参阅下面的示例，以了解如何检索表中所有目标的连接规范：

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

+++Retrieve [!DNL connection spec] 对象 [!DNL Amazon S3]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**响应**

+++[!DNL Amazon S3]  — 连接规范

```json
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Blob存储]

**请求**

+++Retrieve [!DNL connection spec] 对象 [!DNL Azure Blob Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/6d6b59bf-fb58-4107-9064-4d246c0e5bb2' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**响应**

+++[!DNL Azure Blob Storage] — [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**请求**

+++Retrieve [!DNL connection spec] 对象 [!DNL Azure Data Lake Gen 2(ADLS Gen2])

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be2c3209-53bc-47e7-ab25-145db8b873e1' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**响应**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] — [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB 数据登陆区(DLZ)]

**请求**

+++Retrieve [!DNL connection spec] 对象 [!DNL Data Landing Zone(DLZ)]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/10440537-2a7b-4583-ac39-ed38d4b848e8' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**响应**

+++[!DNL Data Landing Zone(DLZ)] — [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Google云存储]

**请求**

+++Retrieve [!DNL connection spec] 对象 [!DNL Google Cloud Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/c5d93acb-ea8b-4b14-8f53-02138444ae99' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**响应**

+++[!DNL Google Cloud Storage] — [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB SFTP]

**请求**

+++Retrieve [!DNL connection spec] 对于SFTP

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/36965a81-b1c6-401b-99f8-22508f1e6a26' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**响应**

+++SFTP - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!ENDTABS]

请按照以下步骤设置指向云存储目标的受众导出数据流。 对于某些步骤，不同云存储目标之间的请求和响应会有所不同。 在这些情况下，使用页面上的选项卡可检索特定于要连接并将受众导出到的目标的请求和响应。 请确保使用正确的 `connection spec` 和 `flow spec` （对于您正在配置的目标）。

## 创建源连接 {#create-source-connection}

![用于激活受众的步骤，其中突出显示用户正在执行的当前步骤](/help/destinations/assets/api/file-based-segment-export/step2.png)

在决定要将受众导出到哪个目标后，您需要创建源连接。 此 [源连接](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 表示与内部 [Experience Platform配置文件存储](/help/profile/home.md#profile-data-store).

>[!BEGINSHADEBOX]

**请求**

+++创建源连接 — 请求

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除内联注释。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
   "name":"Connect to Profile store",
   "description":"Optional",
   "connectionSpec":{
      "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1", // this connection spec ID is always the same for Source Connections
      "version":"1.0"
   }
}'
```

+++

**响应**

+++创建源连接 — 响应

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

成功的响应会返回ID (`id`)和 `etag`. 记下源连接ID，因为稍后创建数据流时会需要它。

## 创建基本连接 {#create-base-connection}

![用于激活受众的步骤，其中突出显示用户正在执行的当前步骤](/help/destinations/assets/api/file-based-segment-export/step3.png)

A [基本连接](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 安全地存储到目标的凭据。 根据目标类型，对该目标进行身份验证所需的凭据可能有所不同。 要查找这些验证参数，请先检索 `connection spec` （对于所需的目标，请参阅部分） [选择要从中导出受众的目标](#select-destination) 然后查看 `authSpec` 响应的。 请参考下面的选项卡 `authSpec` 所有受支持目标的属性。

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] 显示 [!DNL auth spec]

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面示例，其中提供了有关在何处查找身份验证参数的更多信息， [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "name": "amazon-s3",
        "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
        "version": "1.0",
        "authSpec": [
            {
            "name": "Access Key",
            "type": "KeyBased",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "description": "Defines auth params required for connecting to amazon-s3",
                "type": "object",
                "properties": {
                "s3AccessKey": {
                    "description": "Access key id",
                    "type": "string",
                    "pattern": "^[A-Z2-7]{20}$"
                },
                "s3SecretKey": {
                    "description": "Secret access key for the user account",
                    "type": "string",
                    "format": "password",
                    "pattern": "^[A-Za-z0-9\\/\\+]{40}$"
                }
                },
                "required": [
                "s3SecretKey",
                "s3AccessKey"
                ]
            }
            },
            {
            "name": "Assumed Role",
            "type": "S3RoleBased",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "description": "Defines role based auth params required for connecting to amazon-s3",
                "type": "object",
                "properties": {
                "s3Role": {
                    "title": "Role",
                    "description": "S3 role",
                    "type": "string",
                    "format": "password"
                }
                },
                "required": [
                "s3Role"
                ]
            }
            }
        ],
//...
```

+++

>[!TAB Azure Blob存储]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] 显示 [!DNL auth spec]

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面示例，其中提供了有关在何处查找身份验证参数的更多信息， [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "ConnectionString",
                    "type": "ConnectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Connection String for Azure Blob based destinations",
                        "type": "object",
                        "properties": {
                            "connectionString": {
                                "description": "connection string for login",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] 显示 [!DNL auth spec]

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面示例，其中提供了有关在何处查找身份验证参数的更多信息， [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Azure Service Principal Auth",
                    "type": "AzureServicePrincipal",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "type": "object",
                        "properties": {
                            "url": {
                                "description": "Endpoint for Azure Data Lake Storage Gen2.",
                                "type": "string"
                            },
                            "servicePrincipalId": {
                                "description": "Service Principal Id to connect to ADLSGen2.",
                                "type": "string"
                            },
                            "servicePrincipalKey": {
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "type": "string",
                                "format": "password"
                            },
                            "tenant": {
                                "description": "Tenant information(domain name or tenant ID).",
                                "type": "string"
                            }
                        },
                        "required": [
                            "servicePrincipalKey",
                            "url",
                            "tenant",
                            "servicePrincipalId"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB 数据登陆区(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] 显示 [!DNL auth spec]

>[!NOTE]
>
>数据登陆区目标不需要 [!DNL auth spec].

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [],
//...
```

+++

>[!TAB Google云存储]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] 显示 [!DNL auth spec]

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面示例，其中提供了有关在何处查找身份验证参数的更多信息， [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Google Cloud Storage authentication credentials",
                    "type": "GoogleCloudStorageAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to google cloud storage connector.",
                        "type": "object",
                        "properties": {
                            "accessKeyId": {
                                "description": "Access Key Id for the user account",
                                "type": "string"
                            },
                            "secretAccessKey": {
                                "description": "Secret Access Key for the user account",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "accessKeyId",
                            "secretAccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec] 显示 [!DNL auth spec]

>[!NOTE]
>
>SFTP目标包含两个单独的项，分别位于 [!DNL auth spec]，因为它同时支持密码和SSH密钥身份验证。

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面示例，其中提供了有关在何处查找身份验证参数的更多信息， [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "SFTP with Password",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations with a password",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "password": {
                                "description": "Password",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "password",
                            "domain",
                            "username"
                        ]
                    }
                },
                {
                    "name": "SFTP with SSH Key",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations using SSH Key",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "sshKey": {
                                "description": "Base64 string of the private SSH key",
                                "type": "string",
                                "format": "password",
                                "contentEncoding": "base64",
                                "uiAttributes": {
                                    "tooltip": {
                                        "id": "platform_destinations_connect_sftp_ssh",
                                        "fallbackUrl": "http://www.adobe.com/go/destinations-sftp-connection-parameters-en "
                                    }
                                }
                            }
                        },
                        "required": [
                            "sshKey",
                            "domain",
                            "username"
                        ]
                    }
                }
            ],
//...
```

+++

>[!ENDTABS]

使用身份验证规范中指定的属性(即 `authSpec` （从响应中）可以使用特定于每种目标类型的所需凭据创建基本连接，如下面的示例所示：

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

+++[!DNL Amazon S3]  — 具有访问密钥和密钥身份验证的基本连接请求

>[!TIP]
>
>有关如何获取所需身份验证凭据的信息，请参阅 [向目标进行身份验证](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) Amazon S3目标文档页面的部分。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Amazon S3 Base Connection",
  "auth": {
    "specName": "Access Key",
    "params": {
      "s3SecretKey": "<Add secret key>",
      "s3AccessKey": "<Add access key>"
    }
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec
    "version": "1.0"
  }
}'
```

+++

+++[!DNL Amazon S3]  — 具有承担角色身份验证的基本连接请求

>[!TIP]
>
>有关如何获取所需身份验证凭据的信息，请参阅 [向目标进行身份验证](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) Amazon S3目标文档页面的部分。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="17"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Amazon S3 Base Connection",
  "auth": {
    "specName": "Assumed Role",
    "params": {
      "s3Role": "<Add s3 role>"
    }
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec
    "version": "1.0"
  }
}'
```

+++

**响应**

+++[!DNL Amazon S3] 基本连接响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob存储]

**请求**

+++[!DNL Azure Blob Storage]  — 基本连接请求

>[!TIP]
>
>有关如何获取所需身份验证凭据的信息，请参阅 [向目标进行身份验证](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) Azure Blob存储目标文档页面的部分。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="17"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Blob Storage Base Connection",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "connectionString": "<Add Azure Blob connection string>"
    }
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**响应**

+++[!DNL Azure Blob Storage]  — 基本连接响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**请求**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)]  — 基本连接请求

>[!TIP]
>
>有关如何获取所需身份验证凭据的信息，请参阅 [向目标进行身份验证](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) Azure Data Lake Gen 2(ADLS Gen2)目标文档页面的部分。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="20"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Data Lake Gen 2(ADLS Gen2) Base Connection",
  "auth": {
    "specName": "Azure Service Principal Auth",
    "params": {
      "servicePrincipalKey": "<Add servicePrincipalKey>",
      "url": "<Add url>",
      "tenant": "<Add tenant>",
      "servicePrincipalId": "<Add servicePrincipalId>"
    }
  },
  "connectionSpec": {
    "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec
    "version": "1.0"
  }
}'
```

+++

**响应**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)]  — 基本连接响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 数据登陆区(DLZ)]

**请求**

+++[!DNL Data Landing Zone(DLZ)]  — 基本连接请求

>[!TIP]
>
>数据登陆区目标不需要身份验证凭据。 欲了解更多信息，请参见 [向目标进行身份验证](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) 数据登陆区目标文档页面的部分。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone(DLZ) Base Connection"
}'
```

+++

**响应**

+++[!DNL Data Landing Zone]  — 基本连接响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google云存储]

**请求**

+++[!DNL Google Cloud Storage]  — 基本连接请求

>[!TIP]
>
>有关如何获取所需身份验证凭据的信息，请参阅 [向目标进行身份验证](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) Google Cloud Storage目标文档页面的部分。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Google Cloud Storage Base Connection",
  "auth": {
    "specName": "Google Cloud Storage authentication credentials",
    "params": {
      "accessKeyId": "<Add accessKeyId>",
      "secretAccessKey": "<Add secret Access Key>"
    }
  },
  "connectionSpec": {
    "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**响应**

+++[!DNL Google Cloud Storage]  — 基本连接响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**请求**

+++包含密码的SFTP — 基本连接请求

>[!TIP]
>
>有关如何获取所需身份验证凭据的信息，请参阅 [向目标进行身份验证](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) SFTP目标文档页面的部分。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with password Base Connection",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "password": "<Add password>",
      "port": "<Add port>"      
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

| 属性 | 描述 |
| --------- | ----------- |
| `specName` | 使用 `SFTP with Password`. |
| `domain` | SFTP存储位置的IP地址或域名。 |
| `username` | 用于登录到SFTP存储位置的用户名。 |
| `password` | 用于登录到SFTP存储位置的密码。 |
| `port` | SFTP存储位置使用的端口。 |

{style="table-layout:auto"}

+++

+++使用SSH密钥的SFTP — 基本连接请求

>[!TIP]
>
>有关如何获取所需身份验证凭据的信息，请参阅 [向目标进行身份验证](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) SFTP目标文档页面的部分。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>",
      "port": "<Add port>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

| 属性 | 描述 |
| --------- | ----------- |
| `specName` | 使用 `SFTP with Password`. |
| `domain` | SFTP存储位置的IP地址或域名。 |
| `username` | 用于登录到SFTP存储位置的用户名。 |
| `sshKey` | 用于登录到SFTP存储位置的私有SSH密钥。 私钥必须采用Base64编码的字符串格式，且不得受密码保护。 |
| `port` | SFTP存储位置使用的端口。 |

{style="table-layout:auto"}

+++

**响应**

+++SFTP — 基本连接响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

### 向导出的文件添加加密

或者，您也可以向导出的文件添加加密。 为此，您需要从以下位置添加项目： `encryptionSpecs`. 请查阅下面的请求示例，其中必填参数突出显示：


>[!BEGINSHADEBOX]

+++ 查看云存储目标的加密规范

```json {line-numbers="true" start-line="1" highlight="26-27"}
           "encryptionSpecs": [
                {
                    "name": "File PGP/GPG Encryption",
                    "type": "FileAsymmetric",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Defines parameters required for capturing user's inputs for encryption",
                        "type": "object",
                        "properties": {
                            "publicKey": {
                                "description": "Base64 encoded RSA public key",
                                "type": "string",
                                "contentEncoding": "base64"
                            },
                            "encryptionAlgo": {
                                "description": "Algorithm for encryption.",
                                "type": "string",
                                "default": "PGPGPG",
                                "enum": [
                                    "PGPGPG",
                                    "NONE"
                                ]
                            }
                        },
                        "required": [
                            "encryptionAlgo",
                            "publicKey"
                        ]
                    }
                }
            ]
```

+++

**请求**

+++向基本连接添加加密 — 请求

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除内联注释。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>"
      }
    },
  "encryptionSpecs":{
     "specName": "Encryption spec",
     "params": {
         "encryptionAlgo":"PGPGPG",
         "publicKey":"<Add public key>"
      }            
    },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

**响应**

+++向基本连接添加加密 — 响应

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

记下响应中的连接ID。 创建目标连接时，此ID将在下一步中是必需的。

## 创建目标连接 {#create-target-connection}

![用于激活受众的步骤，其中突出显示用户正在执行的当前步骤](/help/destinations/assets/api/file-based-segment-export/step4.png)

接下来，您需要创建目标连接。 [Target连接](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 存储导出受众的导出参数。 导出参数包括导出位置、文件格式、压缩和其他详细信息。 例如，对于CSV文件，您可以选择多个导出选项。 在中获取有关所有受支持的CSV导出选项的更多信息 [“文件格式配置”页](/help/destinations/ui/batch-destinations-file-formatting-options.md).

请参阅 `targetSpec` 目标中提供的属性 `connection spec` 以了解每种目标类型支持的属性。 请参考下面的选项卡 `targetSpec` 所有受支持目标的属性。

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] 显示目标连接参数

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面的示例，其中提供了有关在何处查找 [!DNL target spec] 连接规范中的参数。 您还可以在以下示例中看到以下目标参数 *非* 适用于受众导出目标。

```json {line-numbers="true" start-line="1" highlight="10,56"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { //describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_bucket",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_folderpath",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Azure Blob存储]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] 显示目标连接参数

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面的示例，其中提供了有关在何处查找 [!DNL target spec] 连接规范中的参数。 您还可以在以下示例中看到以下目标参数 *非* 适用于受众导出目标。

```json {line-numbers="true" start-line="1" highlight="10,44"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Output path (relative) indicating where to upload the data",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\'\\(\\)]+$"
                        },
                        "container": {
                            "title": "Container",
                            "description": "Container within the storage where to upload the data",
                            "type": "string",
                            "pattern": "^[a-z0-9](?!.*--)[a-z0-9-]{1,61}[a-z0-9]$"
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "container",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++


>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] 显示目标连接参数

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面的示例，其中提供了有关在何处查找 [!DNL target spec] 连接规范中的参数。 您还可以在以下示例中看到以下目标参数 *非* 适用于受众导出目标。

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Enter the path to your Azure Data Lake Storage folder",
                            "type": "string"
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB 数据登陆区(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] 显示目标连接参数

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面的示例，其中提供了有关在何处查找 [!DNL target spec] 连接规范中的参数。 您还可以在以下示例中看到以下目标参数 *非* 适用于受众导出目标。

```json {line-numbers="true" start-line="1" highlight="9,36"}
"items": [
    {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
        "name": "Data Landing Zone",
        "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
        "version": "1.0",
        "authSpec": [],
        "encryptionSpecs": [],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Enter the path to your Azure Data Lake Storage folder",
                            "type": "string"
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Google云存储]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] 显示目标连接参数

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面的示例，其中提供了有关在何处查找 [!DNL target spec] 连接规范中的参数。 您还可以在以下示例中看到以下目标参数 *非* 适用于受众导出目标。

```json {line-numbers="true" start-line="1" highlight="10,44"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?!^goog.*$)(?!^.*g(o|0)(o|0)gle.*$)(((?=^.{3,63}$)(^([a-z0-9]|[a-z0-9][a-z0-9\\-_]*)[a-z0-9]$))|((?=^.{3,222}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])\\.)*([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])$)))"
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$"
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec] 显示目标连接参数

请注意中带有内联注释的高亮显示行 [!DNL connection spec] 下面的示例，其中提供了有关在何处查找 [!DNL target spec] 连接规范中的参数。 您还可以在以下示例中看到以下目标参数 *非* 适用于受众导出目标。

```json {line-numbers="true" start-line="1" highlight="10,37"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "remotePath": {
                            "title": "Folder path",
                            "description": "Enter your folder path",
                            "type": "string"
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "GZIP",
                                "NONE"
                            ]
                        }
                    },
                    "required": [
                        "remotePath",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                },
//...
```

+++

>[!ENDTABS]

通过使用上述规范，您可以构建特定于所需云存储目标的目标连接请求，如下面的选项卡所示。

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

+++[!DNL Amazon S3] - Target连接请求

>[!TIP]
>
>有关如何获取所需目标参数的信息，请参阅 [填写目标详细信息](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 的部分 [!DNL Amazon S3] 目标文档页面。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Amazon S3 Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Amazon S3]  — 具有CSV选项的Target连接请求

>[!TIP]
>
>有关可用于文件导出的CSV选项的更多信息，请参阅 [“文件格式配置”页](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Amazon S3 Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"4fce964d-3f37-408f-9778-e597338a21ee",
      "version":"1.0"
   }
}'
```

+++

**响应**

+++Target连接 — 响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob存储]

**请求**

+++[!DNL Azure Blob Storage] - Target连接请求

>[!TIP]
>
>有关如何获取所需目标参数的信息，请参阅 [填写目标详细信息](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) 的部分 [!DNL Azure Blob Storage] 目标文档页面。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Blob Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "container": "your-container-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Azure Blob Storage]  — 具有CSV选项的Target连接请求

>[!TIP]
>
>有关可用于文件导出的CSV选项的更多信息，请参阅 [“文件格式配置”页](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Azure Blob Storage Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
      "version":"1.0"
   }
}'
```

+++

**响应**

+++Target连接 — 响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**请求**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Target连接请求

>[!TIP]
>
>有关如何获取所需目标参数的信息，请参阅 [填写目标详细信息](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) Azure的部分 [!DNL Data Lake Gen 2(ADLS Gen2)] 目标文档页面。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Data Lake Gen 2(ADLS Gen2) Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)]  — 具有CSV选项的Target连接请求

>[!TIP]
>
>有关可用于文件导出的CSV选项的更多信息，请参阅 [“文件格式配置”页](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Azure Data Lake Gen 2(ADLS Gen2)",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"be2c3209-53bc-47e7-ab25-145db8b873e1",
      "version":"1.0"
   }
}'
```

+++

**响应**

+++Target连接 — 响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 数据登陆区(DLZ)]

**请求**

+++[!DNL Data Landing Zone] - Target连接请求

>[!TIP]
>
>有关如何获取所需目标参数的信息，请参阅 [填写目标详细信息](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) 的部分 [!DNL Data Landing Zone] 目标文档页面。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Data Landing Zone Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8", // Data Landing Zone connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Data Landing Zone]  — 具有CSV选项的Target连接请求

>[!TIP]
>
>有关可用于文件导出的CSV选项的更多信息，请参阅 [“文件格式配置”页](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Data Landing Zone Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"10440537-2a7b-4583-ac39-ed38d4b848e8",
      "version":"1.0"
   }
}'
```

+++

**响应**

+++Target连接 — 响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google云存储]

**请求**

+++[!DNL Google Cloud Storage] - Target连接请求

>[!TIP]
>
>有关如何获取所需目标参数的信息，请参阅 [填写目标详细信息](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) 的部分 [!DNL Google Cloud Storage] 目标文档页面。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Google Cloud Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Google Cloud Storage]  — 具有CSV选项的Target连接请求

>[!TIP]
>
>有关可用于文件导出的CSV选项的更多信息，请参阅 [“文件格式配置”页](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Google Cloud Storage Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"c5d93acb-ea8b-4b14-8f53-02138444ae99",
      "version":"1.0"
   }
}'
```

+++

**响应**

+++Target连接 — 响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**请求**

+++SFTP - Target连接请求

>[!TIP]
>
>有关如何获取所需目标参数的信息，请参阅 [填写目标详细信息](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) SFTP目标文档页面的部分。

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "SFTP Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "remotePath": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec id
        "version": "1.0"
    }
}'
```

+++

+++SFTP — 使用CSV选项的Target连接请求

>[!TIP]
>
>有关可用于文件导出的CSV选项的更多信息，请参阅 [“文件格式配置”页](/help/destinations/ui/batch-destinations-file-formatting-options.md) .

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"SFTP Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"36965a81-b1c6-401b-99f8-22508f1e6a26",
      "version":"1.0"
   }
}'
```

+++

**响应**

+++Target连接 — 响应

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

请注意 `target connection ID` 从响应中。 创建数据流以导出受众时，在下一步中需要此ID。

成功的响应会返回ID (`id`)和 `etag`. 记下目标连接ID，因为稍后创建数据流时会需要它。

## 创建数据流 {#create-dataflow}

![用于激活受众的步骤，其中突出显示用户正在执行的当前步骤](/help/destinations/assets/api/file-based-segment-export/step5.png)

目标配置的下一步是创建数据流。 A [数据流](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 可将之前创建的实体绑定在一起，并提供用于配置受众导出计划的选项。 要创建数据流，请根据所需的云存储目标使用以下有效负载，并替换之前步骤中的流实体ID。 请注意，在此步骤中，您不会将任何与属性或标识映射相关的信息添加到数据流。 这将在下一步中进行。

>[!BEGINTABS]

>[!TAB Amazon S3]

**请求**

+++创建受众导出数据流到 [!DNL Amazon S3] 目标 — 请求

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to an Amazon S3 cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an Amazon S3 cloud storage destination",
    "flowSpec": {
        "id": "1a0514a6-33d4-4c7f-aff8-594799c47549", // Amazon S3 flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**响应**

+++创建数据流 — 响应

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob存储]

**请求**

+++创建受众导出数据流到 [!DNL Azure Blob Storage] 目标 — 请求

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to an Azure Blob Storage cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an Azure Blob Storage cloud storage destination",
    "flowSpec": {
        "id": "752d422f-b16f-4f0d-b1c6-26e448e3b388", // Azure Blob Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [
        {
        "name": "GeneralTransform",
        "params": {
            "mandatoryFields": [],
            "primaryFields": [],
            "profileMapping": {},
            "segmentSelectors": {
            "selectors": []
            }
        }
        }
    ]
}'
```

+++

**响应**

+++创建数据流 — 响应

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**请求**

+++创建受众导出数据流到 [!DNL Azure Data Lake Gen 2(ADLS Gen2)] 目标 — 请求

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "flowSpec": {
        "id": "17be2013-2549-41ce-96e7-a70363bec293", // Azure Data Lake Gen 2(ADLS Gen2) flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**响应**

+++创建数据流 — 响应

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 数据登陆区(DLZ)]

**请求**

+++创建受众导出数据流到 [!DNL Data Landing Zone] 目标 — 请求

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to a Data Landing Zone cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to a Data Landing Zone cloud storage destination",
    "flowSpec": {
        "id": "cd2fc47e-e838-4f38-a581-8fff2f99b63a", // Data Landing Zone flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**响应**

+++创建数据流 — 响应

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google云存储]

**请求**

+++创建受众导出数据流到 [!DNL Google Cloud Storage] 目标 — 请求

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to a Google Cloud Storage cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to a Google Cloud Storage destination",
    "flowSpec": {
        "id": "585c15c4-6cbf-4126-8f87-e26bff78b657", // Google Cloud Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**响应**

+++创建数据流 — 响应

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**请求**

+++创建到SFTP目标的受众导出数据流 — 请求

请注意请求示例中带有内联注释的高亮显示行，这些行提供了更多信息。 将请求复制粘贴到您选择的终端时，删除请求中的内联注释。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to an SFTP cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an SFTP cloud storage destination",
    "flowSpec": {
        "id": "fd36aaa4-bf2b-43fb-9387-43785eeeb799", // SFTP flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**响应**

+++创建数据流 — 响应

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

记下响应中的数据流ID。 此ID在后续步骤中是必需的。

### 将受众添加到导出

在此步骤中，您还可以选择要导出到目标的受众。 有关此步骤以及将受众添加到数据流时的请求格式的更多信息，请查看中的示例 [更新目标数据流](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflows/operation/patchFlowById) API参考文档中的部分。


## 设置属性和标识映射 {#attribute-and-identity-mapping}

![用于激活受众的步骤，其中突出显示用户正在执行的当前步骤](/help/destinations/assets/api/file-based-segment-export/step6.png)

创建数据流后，您需要为要导出的属性和身份设置映射。 这包含三个步骤，如下所示：

1. 创建输入架构
2. 创建输出架构
3. 设置映射集以连接创建的架构

例如，要获取UI中显示的以下映射，您需要完成上面列出的三个步骤，并在下一个标题中详述。

![映射步骤示例](/help/destinations/assets/api/file-based-segment-export/mapping-example.png)

### 创建输入架构

要创建输入架构，您首先需要检索 [合并架构](/help/profile/ui/union-schema.md) 以及可以导出到目标的身份。 这是属性和标识的架构，您可以选择它作为源映射。

![显示选择源字段视图中的属性和标识选项的录制](/help/destinations/assets/api/file-based-segment-export/select-source-field.gif)

查看以下用于检索属性和身份的请求和响应示例。

>[!BEGINSHADEBOX]

**请求获取属性**

+++从合并架构中获取可用属性 — 请求

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/ups/config/entityTypes/_xdm.context.profile?property=fullSchema==true&property=includeRelationshipDescriptors==true' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**响应**

+++从合并架构获取可用属性 — 响应

为简短起见，下面的答复已缩短。

```json
       "person": {
            "title": "Person",
            "description": "An individual actor, contact, or owner.",
            "meta:referencedFrom": [
                "https://ns.adobe.com/xdm/context/person"
            ],
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "birthDate": {
                    "meta:xdmType": "date",
                    "type": "string",
                    "format": "date",
                    "title": "Birth date(YYYY-MM-DD)",
                    "description": "The full date a person was born."
                },
                "birthDayAndMonth": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Birth date (MM-DD)",
                    "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year."
                },
                "birthYear": {
                    "meta:xdmType": "short",
                    "type": "integer",
                    "minimum": 1,
                    "maximum": 32767,
                    "title": "Birth year",
                    "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date."
                },
                "gender": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Gender",
                    "description": "Gender identity of the person.\n",
                    "enum": [
                        "male",
                        "female",
                        "not_specified",
                        "non_specific"
                    ],
                    "meta:enum": {
                        "male": "Male",
                        "female": "Female",
                        "not_specified": "Not Specified",
                        "non_specific": "Non-specific"
                    },
                    "default": "not_specified"
                },
                "maritalStatus": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Marital Status",
                    "description": "Describes a person's relationship with a significant other.",
                    "enum": [
                        "married",
                        "single",
                        "divorced",
                        "widowed",
                        "not_specified"
                    ],
                    "meta:enum": {
                        "divorced": "Divorced",
                        "not_specified": "Not Specified",
                        "married": "Married",
                        "single": "Single",
                        "widowed": "Widowed"
                    },
                    "default": "not_specified"
                },
                "name": {
                    "title": "Full name",
                    "description": "The person's full name.",
                    "meta:referencedFrom": [
                        "https://ns.adobe.com/xdm/context/person-name"
                    ],
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "courtesyTitle": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Courtesy title",
                            "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr."
                        },
                        "firstName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "First name",
                            "description": "The first audience of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable."
                        },
                        "fullName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Full name",
                            "description": "The full name of the person, in writing order most commonly accepted in the language of the name."
                        },
                        "lastName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Last name",
                            "description": "The last audience of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable."
                        },
                        "middleName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Middle name",
                            "description": "Middle, alternative, or additional names supplied between the first name and last name."
                        },
                        "suffix": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Suffix",
                            "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc."
                        }
                    }
                },
                "nationality": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Nationality",
                    "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code."
                },
                "taxId": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Tax ID",
                    "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
                    "meta:status": "deprecated"
                },
                "type": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Type",
                    "description": "The type of individual in different business contexts like B2C."
                }
            }
        }
```

+++

>[!ENDSHADEBOX]



>[!BEGINSHADEBOX]

**请求获取身份**

+++获取可在映射步骤中使用的可用标识

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/idnamespace/identities' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \ 
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**响应**

+++ 查看要在输入架构中使用的可用身份

响应将返回在创建输入架构时可以使用的标识。 请注意，此响应会返回两者 [标准](/help/identity-service/features/namespaces.md#standard) 和 [自定义](/help/identity-service/features/namespaces.md#manage-namespaces) 您在Experience Platform中设置的身份命名空间。

```json
[
    {
        "updateTime": 1551688425455,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "Adobe Audience Manger UUID",
        "id": 0,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "Adobe Experience Cloud ID",
        "id": 4,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "AdCloud",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "Email_LC_SHA256",
        "status": "ACTIVE",
        "description": "Email addresses need to be hashed using SHA256 and lowercased. Please also note that leading and trailing spaces need to be trimmed before an email address is normalized. You won't be able to change this setting later",
        "id": 11,
        "createTime": 1551688425455,
        "idType": "Email",
        "namespaceType": "Standard",
        "name": "Emails (SHA256, lowercased)",
        "custom": false,
        "hashFunction": "SHA256",
        "transform": "lowercase"
    },
    {
        "updateTime": 1597996026101,
        "code": "Phone_E.164",
        "status": "ACTIVE",
        "description": "Namespace for raw phone numbers in E.164 format. + sign is required",
        "id": 17,
        "createTime": 1597996026101,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (E.164)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "GAID",
        "status": "ACTIVE",
        "description": "This datasource is associated to a Google Ad ID",
        "id": 20914,
        "createTime": 1551688425455,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Google Ad ID (GAID)",
        "custom": false
    },
    {
        "updateTime": 1476993749000,
        "code": "IDFA",
        "status": "ACTIVE",
        "description": "Apple ID for Advertisers. See: https://support.apple.com/en-us/HT202074 for more info.",
        "id": 20915,
        "createTime": 1476993749000,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Apple IDFA (ID for Advertisers)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "AAID",
        "status": "ACTIVE",
        "description": "Adobe Analytics (Legacy ID)",
        "id": 10,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "Adobe Analytics (Legacy ID)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "Email",
        "status": "ACTIVE",
        "description": "Email",
        "id": 6,
        "createTime": 1551688425455,
        "idType": "Email",
        "namespaceType": "Standard",
        "name": "Email",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "WAID",
        "status": "ACTIVE",
        "description": "Windows AID",
        "id": 8,
        "createTime": 1551688425455,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Windows AID",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "TNTID",
        "status": "ACTIVE",
        "description": "Adobe Target (TNTID)",
        "id": 9,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "TNTID",
        "custom": false
    },
    {
        "updateTime": 1556676464714,
        "code": "Google",
        "status": "ACTIVE",
        "id": 771,
        "createTime": 1556676464714,
        "idType": "COOKIE",
        "namespaceType": "Integration",
        "name": "Google",
        "custom": false
    },
    {
        "updateTime": 1604597776019,
        "code": "Phone_SHA256_E.164",
        "status": "ACTIVE",
        "description": "Phone numbers need to be hashed using SHA256 without any dashes. Hash should be completed by customers on raw phone numbers in E.164 format. Please note that some destinations may have different phone number formatting requirements. Refer to documentation or consult your Adobe representative",
        "id": 18,
        "createTime": 1604597776019,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (SHA256_E.164)",
        "custom": false,
        "hashFunction": "SHA256"
    },
    {
        "updateTime": 1604597776019,
        "code": "Phone_SHA256",
        "status": "ACTIVE",
        "description": "Remove symbols, letters, and any leading zeroes before hashing. Prefix the country code before hashing. Please note that some destinations may have different phone number formatting requirements. Refer to documentation or consult your Adobe representative",
        "id": 15,
        "createTime": 1597995542594,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (SHA256)",
        "custom": false,
        "hashFunction": "SHA256"
    },
    {
        "updateTime": 1551688425455,
        "code": "Phone",
        "status": "ACTIVE",
        "description": "Phone",
        "id": 7,
        "createTime": 1551688425455,
        "idType": "PHONE_NUMBER",
        "namespaceType": "Standard",
        "name": "Phone",
        "custom": false
    }
]
```

+++

>[!ENDSHADEBOX]

接下来，您需要复制上面的响应，并使用它创建输入架构。 您可以复制上述响应的整个JSON响应，并将其放入 `jsonSchema` 对象如下所示。

>[!BEGINSHADEBOX]

**请求创建输入架构**

+++创建输入架构 — 请求

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/schemas/' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \ 
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \ 
--header 'Content-Type: application/json' \ 
--data-raw '{
    "name":"Sample Schema for Flow Mapping",
    "jsonSchema":{...insert response from union schema response here}
    '
```

+++

**响应**

+++创建输入架构 — 响应

```json
{
   "id":"8db56468c2ab475dbf17c2621f92c0f8",
   "version":0,
   "jsonSchema":{
      "title":"XDM Individual Profile",
      "description":"An XDM Individual Profile forms a singular representation of the attributes and interests of both identified and partially-identified individuals. Less-identified profiles may contain only anonymous behavioral signals, such as browser cookies, while highly-identified profiles may contain detailed personal information such as name, date of birth, location, and email address. As a profile grows, it becomes a robust repository of personal information, identification information, contact details, and communication preferences for an individual.",
      "type":"object",
      "properties":{ // this section returns the contents that you have added to the jsonSchema object in the request
      }
   }
}
```

+++

>[!ENDSHADEBOX]

响应中的ID表示您创建的输入架构的唯一标识符。 从响应中复制ID，因为您将在后续步骤中重复使用它。

### 创建输出架构

接下来，必须为导出设置输出架构。 首先，您需要查找并检查现有合作伙伴架构。

>[!BEGINSHADEBOX]

**请求**

+++请求获取输出架构的合作伙伴架构

请注意，以下示例使用 `connection spec ID` 适用于Amazon S3。 请将此值替换为特定于目标的连接规范ID。

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**具有示例架构的响应**

Inspect您执行上述调用时获得的响应。 您需要深入查看响应以查找对象 `targetSpec.attributes.partnerSchema.jsonSchema`

+++ 获取输出架构的合作伙伴架构的响应

```json
{
   "title":"defaultschema",
   "type":"object",
   "properties":{
      "attributes":{
         "type":"object",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"object",
            "properties":{
               "value":{
                  "type":"string",
                  "title":"Value"
               }
            },
            "meta:xdmType":"object"
         }
      },
      "identityMap":{
         "type":"object",
         "meta:xdmField":"xdm:identityMap",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"array",
            "items":{
               "type":"object",
               "properties":{
                  "id":{
                     "type":"string",
                     "title":"Identifier",
                     "description":"Identity of the consumer in the related namespace.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:id"
                  },
                  "primary":{
                     "type":"boolean",
                     "title":"Primary",
                     "default":false,
                     "description":"Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                     "meta:xdmType":"boolean",
                     "meta:xdmField":"xdm:primary"
                  },
                  "authenticatedState":{
                     "enum":[
                        "ambiguous",
                        "authenticated",
                        "loggedOut"
                     ],
                     "type":"string",
                     "default":"ambiguous",
                     "meta:enum":{
                        "ambiguous":"Ambiguous",
                        "loggedOut":"User was identified by a login action at some point of time previously, but is not currently logged in.",
                        "authenticated":"User identified by a login or similar action that was valid at the time of the event observation."
                     },
                     "description":"The state this identity is authenticated as for this observed ExperienceEvent.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:authenticatedState"
                  }
               },
               "meta:xdmType":"object",
               "meta:referencedFrom":"https://ns.adobe.com/xdm/context/identityitem"
            },
            "meta:xdmType":"array"
         }
      },
      "segmentMembership":{
         "title":"Segment membership map",
         "type":"object",
         "meta:xdmField":"xdm:segmentMembership",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"object",
            "title":"Segment membership per namespace",
            "meta:xdmType":"map",
            "additionalProperties":{
               "type":"object",
               "properties":{
                  "status":{
                     "enum":[
                        "realized",
                        "exited"
                     ],
                     "type":"string",
                     "title":"Status",
                     "default":"realized",
                     "meta:enum":{
                        "exited":"Entity is exiting the segment.",
                        "realized":"Entity is entering the segment."
                     },
                     "description":"Is the audience participation realized as part of the current request.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:status"
                  },
                  "payload":{
                     "type":"object",
                     "title":"Payload",
                     "required":[
                        "payloadType"
                     ],
                     "properties":{
                        "payloadType":{
                           "enum":[
                              "boolean",
                              "number",
                              "propensity",
                              "string"
                           ],
                           "type":"string",
                           "title":"Payload Type",
                           "meta:enum":{
                              "number":"Number",
                              "string":"String",
                              "boolean":"Boolean",
                              "propensity":"Propensity"
                           },
                           "description":"The type of payload.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:payloadType"
                        },
                        "payloadNumberValue":{
                           "type":"number",
                           "title":"Value",
                           "description":"The number.",
                           "meta:xdmType":"number",
                           "meta:xdmField":"xdm:payloadNumberValue"
                        },
                        "payloadStringValue":{
                           "type":"string",
                           "title":"Value",
                           "description":"The string value.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:payloadStringValue"
                        },
                        "payloadBooleanValue":{
                           "type":"boolean",
                           "title":"Value",
                           "description":"The boolean value.",
                           "meta:xdmType":"boolean",
                           "meta:xdmField":"xdm:payloadBooleanValue"
                        },
                        "payloadPropensityValue":{
                           "type":"number",
                           "title":"Value",
                           "maximum":1,
                           "description":"The propensity.",
                           "meta:xdmType":"number",
                           "meta:xdmField":"xdm:payloadPropensityValue",
                           "exclusiveMinimum":0
                        }
                     },
                     "description":"Values that are directly related with the audience realization. This payload exists with the same 'validUntil' as the audience realization. Note that the intention is that exactly one payload value be included, as indicated by the payload type. This was originally modeled using 'oneOf', but due to limitations in our tooling that was removed. This more semantically meaningful representation will be re-introduced in the future.",
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:payload"
                  },
                  "version":{
                     "type":"string",
                     "title":"Version",
                     "description":"The version of the audience definition used in this audience assertion. Version can be omitted in audience lists when all memberships versions are the same.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:version"
                  },
                  "segmentID":{
                     "type":"object",
                     "title":"Segment ID",
                     "properties":{
                        "_id":{
                           "type":"string",
                           "title":"Identifier",
                           "format":"uri-reference",
                           "description":"Identity of the audience in the related namespace.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"@id"
                        },
                        "xid":{
                           "type":"string",
                           "title":"Experience identifier",
                           "description":"When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:xid"
                        },
                        "namespace":{
                           "type":"object",
                           "title":"Namespace",
                           "required":[
                              "code"
                           ],
                           "properties":{
                              "code":{
                                 "type":"string",
                                 "title":"Code",
                                 "description":"The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                 "meta:xdmType":"string",
                                 "meta:xdmField":"xdm:code"
                              }
                           },
                           "description":"The namespace associated with the `xid` attribute.",
                           "meta:xdmType":"object",
                           "meta:xdmField":"xdm:namespace",
                           "meta:referencedFrom":"https://ns.adobe.com/xdm/context/namespace"
                        }
                     },
                     "description":"The identity of the audience or snapshot definition in with the domain of the specific system that processes that type of segment. Deprecated.",
                     "meta:status":"deprecated",
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:segmentID",
                     "meta:referencedFrom":"https://ns.adobe.com/xdm/context/segmentidentity"
                  },
                  "validUntil":{
                     "type":"string",
                     "title":"Valid until",
                     "format":"date-time",
                     "description":"The timestamp for when the audienceassertion should no longer be assumed to be valid and should either be ignored or revalidated.",
                     "meta:xdmType":"date-time",
                     "meta:xdmField":"xdm:validUntil"
                  },
                  "profileStitchID":{
                     "type":"object",
                     "properties":{
                        "_id":{
                           "type":"string",
                           "title":"Identifier",
                           "format":"uri-reference",
                           "description":"Identity of the profile stitch in the related namespace.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"@id"
                        },
                        "xid":{
                           "type":"string",
                           "title":"Experience identifier",
                           "description":"When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:xid"
                        },
                        "namespace":{
                           "type":"object",
                           "title":"Namespace",
                           "required":[
                              "code"
                           ],
                           "properties":{
                              "code":{
                                 "type":"string",
                                 "title":"Code",
                                 "description":"The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                 "meta:xdmType":"string",
                                 "meta:xdmField":"xdm:code"
                              }
                           },
                           "description":"The namespace associated with the `xid` attribute.",
                           "meta:xdmType":"object",
                           "meta:xdmField":"xdm:namespace",
                           "meta:referencedFrom":"https://ns.adobe.com/xdm/context/namespace"
                        }
                     },
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:profileStitchID",
                     "meta:referencedFrom":"https://ns.adobe.com/xdm/context/profileStitchIdentity"
                  },
                  "lastQualificationTime":{
                     "type":"string",
                     "title":"Last qualification time",
                     "format":"date-time",
                     "description":"The timestamp when the assertion of audience membership was made.",
                     "meta:xdmType":"date-time",
                     "meta:xdmField":"xdm:lastQualificationTime"
                  }
               },
               "meta:xdmType":"object",
               "meta:referencedFrom":"https://ns.adobe.com/xdm/context/segmentmembership"
            }
         }
      }
   }
}
```

+++

>[!ENDSHADEBOX]

接下来，您需要创建输出架构。 复制您上面的JSON响应并将其粘贴到 `jsonSchema` 下方的对象。

>[!BEGINSHADEBOX]

**请求**

+++创建输出架构 — 请求

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/schemas' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer TOKEN' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Sample Schema for Flow Mapping",
"jsonSchema":{...insert JSON from the response above here}
}
'
```

+++

**响应**

+++创建输出架构 — 响应

```json
{
    "id": "2f4fd51934c1409fb1d8207dd9f43dc9",
    "version": 0,
    "jsonSchema": {
        "title": "defaultschema",
        "type": "object",
        "properties": {
            "identityMap": {
                "type": "object",
                "meta:xdmField": "xdm:identityMap",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "meta:xdmType": "array",
                    "items": {
                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/identityitem",
                        "properties": {
                            "primary": {
                                "meta:xdmField": "xdm:primary",
                                "meta:xdmType": "boolean",
                                "description": "Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                                "default": false,
                                "type": "boolean",
                                "title": "Primary"
                            },
                            "id": {
                                "meta:xdmField": "xdm:id",
                                "meta:xdmType": "string",
                                "description": "Identity of the consumer in the related namespace.",
                                "type": "string",
                                "title": "Identifier"
                            },
                            "authenticatedState": {
                                "meta:xdmField": "xdm:authenticatedState",
                                "meta:xdmType": "string",
                                "meta:enum": {
                                    "loggedOut": "User was identified by a login action at some point of time previously, but is not currently logged in.",
                                    "authenticated": "User identified by a login or similar action that was valid at the time of the event observation.",
                                    "ambiguous": "Ambiguous"
                                },
                                "enum": [
                                    "ambiguous",
                                    "authenticated",
                                    "loggedOut"
                                ],
                                "default": "ambiguous",
                                "type": "string",
                                "description": "The state this identity is authenticated as for this observed ExperienceEvent."
                            }
                        },
                        "meta:xdmType": "object",
                        "type": "object"
                    },
                    "type": "array"
                }
            },
            "segmentMembership": {
                "title": "Segment membership map",
                "type": "object",
                "meta:xdmField": "xdm:segmentMembership",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "additionalProperties": {
                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/segmentmembership",
                        "properties": {
                            "version": {
                                "meta:xdmField": "xdm:version",
                                "meta:xdmType": "string",
                                "description": "The version of the audience definition used in this audience assertion. Version can be omitted in audience lists when all memberships versions are the same.",
                                "type": "string",
                                "title": "Version"
                            },
                            "validUntil": {
                                "meta:xdmField": "xdm:validUntil",
                                "meta:xdmType": "date-time",
                                "description": "The timestamp for when the audienceassertion should no longer be assumed to be valid and should either be ignored or revalidated.",
                                "format": "date-time",
                                "type": "string",
                                "title": "Valid until"
                            },
                            "status": {
                                "meta:xdmField": "xdm:status",
                                "meta:xdmType": "string",
                                "meta:enum": {
                                    "exited": "Entity is exiting the segment.",
                                    "realized": "Entity is entering the segment."
                                },
                                "enum": [
                                    "realized",
                                    "exited"
                                ],
                                "default": "realized",
                                "description": "Is the audience participation realized as part of the current request.",
                                "type": "string",
                                "title": "Status"
                            },
                            "segmentID": {
                                "meta:xdmField": "xdm:segmentID",
                                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/segmentidentity",
                                "properties": {
                                    "xid": {
                                        "meta:xdmField": "xdm:xid",
                                        "meta:xdmType": "string",
                                        "description": "When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                                        "type": "string",
                                        "title": "Experience identifier"
                                    },
                                    "namespace": {
                                        "meta:xdmField": "xdm:namespace",
                                        "required": [
                                            "code"
                                        ],
                                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/namespace",
                                        "properties": {
                                            "code": {
                                                "meta:xdmField": "xdm:code",
                                                "meta:xdmType": "string",
                                                "description": "The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                                "type": "string",
                                                "title": "Code"
                                            }
                                        },
                                        "meta:xdmType": "object",
                                        "type": "object",
                                        "description": "The namespace associated with the `xid` attribute.",
                                        "title": "Namespace"
                                    },
                                    "_id": {
                                        "meta:xdmField": "@id",
                                        "meta:xdmType": "string",
                                        "description": "Identity of the audience in the related namespace.",
                                        "format": "uri-reference",
                                        "type": "string",
                                        "title": "Identifier"
                                    }
                                },
                                "meta:xdmType": "object",
                                "type": "object",
                                "description": "The identity of the audience or snapshot definition in with the domain of the specific system that processes that type of segment. Deprecated.",
                                "meta:status": "deprecated",
                                "title": "Segment ID"
                            },
                            "profileStitchID": {
                                "meta:xdmField": "xdm:profileStitchID",
                                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/profileStitchIdentity",
                                "properties": {
                                    "xid": {
                                        "meta:xdmField": "xdm:xid",
                                        "meta:xdmType": "string",
                                        "description": "When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                                        "type": "string",
                                        "title": "Experience identifier"
                                    },
                                    "namespace": {
                                        "meta:xdmField": "xdm:namespace",
                                        "required": [
                                            "code"
                                        ],
                                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/namespace",
                                        "properties": {
                                            "code": {
                                                "meta:xdmField": "xdm:code",
                                                "meta:xdmType": "string",
                                                "description": "The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                                "type": "string",
                                                "title": "Code"
                                            }
                                        },
                                        "meta:xdmType": "object",
                                        "type": "object",
                                        "description": "The namespace associated with the `xid` attribute.",
                                        "title": "Namespace"
                                    },
                                    "_id": {
                                        "meta:xdmField": "@id",
                                        "meta:xdmType": "string",
                                        "description": "Identity of the profile stitch in the related namespace.",
                                        "format": "uri-reference",
                                        "type": "string",
                                        "title": "Identifier"
                                    }
                                },
                                "meta:xdmType": "object",
                                "type": "object"
                            },
                            "payload": {
                                "meta:xdmField": "xdm:payload",
                                "meta:xdmType": "object",
                                "required": [
                                    "payloadType"
                                ],
                                "properties": {
                                    "payloadType": {
                                        "meta:xdmField": "xdm:payloadType",
                                        "meta:xdmType": "string",
                                        "description": "The type of payload.",
                                        "meta:enum": {
                                            "string": "String",
                                            "propensity": "Propensity",
                                            "number": "Number",
                                            "boolean": "Boolean"
                                        },
                                        "enum": [
                                            "boolean",
                                            "number",
                                            "propensity",
                                            "string"
                                        ],
                                        "type": "string",
                                        "title": "Payload Type"
                                    },
                                    "payloadStringValue": {
                                        "meta:xdmField": "xdm:payloadStringValue",
                                        "meta:xdmType": "string",
                                        "description": "The string value.",
                                        "type": "string",
                                        "title": "Value"
                                    },
                                    "payloadPropensityValue": {
                                        "meta:xdmField": "xdm:payloadPropensityValue",
                                        "meta:xdmType": "number",
                                        "maximum": 1,
                                        "exclusiveMinimum": 0,
                                        "description": "The propensity.",
                                        "type": "number",
                                        "title": "Value"
                                    },
                                    "payloadNumberValue": {
                                        "meta:xdmField": "xdm:payloadNumberValue",
                                        "meta:xdmType": "number",
                                        "description": "The number.",
                                        "type": "number",
                                        "title": "Value"
                                    },
                                    "payloadBooleanValue": {
                                        "meta:xdmField": "xdm:payloadBooleanValue",
                                        "meta:xdmType": "boolean",
                                        "description": "The boolean value.",
                                        "type": "boolean",
                                        "title": "Value"
                                    }
                                },
                                "type": "object",
                                "description": "Values that are directly related with the audience realization. This payload exists with the same 'validUntil' as the audience realization. Note that the intention is that exactly one payload value be included, as indicated by the payload type. This was originally modeled using 'oneOf', but due to limitations in our tooling that was removed. This more semantically meaningful representation will be re-introduced in the future.",
                                "title": "Payload"
                            },
                            "lastQualificationTime": {
                                "meta:xdmField": "xdm:lastQualificationTime",
                                "meta:xdmType": "date-time",
                                "description": "The timestamp when the assertion of audience membership was made.",
                                "format": "date-time",
                                "type": "string",
                                "title": "Last qualification time"
                            }
                        },
                        "meta:xdmType": "object",
                        "type": "object"
                    },
                    "meta:xdmType": "map",
                    "type": "object",
                    "title": "Segment membership per namespace"
                }
            },
            "attributes": {
                "type": "object",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "properties": {
                        "value": {
                            "type": "string",
                            "title": "Value"
                        }
                    },
                    "meta:xdmType": "object",
                    "type": "object"
                }
            },
            "firstName": {
                "title": "firstName",
                "type": "string"
            },
            "Email": {
                "title": "Email",
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "id": {
                            "title": "id",
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                },
                "meta:xdmType": "array"
            }
        }
    }
}
```

响应中的ID表示您创建的输入架构的唯一标识符。 从响应中复制ID，因为您将在后续步骤中重复使用它。

>[!ENDSHADEBOX]

### 创建映射集 {#create-mapping-set}

接下来，使用 [数据准备API](https://developer.adobe.com/experience-platform-apis/references/data-prep/#tag/Mapping-sets/operation/createMappingSet) 使用输入架构ID、输出架构ID和所需的字段映射创建映射集。

>[!BEGINSHADEBOX]

**请求**

+++创建映射集 — 请求

>[!IMPORTANT]
>
>* 在下面显示的映射对象中， `destination` 参数不接受点 `"."`. 例如，您需要使用personalEmail_address或segmentMembership_status ，如配置示例中突出显示的内容所示。
>* 当源属性是标识属性并包含点时，有一种特殊情况。 在这种情况下，属性需要转义 `//`，如下面突出显示的那样。
>* 另请注意，即使下面的示例配置包括 `Email` 和 `Phone_E.164`，则每个数据流只能导出一个标识属性。

```shell {line-numbers="true" start-line="1" highlight="16-38"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer TOKEN' \
--header 'Content-Type: application/json' \
--data-raw '{
    "inputSchema": {
        "id": "81d7fc5376e54eb58d5186fd30d5a8c9"
    },  
    "outputSchema": {
        "id": "2f4fd51934c1409fb1d8207dd9f43dc9"
    },
    "mappings": [
        {
            "destination": "firstName",
            "source": "person.name.firstName",
            "sourceType": "ATTRIBUTE"
        }, 
        {
            "destination": "Email",
            "source": "identityMap.Email",
            "sourceType": "ATTRIBUTE"
        },
        {
            "destination": "Phone_E_164",
            "source": "identityMap.Phone_E//.164",
            "sourceType": "ATTRIBUTE"
        },
        {
            "destination": "personalEmail_address",
            "source": "personalEmail.address",
            "sourceType": "ATTRIBUTE"
        },        
        {
            "destination": "segmentMembership_status",
            "source": "segmentMembership.ups.seg_id.status",
            "sourceType": "ATTRIBUTE"
        }        
    ],
    "xdmVersion": "1.0"
}'
```

+++

**响应**

+++ 创建映射集 — 响应

```json
{
    "id": "5f0031f8ccd4444dac9c5c391389e9e8",
    "version": 0,
    "createdDate": 1678999005197,
    "modifiedDate": 1678999005197,
    "createdBy": "example@AdobeID",
    "modifiedBy": "example@AdobeID"
}
```

+++

>[!ENDSHADEBOX]

记下映射集的ID，因为您将需要在下一步中使用映射集ID更新现有数据流。

接下来，获取要更新的数据流的ID。

>[!BEGINSHADEBOX]

请参阅 [检索目标数据流的详细信息](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflows/operation/getFlowById) 以了解有关检索数据流ID的信息。

>[!ENDSHADEBOX]

最后，您需要 `PATCH` 包含刚刚创建的映射集信息的数据流。

>[!BEGINSHADEBOX]

**请求**

+++ 使用映射集信息更新数据流 — 请求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/df8245a8-dd8f-42da-a04a-2d3a92654d9e' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: ETAG_HERE' \
--data-raw '[
   {
      "op":"ADD",
      "path":"/transformations/0/params/profileMapping",
      "value":{
         "mappingId":"304ca6a2fff244949c956cad1cd9eae6",
         "mappingVersion":0
      }
   }
]'
```

+++

**响应**

+++ 使用映射集信息更新数据流 — 响应

流服务API的响应将返回已更新数据流的ID。

```json
{
    "id": "1c246ae4-ba0d-43cd-a0ec-f16fe0a56b55",
    "etag": "\"1500c67f-0000-0200-0000-64137ee00000\""
}
```

+++

>[!ENDSHADEBOX]

## 进行其他数据流更新 {#other-dataflow-updates}

![用于激活受众的步骤，其中突出显示用户正在执行的当前步骤](/help/destinations/assets/api/file-based-segment-export/step7.png)

要更新数据流，请使用 `PATCH` 操作。 例如，您可以向数据流添加营销操作。 或者，您可以更新数据流以选择字段作为必需键或重复数据删除键。

### 添加营销操作 {#add-marketing-action}

添加 [营销活动](/help/data-governance/api/marketing-actions.md)，请参阅下面的请求和响应示例。

>[!IMPORTANT]
>
>此 `If-Match` 进行以下操作时需要标题： `PATCH` 请求。 此标头的值是要更新的数据流的唯一版本。 每次成功更新流实体（例如数据流、目标连接等）时，etag值都会更新。
>
> GET要获取最新版本的etag值，请对 `https://platform.adobe.io/data/foundation/flowservice/flows/{ID}` 端点，其中 `{ID}` 是您要更新的数据流ID。
>
> 确保将 `If-Match` 标题加双引号，如下面的示例所示 `PATCH` 请求。

>[!BEGINSHADEBOX]

**请求**

>[!TIP]
>
>将营销操作添加到数据流之前，您可以查找现有的核心营销操作和自定义营销操作。 视图 [如何检索现有营销操作的列表](/help/data-governance/api/marketing-actions.md#list).

+++将营销操作添加到目标数据流 — 请求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'accept: application/json' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '[
   {
      "op":"add",
      "path":"/policy",
      "value":{
         "enforcementRefs":[
            
         ]
      }
   },
   {
      "op":"add",
      "path":"/policy/enforcementRefs/-",
      "value":"/dulepolicy/marketingActions/custom/6b935bc8-bb9e-451b-a327-0ffddfb91e66/constraints"
   }
]'
```

+++


**响应**

+++添加营销操作 — 响应

成功的响应返回响应代码 `200` 以及已更新数据流和已更新eTag的ID。

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDSHADEBOX]

### 添加必需键 {#add-mandatory-key}

添加 [必需键](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes)，请参阅下面的请求和响应示例。

>[!IMPORTANT]
>
>此 `If-Match` 进行以下操作时需要标题： `PATCH` 请求。 此标头的值是要更新的数据流的唯一版本。 每次成功更新流实体（例如数据流、目标连接等）时，etag值都会更新。
>
> GET要获取最新版本的etag值，请对 `https://platform.adobe.io/data/foundation/flowservice/flows/{ID}` 端点，其中 `{ID}` 是您要更新的数据流ID。
>
> 确保将 `If-Match` 标题加双引号，如下面的示例所示 `PATCH` 请求。

>[!BEGINSHADEBOX]

**请求**

+++将标识添加为必填字段 — 请求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/mandatoryFields",
    "value": [
      "GAID"
    ]
  }
]'
```

+++

+++添加XDM属性作为必填字段 — 请求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/mandatoryFields",
    "value": [
      "GAID"
    ]
  }
]'
```

+++

**响应**

+++添加必填字段 — 响应

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDSHADEBOX]

### 添加重复数据删除键 {#add-deduplication-key}

添加 [重复数据删除键](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys)，请参阅下面的请求和响应示例

>[!IMPORTANT]
>
>此 `If-Match` 进行以下操作时需要标题： `PATCH` 请求。 此标头的值是要更新的数据流的唯一版本。 每次成功更新流实体（例如数据流、目标连接等）时，etag值都会更新。
>
> GET要获取最新版本的etag值，请对 `https://platform.adobe.io/data/foundation/flowservice/flows/{ID}` 端点，其中 `{ID}` 是您要更新的数据流ID。
>
> 确保将 `If-Match` 标题加双引号，如下面的示例所示 `PATCH` 请求。

>[!BEGINSHADEBOX]

**请求**

+++添加标识作为重复数据删除键 — 请求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/primaryFields",
    "value": [
      {
        "identityNamespace": "GAID",
        "fieldType": "IDENTITY"
      }
    ]
  }
]'
```

+++

+++添加XDM属性作为重复数据删除键 — 请求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/primaryFields",
    "value": [
      {
        "identityNamespace": "GAID",
        "fieldType": "IDENTITY"
      }
    ]
  }
]'
```

+++

**响应**

+++添加必填字段 — 响应

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDSHADEBOX]

## 验证数据流（获取数据流运行） {#get-dataflow-runs}

![用于激活受众的步骤，其中突出显示用户正在执行的当前步骤](/help/destinations/assets/api/file-based-segment-export/step8.png)

要检查数据流的执行，请使用数据流运行API：

>[!BEGINSHADEBOX]

**请求**

+++获取数据流运行 — 请求

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw ''
```

+++

**响应**

+++获取数据流运行 — 响应

```json
{
    "items": [
        {
            "id": "4b7728dd-83c9-4c38-95a4-24ddab545404",
            "createdAt": 1675807718296,
            "updatedAt": 1675807731834,
            "createdBy": "aep_activation_batch@AdobeID",
            "updatedBy": "acp_foundation_connectors@AdobeID",
            "createdClient": "aep_activation_batch",
            "updatedClient": "acp_foundation_connectors",
            "sandboxId": "7dfdcd30-0a09-11ea-8ea6-7bf93ce86c28",
            "sandboxName": "sand-1",
            "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
            "flowId": "aae5ec63-b0ac-4808-9a44-abf2ea67bd5a",
            "flowSpec": {
                "id": "615d3489-36d2-4671-9467-4ae1129facd3",
                "version": "1.0"
            },
            "providerRefId": "ba56f98e0c49b572adb249980c39b1c7",
            "etag": "\"08005e9e-0000-0200-0000-63e2cbf30000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1675807719411,
                    "completedAtUTC": 1675807719416
                },
                "sizeSummary": {
                    "inputBytes": 0
                },
                "recordSummary": {
                    "inputRecordCount": 0,
                    "skippedRecordCount": 0,
                    "sourceSummaries": [
                        {
                            "id": "ea2b1205-4692-49de-b448-ebf75b1d188a",
                            "inputRecordCount": 0,
                            "skippedRecordCount": 0,
                            "entitySummaries": [
                                {
//...
```

+++

>[!ENDSHADEBOX]

您可以找到有关 [数据流运行API返回的各种参数](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns) API参考文档中的。

## API错误处理 {#api-error-handling}

本教程中的API端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](/help/landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](/help/landing/troubleshooting.md#request-header-errors) 有关解释错误响应的更多信息，请参阅平台故障排除指南。

## 后续步骤 {#next-steps}

通过学习本教程，您已成功将Platform连接到其中一个首选云存储目标，并将数据流设置到相应的目标以导出受众。 有关更多详细信息，请参阅以下页面，例如如何使用流服务API编辑现有数据流：

* [目标概述](../home.md)
* [目标目录概述](../catalog/overview.md)
* [使用流服务API更新目标数据流](../api/update-destination-dataflows.md)
