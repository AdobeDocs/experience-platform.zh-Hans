---
keywords: Experience Platform；主页；热门主题；批量摄取；批量摄取；部分摄取；部分摄取；检索错误；检索错误；部分批量摄取；部分批量摄取；部分；摄取；摄取；
solution: Experience Platform
title: 部分批量摄取概述
description: 本文档提供了有关管理部分批处理摄取的教程。
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: bc72f77b1b4a48126be9b49c5c663ff11e9054ea
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 9%

---

# 部分批次摄取

部分批量摄取是指在一定阈值内摄取包含错误的数据的能力。 借助此功能，用户可以成功地将其所有正确数据摄取到Adobe Experience Platform，同时对其所有不正确的数据进行单独批处理，并且提供有关其无效原因的详细信息。

本文档提供了有关管理部分批处理摄取的教程。

## 快速入门

本教程需要具备与部分批量摄取相关的各种Adobe Experience Platform服务的实际操作知识。 在开始本教程之前，请查看以下服务的文档：

- [批量摄取](./overview.md)： [!DNL Experience Platform]从数据文件（如CSV和Parquet）摄取和存储数据的方法。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。

以下部分提供成功调用[!DNL Experience Platform] API所需了解的其他信息。

### 正在读取示例 API 调用

本指南提供了示例 API 调用来演示如何格式化请求。这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例 API 调用的文档中所用惯例的信息，请参阅故障排除指南中的[如何读取示例 API 调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform]。

### 收集所需标头的值

