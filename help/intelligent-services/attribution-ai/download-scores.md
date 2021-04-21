---
keywords: Experience Platform；归因ai；访问得分；热门主题；下载得分；归因ai得分；导出；导出
solution: Experience Platform, Intelligent Services
title: 下载Attribution AI中的分数
topic-legacy: Downloading scores
description: 此文档用于下载Attribution AI的得分。
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 2%

---

# 下载Attribution AI分数

此文档用于下载Attribution AI的得分。

## 入门指南

Attribution AI允许您下载Parce文件格式的分数。 本教程要求您已阅读并完成[入门](./getting-started.md)指南中的下载Attribution AI得分部分。

此外，为了访问Attribution AI的分数，您需要有一个运行状态成功的服务实例可用。 要创建新服务实例，请访问[Attribution AI用户指南](./user-guide.md)。 如果您最近创建了一个服务实例，但它仍在培训和得分，请允许24小时以完成运行。

## 查找数据集ID {#dataset-id}

在Attribution AI分析的服务实例中，单击右上方导航中的&#x200B;*更多操作*&#x200B;下拉列表，然后选择&#x200B;**[!UICONTROL Access scores]**。

![更多操作](./images/download-scores/more-actions.png)

此时将显示一个新对话框，其中包含指向下载得分文档的链接以及当前实例的数据集ID。 将数据集ID复制到剪贴板，然后继续执行下一步。

![数据集 ID](../customer-ai/images/download-scores/access-scores.png)

## 检索批ID {#retrieve-your-batch-id}

使用上一步中的数据集ID，您需要调用目录API以检索批处理ID。 此API调用使用其他查询参数，以返回最新的成功批次，而不是属于您组织的一列表批。 要返回其他批，请将`limit`查询参数的数量增加到希望返回的所需数量。 有关可用查询参数类型的详细信息，请访问有关[使用查询参数筛选目录数据的指南](../../catalog/api/filter-data.md)。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | “Access Scores”（访问分数）对话框中提供的数据集ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含批处理ID对象的有效负荷。 在此示例中，返回对象的键值是批处理ID `01E5QSWCAASFQ054FNBKYV6TIQ`。 复制批处理ID以在下次API调用中使用。

>[!NOTE]
>
> 以下响应已对`tags`对象进行了可读性重新格式化。

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

## 使用您的批ID {#retrieve-the-next-api-call-with-your-batch-id}检索下一个API调用

获得批ID后，您可以对`/batches`发出新GET请求。 该请求返回用作下一个API请求的链接。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步[中检索的批ID可检索您的批ID](#retrieve-your-batch-id)。 |

**请求**

使用您自己的批ID，发出以下请求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含`_links`对象的有效负荷。 在`_links`对象中是一个`href`，其值为新API调用。 复制此值以继续执行下一步。

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

## 检索文件{#retrieving-your-files}

使用上一步中得到的`href`值作为API调用，发出新GET请求以检索文件目录。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID在[上一步](#retrieve-the-next-api-call-with-your-batch-id)的`href`值中返回。 也可以在`data`数组中对象类型`dataSetFileId`下访问它。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包含一个数据数组，该数组可能具有一个条目或属于该目录的文件列表。 以下示例包含文件列表，并已压缩可读性。 在此方案中，您需要按照每个文件的URL来访问该文件。

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

## 下载文件数据

要下载文件GET，请向上一步[中复制的`"href"`值发出数据请求，以检索文件](#retrieving-your-files)。

>[!NOTE]
>
>如果您直接在命令行中发出此请求，可能会提示您在请求标头后添加输出。 以下请求示例使用`--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID在`href`值中从上一步[返回。](#retrieve-the-next-api-call-with-your-batch-id) |
| `{FILE_NAME}` | 文件的名称。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>在发出GET请求之前，请确保您位于要将文件保存到的正确目录或文件夹中。

**响应**

响应将下载您在当前目录中请求的文件。 在此示例中，文件名为“file.parce”。

![终端](./images/download-scores/terminal-output.png)

下载的分数将采用Parce格式，并且需要[!DNL Spark]-shell或Parce阅读器来视图分数。 要查看原始分数，您可以使用[Apache Parce工具](https://github.com/apache/parquet-mr/tree/master/parquet-tools)。 拼花工具可以使用[!DNL Spark]分析数据。

## 后续步骤

此文档概述了下载Attribution AI分数所需的步骤。 有关得分输出的详细信息，请访问[属性AI输入和输出](./input-output.md)文档。

## 使用Snowflake

>[!IMPORTANT]
>
>有关使用Snowflake访问得分的更多详细信息，请与attributionai-support@adobe.com联系。

您可以通过Snowflake访问汇总的Attribution AI分数。 目前，您需要通过电子邮件将Adobe支持发送到attributionai-support@adobe.com，以便设置并接收您的Reader帐户中的Snowflake凭据。

Adobe支持处理您的请求后，将为您提供一个URL，供读者帐户使用，并在下面显示相应的凭据：

- SnowflakeURL
- 用户名
- 密码

>[!NOTE]
>
>Reader帐户用于使用支持JDBC连接器的sql客户端、工作表和BI解决方案查询数据。

拥有凭据和URL后，您便可以查询模型表，按触点日期或转换日期汇总。

### 在Snowflake中查找模式

使用提供的凭据登录到Snowflake。 单击左上方主导航中的&#x200B;**工作表**&#x200B;选项卡，然后导航到左面板中的数据库目录。

![工作表和导航](./images/download-scores/edited_snowflake_1.png)

接下来，单击屏幕右上角的&#x200B;**选择模式**。 在显示的快显窗口中，确认您选择了正确的数据库。 然后，单击&#x200B;*模式*&#x200B;下拉列表，并选择列出的模式之一。 您可以直接从选定查询下列出的得分表进行模式。

![查找模式](./images/download-scores/edited_snowflake_2.png)

## 将PowerBI连接到Snowflake（可选）

您的Snowflake凭据可用于在PowerBI Desktop和Snowflake数据库之间建立连接。

首先，在&#x200B;*Server*&#x200B;框下，键入您的SnowflakeURL。 接下来，在&#x200B;*Warehouse*&#x200B;下，键入“XSMALL”。 然后，键入用户名和密码。

![POWERBI示例](./images/download-scores/powerbi-snowflake.png)

建立连接后，选择Snowflake数据库，然后选择相应的模式。 现在，您可以加载所有表。
