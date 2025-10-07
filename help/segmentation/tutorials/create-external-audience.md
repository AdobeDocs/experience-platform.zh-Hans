---
title: 创建和激活外部受众
type: Tutorial
description: 了解如何使用Experience Platform API在Adobe Experience Platform中创建外部受众。
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 3%

---


# 使用API创建和激活外部受众

本教程将介绍使用Adobe Experience Platform API创建外部受众所需的步骤。

## 快速入门

本教程需要对创建外部受众涉及的各种Experience Platform服务有一定的了解。 在开始本教程之前，请阅读以下服务的文档：

- [源](../../sources/home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：允许您从外部数据构建受众。
- [目标](../../destinations/home.md)：目标是预建的与常用应用程序的集成，可无缝激活Experience Platform中的数据，以用于跨渠道营销活动、电子邮件营销活动、定向广告等。

### 必需的标头

本教程还要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用[!DNL Experience Platform] API。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- 授权：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的请求需要一个标头，该标头指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

所有POST、PUT和PATCH请求都需要额外的标头：

- Content-Type： application/json

## 准备外部受众 {#prepare}

在Experience Platform中创建外部受众之前，您需要准备一个包含受众数据的文件。

对于此示例，您应使用CSV文件。 确保您的CSV文件包含&#x200B;**至少**&#x200B;列标识值，如ECID、电子邮件ID或CRM ID。 此外，确保包含分段和激活所需的所有扩充属性。

您还需要确保文件符合Experience Platform架构的要求。 有关创建架构的更多信息，请阅读有关使用API创建架构的[教程](/help/xdm/tutorials/create-schema-api.md)或有关使用UI创建架构的[教程](/help/xdm/tutorials/create-schema-ui.md)。

在您确认CSV文件包含您需要的所有信息并符合架构后，您需要将CSV文件上传到云存储提供商，以便使用源将数据摄取到Experience Platform。 有关使用云存储源的更多信息，请阅读有关使用API[浏览云存储选项的](/help/sources/tutorials/api/explore/cloud-storage.md)教程或[源概述](/help/sources/home.md#cloud-storage)。

## 创建外部受众 {#create}

准备CSV文件后，您现在可以开始创建外部受众的过程。

您可以通过向`/external-audience/`端点发出POST请求来创建外部受众。

提出此请求时，您需要指定以下信息：

- 受众的名称
- 受众描述
- CSV和架构之间的对应字段
- 源规格信息
   - 这包括要摄取的CSV文件的文件路径
      - 文件路径&#x200B;**不能**&#x200B;包含任何空格。 例如，如果您的路径为`activation/sample-source/Example CSV File.csv`，则将路径设置为`activation/sample-source/ExampleCSVFile.csv`。

有关如何使用此端点的更多详细信息，请阅读[外部受众端点指南](/help/segmentation/api/external-audiences.md#create-audience)。

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

+++

发出此请求后，请确保记下您从响应中收到的`operationId`，以便您可以检索受众ID。

## 检索受众ID {#retrieve-audience-id}

现在，您已创建外部受众，您需要获取受众ID，才能将受众摄取到Experience Platform。

您可以通过向`/external-audiences/operations`端点发出GET请求并提供您之前从创建外部受众响应中收到的操作的ID来检索受众ID。

有关如何使用此端点的更多详细信息，请阅读[外部受众端点指南](/help/segmentation/api/external-audiences.md#retrieve-status)。

+++ 请求

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/{OPERATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

发出此请求后，请确保记下从响应中收到的`audienceId`，以便能够触发受众的摄取作业。

## 开始受众引入 {#start-ingestion}

由于您已经拥有`audienceId`，因此现在可以触发将外部受众摄取到Experience Platform中。

您可以在提供受众ID的同时，通过向以下端点发出POST请求来开始受众摄取。 此外，您需要指定开始时间以确定将处理哪些文件。

有关如何使用此端点的更多详细信息，请阅读[外部受众端点指南](/help/segmentation/api/external-audiences.md#start-audience-ingestion)

+++ 请求

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

+++

发出此请求后，请确保记下您从响应中收到的`runId`，以便您可以监视摄取状态。

## 监测摄取状态 {#monitor-ingestion}

触发受众摄取后，您现在可以监视摄取的进度，以确认摄取是否成功并验证受众是否可用于下游激活。

您可以在提供受众和运行ID的同时，通过向以下端点发出GET请求来检索受众摄取状态。

有关如何使用此端点的更多详细信息，请阅读[外部受众端点指南](/help/segmentation/api/external-audiences.md#retrieve-ingestion-status)。

+++ 请求

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs/{RUN_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

## 后续步骤 {#next-steps}

>[!IMPORTANT]
>
>要使用外部生成的受众，您&#x200B;**必须**&#x200B;等待每日分段作业完成。

确认已成功摄取外部受众后，您可以在Audience Portal中看到该受众，并将其用于下游服务，例如目标。

有关受众门户的详细信息，请阅读[受众门户用户界面指南](/help/segmentation/ui/audience-portal.md)。 有关目标的详细信息，请阅读[目标概述](/help/destinations/home.md)。