为调用 [!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- 授权：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

## 在API中为部分批次摄取启用批次 {#enable-api}

>[!NOTE]
>
>本节介绍如何使用API为部分批量摄取启用批处理。 有关使用UI的说明，请阅读[在UI](#enable-ui)步骤中为部分批次摄取启用批次。

您可以创建一个启用了部分摄取的新批次。

要创建新批次，请按照[批次摄取开发人员指南](./api-overview.md)中的步骤操作。 完成&#x200B;**[!UICONTROL Create batch]**&#x200B;步骤后，在请求正文中添加以下字段：

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 允许[!DNL Experience Platform]生成有关批次的详细错误消息的标志。 |
| `partialIngestionPercent` | 整个批次失败之前可接受的错误百分比。 因此，在此示例中，最多有5%的批次可能是错误，然后才会失败。 |


## 在UI中为部分批次摄取启用批次 {#enable-ui}

>[!NOTE]
>
>本节介绍如何使用UI为部分批次摄取启用批处理。 如果已使用API为部分批次摄取启用批次，则可以跳至下一部分。

要通过[!DNL Experience Platform] UI为部分摄取启用批次，您可以通过源连接创建新批次、在现有数据集中创建新批次或通过“[!UICONTROL Map CSV to XDM flow]”创建新批次。

### 创建新的源连接 {#new-source}

要创建新的源连接，请按照[源概述](../../sources/home.md)中列出的步骤操作。 完成&#x200B;**[!UICONTROL Dataflow detail]**&#x200B;步骤后，请记下&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;和&#x200B;**[!UICONTROL Error diagnostics]**&#x200B;字段。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

**[!UICONTROL Partial ingestion]**&#x200B;切换允许您启用或禁用部分批次摄取。

**[!UICONTROL Error diagnostics]**&#x200B;切换仅在关闭&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切换时显示。 此功能允许[!DNL Experience Platform]生成有关您摄取的批次的详细错误消息。 如果&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切换处于打开状态，则会自动强制实施增强的错误诊断。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;允许您在整个批次失败之前设置可接受错误的百分比。 默认情况下，此值设置为5%。

### 使用现有数据集 {#existing-dataset}

要使用现有数据集，请先选择一个数据集。 右侧边栏会填充有关数据集的信息。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

**[!UICONTROL Partial ingestion]**&#x200B;切换允许您启用或禁用部分批次摄取。

**[!UICONTROL Error diagnostics]**&#x200B;切换仅在关闭&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切换时显示。 此功能允许[!DNL Experience Platform]生成有关您摄取的批次的详细错误消息。 如果&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切换处于打开状态，则会自动强制实施增强的错误诊断。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;允许您在整个批次失败之前设置可接受错误的百分比。 默认情况下，此值设置为5%。

现在，您可以使用&#x200B;**添加数据**&#x200B;按钮上传数据，该数据将使用部分摄取来摄取。

### 使用“[!UICONTROL Map CSV to XDM schema]”流 {#map-flow}

要使用“[!UICONTROL Map CSV to XDM schema]”流程，请按照[映射CSV文件教程](../tutorials/map-csv/overview.md)中列出的步骤操作。 完成&#x200B;**[!UICONTROL Add data]**&#x200B;步骤后，请记下&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;和&#x200B;**[!UICONTROL Error diagnostics]**&#x200B;字段。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

**[!UICONTROL Partial ingestion]**&#x200B;切换允许您启用或禁用部分批次摄取。

**[!UICONTROL Error diagnostics]**&#x200B;切换仅在关闭&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切换时显示。 此功能允许[!DNL Experience Platform]生成有关您摄取的批次的详细错误消息。 如果&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切换处于打开状态，则会自动强制实施增强的错误诊断。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;允许您在整个批次失败之前设置可接受错误的百分比。 默认情况下，此值设置为5%。

## 为现有数据流启用部分摄取和错误诊断

如果在Experience Platform中创建数据流时未启用部分摄取或错误诊断，则您仍然可以启用这些功能而不重新创建数据流。 通过启用部分摄取和强大的错误诊断，您可以极大地增强数据摄取工作流中的可靠性和故障排查的便利性。 请阅读以下部分，了解如何使用[!DNL Flow Service] API为现有数据流启用部分摄取和错误诊断。

默认情况下，数据流可能没有启用部分摄取或错误诊断。 这些功能有助于识别和隔离数据摄取期间的问题。 使用[!DNL Flow Service] API，您可以检索当前数据流配置，并使用PATCH请求应用必要的更改。

按照以下步骤为现有数据流启用部分摄取和错误诊断。

### 检索流详细信息

要检索数据流配置，请向`/flows/{FLOW_ID}`端点发出GET请求，并提供数据流的ID。 有关检索数据流详细信息的详细信息，请参阅[使用 [!DNL Flow Service] API](../../sources/tutorials/api/update-dataflows.md)更新数据流指南。

确保保存响应中返回的`etag`字段的值。 这对于更新请求来说是必需的，以确保版本一致性。

### 更新流配置

接下来，向`/flows/`端点发出PATCH请求，并提供要为其启用部分摄取和错误诊断的数据流的ID。

>[!IMPORTANT]
>
>- 使用If-Match键在请求标头中包含之前保存的`etag`值。
>- 您可以修改`partialIngestionPercent`值以满足您的特定需求。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
        {
            "op": "add",
            "path": "/options",
            "value": {
                "partialIngestionPercent": "10"
            }
        },
        {
            "op": "add",
            "path": "/options/errorDiagnosticsEnabled",
            "value": true
        }
    ]'
```

**响应**

成功的响应返回数据流的`id`和更新的`etag`。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

### 验证更新

PATCH完成后，发出GET请求并检索您的数据流，以验证更改是否已成功完成。

**API格式**

```http
GET /flows/{FLOW_ID}
```

**请求**

以下请求将检索有关您的流ID的更新信息。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应将返回您的数据流详细信息，确认现在已在`options`部分启用部分摄取和错误诊断。

```json
"options": {
    "partialIngestionPercent": 10,
    "errorDiagnosticsEnabled": true
}
```

## 后续步骤 {#next-steps}

本教程介绍了如何创建或修改数据集以启用部分批次摄取。 有关批量摄取的更多信息，请阅读[批量摄取开发人员指南](./api-overview.md)。

有关监控部分摄取错误的信息，请阅读[批处理摄取错误诊断指南](../quality/error-diagnostics.md)。
