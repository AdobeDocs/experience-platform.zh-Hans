---
title: 重试失败的数据流运行
description: 了解如何使用流服务API重试失败的数据流运行。
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: d4dba26a151619a555a69287e182ff8398cca7b4
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---

# 重试失败的数据流运行

>[!IMPORTANT]
>
>对重试失败的数据流运行支持适用于批处理源。 您只能重试失败的数据流运行。

本教程介绍了有关如何使用重试失败的数据流运行的步骤。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教程要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙盒](../../../sandboxes/home.md)：Experience Platform提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 重试失败的数据流运行

POST要重试失败的数据流运行，请向 `/runs` 端点，同时提供数据流的运行ID和 `re-trigger` 操作作为查询参数的一部分。

**API格式**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 参数 | 描述 |
| --- | --- |
| `{RUN_ID}` | 与要重试的数据流运行对应的运行ID。 |
| `op` | 确定要执行的操作的操作。 要重试失败的数据流运行，必须指定 `re-trigger` 作为你的行动。 |

**请求**

>[!NOTE]
>
>您可以使用 `re-trigger` 在成功的数据流运行没有引入记录的情况下，重试成功的数据流运行的操作。

以下请求会重试为运行ID运行的数据流 `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**响应**

成功的响应会返回新创建的流运行ID及其对应的电子标记版本。

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
