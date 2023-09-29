---
keywords: Experience Platform；主页；热门主题；流服务；
title: 使用流服务API为按需引入创建流运行
description: 了解如何使用流服务API为按需引入创建流运行
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: cea12160656ba0724789db03e62213022bacd645
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 1%

---

# 使用为按需引入创建流运行 [!DNL Flow Service] API

流运行表示流执行的实例。 例如，如果某个流计划在上午9:00、上午10:00和上午11:00每小时运行，则您将运行该流的三个实例。 流量运行特定于您的特定组织。

按需引入允许您针对给定数据流创建流运行。 这允许您的用户基于给定的参数创建流运行并创建引入周期，而不使用服务令牌。 仅对批来源提供按需摄取支持。

本教程涵盖了有关如何使用按需引入以及使用创建流量运行的步骤。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

>[!NOTE]
>
>要创建流运行，您必须首先具有计划为一次性摄取的数据流的流ID。

本教程要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下内容构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 为基于表的源创建流运行

要为基于表的来源创建流，请向以下地址发出POST请求： [!DNL Flow Service] API，同时提供要创建运行的流的ID以及开始时间、结束时间和增量列的值。

>[!TIP]
>
>基于表的源包括以下源类别：广告、分析、同意和偏好设置、CRM、客户成功、数据库、营销自动化、支付和协议。

**API格式**

```http
POST /runs/
```

**请求**

以下请求创建流ID的流运行 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>您只需提供 `deltaColumn` 创建首次流量运行时。 之后， `deltaColumn` 将作为的一部分进行修补 `copy` 流和中的转换将被视为真理的来源。 任何更改 `deltaColumn` 流运行参数的值将导致错误。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `flowId` | 将创建流运行时所针对的流的ID。 |
| `params.startTime` | 按需流运行的计划开始时间。 此值以unix时间表示。 |
| `params.windowStartTime` | 从中检索数据的最早日期和时间。 此值以unix时间表示。 |
| `params.windowEndTime` | 检索数据的日期和时间。 此值以unix时间表示。 |
| `params.deltaColumn` | 需要对数据进行分区并将新摄取的数据与历史数据进行分离。 **注意**：和 `deltaColumn` 仅在创建首次流量运行时才需要。 |
| `params.deltaColumn.name` | 增量列的名称。 |

**响应**

成功的响应会返回新创建的流运行的详细信息，包括其唯一运行 `id`.

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 新创建的流运行的ID。 请参阅指南，网址为 [正在检索流规范](../api/collect/database-nosql.md#specs) 有关基于表的运行规范的详细信息。 |
| `etag` | 流运行的资源版本。 |
<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

## 为基于文件的源创建流运行

POST要为基于文件的源创建流，请向 [!DNL Flow Service] API，同时提供要创建针对的运行的ID以及开始时间和结束时间的值。

>[!TIP]
>
>基于文件的源包括所有云存储源。

**API格式**

```http
POST /runs/
```

**请求**

以下请求创建流ID的流运行 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `flowId` | 将创建流运行时所针对的流的ID。 |
| `params.startTime` | 按需流运行的计划开始时间。 此值以unix时间表示。 |
| `params.windowStartTime` | 从中检索数据的最早日期和时间。 此值以unix时间表示。 |
| `params.windowEndTime` | 检索数据的日期和时间。 此值以unix时间表示。 |

**响应**

成功的响应会返回新创建的流运行的详细信息，包括其唯一运行 `id`.


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 新创建的流运行的ID。 请参阅指南，网址为 [正在检索流规范](../api/collect/database-nosql.md#specs) 有关基于表的运行规范的详细信息。 |
| `etag` | 流运行的资源版本。 |

## 监测流量运行

创建流运行后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 要使用API监控流量运行，请参阅关于的教程 [在API中监控数据流](./monitor.md). 要使用Platform UI监控流量运行，请参阅上的指南 [使用监视仪表板监视源数据流](../../../dataflows/ui/monitor-sources.md).
