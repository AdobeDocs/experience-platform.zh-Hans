---
keywords: Experience Platform；归因ai；访问得分；热门主题；下载得分；归因ai得分；导出
feature: Attribution AI
title: 在Attribution AI中下载分数
description: 本文档是下载Attribution AI得分的指南。
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 2%

---

# 下载Attribution AI分数

本文档是下载Attribution AI得分的指南。

## 快速入门

Attribution AI允许您以Parquet文件格式下载分数。 本教程要求您已阅读并完成下载Attribution AI得分部分(位于 [入门](./getting-started.md) 的双曲余切值。

此外，要访问Attribution AI的得分，您需要有一个运行状态成功的服务实例可用。 要创建新的服务实例，请访问 [Attribution AI用户指南](./user-guide.md). 如果您最近创建了一个服务实例，但该实例仍在培训和评分，请允许24小时才能完成运行。

## 查找数据集ID {#dataset-id}

在您的服务实例中，单击 *更多操作* 右上方导航中的下拉列表，然后选择 **[!UICONTROL 访问分数]**.

![更多操作](./images/download-scores/more-actions.png)

此时会显示一个新对话框，其中包含指向下载分数文档的链接以及您当前实例的数据集ID。 将数据集ID复制到剪贴板，然后继续执行下一步。

![数据集 ID](../customer-ai/images/download-scores/access-scores.png)

## 检索批处理ID {#retrieve-your-batch-id}

使用上一步中的数据集ID，您需要调用目录API以检索批处理ID。 此API调用使用其他查询参数，以返回最新的成功批次，而不是属于贵组织的批次列表。 要返回其他批，请增加 `limit` 查询参数的值。 有关可用查询参数类型的更多信息，请访问 [使用查询参数筛选目录数据](../../catalog/api/filter-data.md).

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

成功的响应会返回包含批处理ID对象的有效负荷。 在此示例中，返回对象的键值是批处理ID `01E5QSWCAASFQ054FNBKYV6TIQ`. 复制批量ID以在下一次API调用中使用。

>[!NOTE]
>
> 以下答复已 `tags` 为了可读性而对对象进行了重构。

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

## 使用您的批处理ID检索下一个API调用 {#retrieve-the-next-api-call-with-your-batch-id}

获得批处理ID后，您便能够向 `/batches`. 该请求会返回用作下一个API请求的链接。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步骤中检索的批ID [检索批ID](#retrieve-your-batch-id). |

**请求**

使用您自己的批处理ID，发出以下请求。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回包含 `_links` 对象。 在 `_links` 对象是 `href` 使用新API调用作为其值。 复制此值以继续执行下一步。

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

使用 `href` 作为API调用在上一步中获得的值，请发出新的GET请求以检索您的文件目录。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在 `href` 值 [上一步](#retrieve-the-next-api-call-with-your-batch-id). 也可以在 `data` 对象类型下的数组 `dataSetFileId`. |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包含一个数据数组，该数据数组可能具有一个条目，或属于该目录的文件列表。 以下示例包含一个文件列表，为方便阅读，已对其进行了压缩。 在此方案中，您需要遵循每个文件的URL才能访问该文件。

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
| `_links.self.href` | GET请求URL，用于下载目录中的文件。 |


复制 `href` 值 `data` 数组，然后继续执行下一步。

## 下载文件数据

要下载文件数据，请向 `"href"` 您在上一步中复制的值 [检索文件](#retrieving-your-files).

>[!NOTE]
>
>如果您直接在命令行中发出此请求，则可能会提示您在请求标头之后添加输出。 以下请求示例使用 `--output {FILENAME.FILETYPE}`.

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 在 `href` 值 [上一步](#retrieve-the-next-api-call-with-your-batch-id). |
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
>在发出GET请求之前，请确保您位于您希望将文件保存到的正确目录或文件夹中。

**响应**

响应将下载您在当前目录中请求的文件。 在本例中，文件名为“file.parquet”。

![终端](./images/download-scores/terminal-output.png)

下载的分数将采用Parquet格式，并且要么需要 [!DNL Spark]-shell或Parquet阅读器查看分数。 要查看原始分数，您可以使用 [Apache Parquet Tools](https://parquet.apache.org/docs/). 镶木工具可分析 [!DNL Spark].

## 后续步骤

本文档概述了下载Attribution AI得分所需的步骤。 有关分数输出的详细信息，请访问 [归因AI输入和输出](./input-output.md) 文档。

## 使用Snowflake访问分数

>[!IMPORTANT]
>
>有关使用Snowflake访问分数的更多详细信息，请联系attributionai-support@adobe.com。

您可以通过Snowflake访问汇总Attribution AI得分。 目前，您需要通过电子邮件将Adobe支持发送到attributionai-support@adobe.com，以设置凭据并将凭据接收到您的读者帐户以进行Snowflake。

在Adobe支持处理了您的请求后，将为您提供一个要Snowflake的读者帐户URL以及下面的相应凭据：

- SnowflakeURL
- 用户名
- 密码

>[!NOTE]
>
>读取器帐户用于使用支持JDBC连接器的SQL客户端、工作表和BI解决方案查询数据。

拥有凭据和URL后，您可以查询按接触点日期或转化日期汇总的模型表。

### 在Snowflake中查找架构

使用提供的凭据登录到Snowflake。 单击 **工作表** 选项卡，然后导航到左侧面板中的数据库目录。

![工作表和导航](./images/download-scores/edited_snowflake_1.png)

接下来，单击 **选择架构** 中。 在显示的弹出窗口中，确认您选择了正确的数据库。 接下来，单击 *架构* 下拉列表，然后选择列出的模式之一。 您可以直接从所选架构下列出的得分表中查询。

![查找模式](./images/download-scores/edited_snowflake_2.png)

## 将PowerBI连接到Snowflake（可选）

您的Snowflake凭据可用于在PowerBI Desktop和Snowflake数据库之间设置连接。

首先，在 *服务器* 框中，键入SnowflakeURL。 下一个，下 *仓库*，键入“XSMALL”。 然后，键入您的用户名和密码。

![POWERBI示例](./images/download-scores/powerbi-snowflake.png)

建立连接后，选择Snowflake数据库，然后选择相应的架构。 现在，您可以加载所有表。
