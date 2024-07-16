---
keywords: Experience Platform；归因人工智能；访问分数；热门主题；下载分数；归因人工智能分数；导出；导出
feature: Attribution AI
title: 在Attribution AI中下载分数
description: 本文档可用作下载Attribution AI得分的指南。
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 2%

---

# 在Attribution AI中下载分数

本文档可用作下载Attribution AI得分的指南。

## 快速入门

Attribution AI允许您以Parquet文件格式下载得分。 本教程要求您已阅读并完成[快速入门](./getting-started.md)指南中的Attribution AI得分下载部分。

此外，要访问Attribution AI得分，您需要具有成功运行状态的服务实例。 要创建新的服务实例，请访问[Attribution AI用户指南](./user-guide.md)。 如果您最近创建了一个服务实例，但该实例仍在训练和评分中，请留出24小时以使它完成运行。

## 查找您的数据集ID {#dataset-id}

在用于Attribution AI分析的服务实例中，单击右上角导航中的&#x200B;*更多操作*&#x200B;下拉列表，然后选择&#x200B;**[!UICONTROL 访问得分]**。

![更多操作](./images/download-scores/more-actions.png)

此时将显示一个新对话框，其中包含指向下载得分文档的链接以及当前实例的数据集ID。 将数据集ID复制到剪贴板中，然后继续执行下一步。

![数据集ID](../customer-ai/images/download-scores/access-scores.png)

## 检索您的批次ID {#retrieve-your-batch-id}

使用上一步中的数据集ID，您需要调用目录API以检索批次ID。 此API调用使用附加查询参数来返回最新的成功批次，而不是返回属于您组织的批次列表。 要返回其他批次，请将`limit`查询参数的数字增加到您希望返回的所需数量。 有关可用查询参数类型的详细信息，请访问有关[使用查询参数筛选目录数据](../../catalog/api/filter-data.md)的指南。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | “访问得分”对话框中可用的数据集ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含批次ID对象的有效负载。 在此示例中，返回对象的键值是批次ID `01E5QSWCAASFQ054FNBKYV6TIQ`。 复制您的批次ID以用于下一个API调用。

>[!NOTE]
>
> 以下响应已重新构建`tags`对象以提高可读性。

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5e8f81cf7a4ecb28a8d85b22"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## 使用您的批次ID检索下一个API调用 {#retrieve-the-next-api-call-with-your-batch-id}

获得批次ID后，您便能够向`/batches`发出新的GET请求。 该请求会返回用作下一个API请求的链接。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步中检索的批次ID [检索您的批次ID](#retrieve-your-batch-id)。 |

**请求**

使用您自己的批次ID提出以下请求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含`_links`对象的有效负载。 在`_links`对象中，有一个值为新API调用的`href`。 复制此值以继续执行下一步。

```json
{
    "data": [
        {
            "dataSetFileId": "01E5QSWCAASFQ054FNBKYV6TIQ-1",
            "dataSetViewId": "5e8f81cf7a4ecb28a8d85b22",
            "version": "1.0.0",
            "created": "1586715582571",
            "updated": "1586715582571",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## 检索文件 {#retrieving-your-files}

使用上一步中获取的`href`值作为API调用，发出新的GET请求以检索文件目录。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 从[上一步](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中返回了dataSetFile ID。 它也可以在`data`数组中的对象类型`dataSetFileId`下访问。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包含一个数据数组，该数据数组可能有一个条目或属于该目录的文件列表。 以下示例包含文件列表，并且已经过压缩以提高可读性。 在此方案中，您需要跟踪每个文件的URL才能访问该文件。

```json
{
    "data": [
        {
            "name": "part-00000-tid-5614147572541837832-908bd66a-d856-47fe-b7da-c8e7d22a4097-1370467-1.c000.snappy.parquet",
            "length": "2380211",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `_links.self.href` | 用于下载目录中文件的GET请求URL。 |


复制`data`数组中任何文件对象的`href`值，然后继续执行下一步。

## 下载您的文件数据

要下载文件数据，请对您在上一步中复制的`"href"`值[检索文件](#retrieving-your-files)发出GET请求。

>[!NOTE]
>
>如果您直接在命令行中发出此请求，则可能会提示您在“请求标头”后添加输出。 以下请求示例使用`--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 从[上一步](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中返回了dataSetFile ID。 |
| `{FILE_NAME}` | 文件的名称。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>在发出GET请求之前，请确保您位于希望将文件保存到的正确目录或文件夹中。

**响应**

响应会将您请求的文件下载到当前目录中。 在此示例中，文件名为“file.parquet”。

![终端](./images/download-scores/terminal-output.png)

下载的分数将采用Parquet格式，并且需要[!DNL Spark]外壳程序或Parquet读取器才能查看分数。 要查看原始得分，您可以使用[Apache Parquet工具](https://parquet.apache.org/docs/)。 Parquet工具可以使用[!DNL Spark]分析数据。

## 后续步骤

本文档概述了下载Attribution AI得分所需的步骤。 有关得分输出的更多信息，请访问[归因人工智能输入和输出](./input-output.md)文档。

## 使用Snowflake访问得分

>[!IMPORTANT]
>
>有关使用Snowflake访问得分的更多详细信息，请联系attributionai-support@adobe.com。

您可以通过Snowflake访问汇总的Attribution AI分数。 目前，您需要通过attributionai-support@adobe.com向Adobe支持发送电子邮件，以便设置和接收用于Snowflake的reader帐户的凭据。

在Adobe支持处理完您的请求后，将为您提供一个URL供读者帐户Snowflake，并提供以下相应的凭据：

- SNOWFLAKEURL
- 用户名
- 密码

>[!NOTE]
>
>读取器帐户用于使用支持JDBC连接器的SQL客户端、工作表和BI解决方案来查询数据。

获得凭据和URL后，您可以查询按接触点日期或转化日期汇总的模型表。

### 在Snowflake中查找架构

使用提供的凭据登录Snowflake。 单击左上主导航中的&#x200B;**工作表**&#x200B;选项卡，然后导航到左侧面板中的数据库目录。

![工作表和导航](./images/download-scores/edited_snowflake_1.png)

接下来，单击屏幕右上角的&#x200B;**选择架构**。 在显示的弹出窗口中，确认选择了正确的数据库。 接下来，单击&#x200B;*架构*&#x200B;下拉列表，并选择其中一个列出的架构。 您可以直接从在所选模式下列出的得分表中进行查询。

![查找架构](./images/download-scores/edited_snowflake_2.png)

## 将PowerBI连接到Snowflake（可选）

可以使用您的Snowflake凭据在PowerBI Desktop和Snowflake数据库之间建立连接。

首先，在&#x200B;*服务器*&#x200B;框下，键入您的SnowflakeURL。 接下来，在&#x200B;*仓库*&#x200B;下，键入“XSMALL”。 然后，键入您的用户名和密码。

![POWERBI示例](./images/download-scores/powerbi-snowflake.png)

建立连接后，选择您的Snowflake数据库，然后选择适当的方案。 现在，您可以加载所有表。
