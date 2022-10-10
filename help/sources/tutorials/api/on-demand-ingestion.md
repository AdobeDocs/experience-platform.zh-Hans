---
keywords: Experience Platform；主页；热门主题；流程服务；
title: （测试版）使用流量服务API为按需摄取创建流量运行
description: 本教程介绍了使用流量服务API创建针对按需摄取的流量运行的步骤
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 795b1af6421c713f580829588f954856e0a88277
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 1%

---

# （测试版）使用 [!DNL Flow Service] API

>[!IMPORTANT]
>
>按需摄取当前处于测试阶段，您的组织可能还无法访问该摄取。 本文档中描述的功能可能会发生更改。

流运行表示流执行的实例。 例如，如果某个流量计划在上午9:00 、上午10:00和上午11:00每小时运行一次，那么您将有三个流量运行实例。 流量运行特定于您的特定组织。

按需摄取为您提供了创建针对给定数据流运行的流的功能。 这允许用户根据给定参数创建流程运行，并创建摄取周期，而无需服务令牌。 对按需摄取的支持仅适用于批处理源。

本教程介绍有关如何使用按需摄取和使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

>[!NOTE]
>
>要创建流运行，您必须首先具有计划一次性摄取的数据流的流ID。

本教程要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 为基于表的源创建流运行

要为基于表的源创建流，请向 [!DNL Flow Service] API，同时提供要创建运行对象的流的ID以及开始时间、结束时间和增量列的值。

>[!TIP]
>
>基于表的来源包括以下来源类别：广告、分析、同意和偏好、CRM、客户成功、数据库、营销自动化、支付和协议。

**API格式**

```http
POST /runs/
```

**请求**

以下请求为流ID创建流运行 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>您只需提供 `deltaColumn` 创建您的第一个流时运行。 之后， `deltaColumn` 将作为 `copy` 在流中进行转换，并将视为真实的源。 任何更改 `deltaColumn` 值通过流运行参数将导致错误。

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
| `flowId` | 将为其创建流运行的流的ID。 |
| `params.startTime` | 定义运行开始时间的整数。 该值以unix纪元时间表示。 |
| `params.windowStartTime` | 一个整数，用于定义提取数据的窗口的开始时间。 该值以unix时间表示。 |
| `params.windowEndTime` | 一个整数，用于定义提取数据的窗口的结束时间。 该值以unix时间表示。 |
| `params.deltaColumn` | 需要增量列来划分数据，并将新摄取的数据与历史数据分开。 **注意**:的 `deltaColumn` 仅在创建您的第一个流运行时需要。 |
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
| `id` | 新创建的流运行的ID。 请参阅 [检索流量规范](../api/collect/database-nosql.md#specs) 有关基于表的运行规范的详细信息。 |
| `etag` | 运行流的资源版本。 |
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

要为基于文件的源创建流，请向 [!DNL Flow Service] API，同时提供要创建运行对象的流ID以及开始时间和结束时间的值。

>[!TIP]
>
>基于文件的源包括所有云存储源。

**API格式**

```http
POST /runs/
```

**请求**

以下请求为流ID创建流运行 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

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
| `flowId` | 将为其创建流运行的流的ID。 |
| `params.startTime` | 定义运行开始时间的整数。 该值以unix纪元时间表示。 |
| `params.windowStartTime` | 一个整数，用于定义提取数据的窗口的开始时间。 该值以unix时间表示。 |
| `params.windowEndTime` | 一个整数，用于定义提取数据的窗口的结束时间。 该值以unix时间表示。 |

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
| `id` | 新创建的流运行的ID。 请参阅 [检索流量规范](../api/collect/database-nosql.md#specs) 有关基于表的运行规范的详细信息。 |
| `etag` | 运行流的资源版本。 |

## 监控流运行

创建流运行后，您可以监控通过其摄取的数据，以查看有关流运行、完成状态和错误的信息。 要使用API监控您的流量运行，请参阅 [监控API中的数据流 ](./monitor.md). 要使用Platform UI监控流量运行，请参阅 [使用监控仪表板监控源数据流](../../../dataflows/ui/monitor-sources.md).
