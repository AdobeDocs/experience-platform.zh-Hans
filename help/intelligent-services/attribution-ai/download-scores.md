---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: 在归因AI中获得分数
topic: Accessing scores
translation-type: tm+mt
source-git-commit: 01a500959802aa8c02bdaa8f024a9849ec23be51

---


# 在归因AI中下载得分

此文档用作下载归因AI得分的指南。

## 入门指南

归因AI允许您以镶木地板文件格式下载分数。 本教程要求您已阅读并完成入门指南中的下载归因AI [得分部](./getting-started.md) 分。

此外，要访问归因AI的得分，您需要有一个运行状态成功的服务实例可用。 要创建新服务实例，请访 [问Attribution AI用户指南](./user-guide.md)。 如果您最近创建了一个服务实例，但它仍在培训和评分中，请允许24小时，它才能完成运行。

## Find your dataset ID {#dataset-id}

在Attribution AI洞察的服务实例中，单击右 *上方导航* 中的更多操作下拉菜单，然后选择 **[!UICONTROL Access scores]**。

![更多操作](./images/download-scores/more-actions.png)

此时将显示一个新对话框，其中包含一个指向下载得分文档的链接以及当前实例的数据集ID。 将数据集ID复制到剪贴板，然后继续执行下一步。

![数据集ID](../customer-ai/images/download-scores/access-scores.png)

## 检索批ID {#retrieve-your-batch-id}

使用上一步中的数据集ID，您需要调用目录API以检索批处理ID。 此API调用使用其他查询参数，以返回最新的成功批次，而不是属于您组织的列表批次。 要返回其他批，请将查询参数 `limit` 的数量增加到您希望返回的所需数量。 有关可用查询参数类型的详细信息，请访问有关使用查询参数 [筛选目录数据的指南](../../catalog/api/filter-data.md)。

**API格式**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | “Access Scores”对话框中提供的数据集ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含批ID对象的有效负荷。 在此示例中，返回对象的键值是批处理ID `01E5QSWCAASFQ054FNBKYV6TIQ`。 复制批ID以用于下一个API调用。

>[!NOTE]
> 以下响应已对对象进行 `tags` 了重新格式化，以便可读。

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

## 使用您的批ID检索下一个API调用 {#retrieve-the-next-api-call-with-your-batch-id}

获得批ID后，您便可以向发出新的GET请求 `/batches`。 该请求返回用作下一个API请求的链接。

**API格式**

```http
GET batches/{BATCH_ID}/files
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 在上一步骤中检索的批ID可 [以检索批ID](#retrieve-your-batch-id)。 |

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

成功的响应返回包含对象的有效 `_links` 负荷。 对象 `_links` 中包含 `href` 一个新的API调用作为其值。 复制此值以继续执行下一步。

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

使用上 `href` 一步中获得的值作为API调用，发出新的GET请求以检索文件目录。

**API格式**

```http
GET files/{DATASETFILE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 数据集文件ID以上一步 `href` 中的值 [返回](#retrieve-the-next-api-call-with-your-batch-id)。 也可在对象类型下 `data` 的数组中访问该 `dataSetFileId`项。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

该响应包含一个列表数组，该数组可能具有一个条目或属于该目录的文件的一个数据。 以下示例包含一列表文件，并经过压缩以便可读。 在此情况下，您需要按照每个文件的URL来访问该文件。

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


复制数 `href` 组中任何文件对象的 `data` 值，然后继续执行下一步。

## 下载文件数据

要下载文件数据，请对您在上一步检索 `"href"` 文件时复制的值发出 [GET请求](#retrieving-your-files)。

>[!NOTE] 如果您直接在命令行中发出此请求，可能会提示您在请求标头后添加输出。 以下请求示例使用 `--output {FILENAME.FILETYPE}`。

**API格式**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | 数据集文件ID在上一步 `href` 的值中 [返回](#retrieve-the-next-api-call-with-your-batch-id)。 |
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

>[!TIP] 在发出GET请求之前，请确保您位于要保存文件的正确目录或文件夹中。

**响应**

响应将下载您在当前目录中请求的文件。 在本示例中，文件名为“file.parke”。

![终端](./images/download-scores/terminal-output.png)

## 后续步骤

此文档概述了下载归因AI得分所需的步骤。 您现在可以继续浏览提供 [的其他](../home.md) “智能服务”和指南。

## 使用雪花获得分数

>[!IMPORTANT] 有关使用SnowFlake访问分数的更多详细信息，请与attributionai-support@adobe.com联系。

您可以通过雪花访问聚集的归因人工智能得分。 目前，您需要向attributionai-support@adobe.com发送电子邮件至Adobe支持，以设置并接收Snowflake的读者帐户凭据。

在Adobe支持部门处理您的请求后，将为您提供Snowflake的读者帐户URL和下面的相应凭据：

- 雪花URL
- 用户名
- 密码

>[!NOTE] Reader帐户用于使用支持JDBC连接器的sql客户端、工作表和BI解决方案查询数据。

获得凭据和URL后，您可以查询模型表，按触点日期或转换日期进行聚合。

### 在雪花里寻找模式

使用提供的凭据登录雪花。 单击左 **上角** 的主导航中的“工作表”选项卡，然后导航到左面板中的数据库目录。

![工作表和导航](./images/download-scores/edited_snowflake_1.png)

然后，单 **击屏幕** 右上角的“选择模式”。 在出现的快门窗中，确认您选择了正确的数据库。 接下来，单击 *模式* 下拉列表，然后选择其中一个列出的模式。 您可以直接从所选查询下列出的得分表进行模式。

![查找模式](./images/download-scores/edited_snowflake_2.png)

## 将PowerBI连接到雪花（可选）

您的雪花凭据可用于在PowerBI桌面和雪花数据库之间建立连接。

首先，在“服 *务器* ”框下，键入雪花URL。 然后，在“ *仓库*”下键入“XSMALL”。 然后，键入用户名和密码。

![POWERBI示例](./images/download-scores/powerbi-snowflake.png)

建立连接后，选择Snowflake模式库，然后选择相应的数据。 您现在可以加载所有表。
