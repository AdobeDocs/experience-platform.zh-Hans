---
keywords: Experience Platform；主页；热门主题；流程服务；
title: 重试失败的数据流运行
description: 本教程介绍了如何使用流服务API重试失败的数据流运行的步骤
source-git-commit: dfb95f457d7ddb730950159165ed85b2f532f9ab
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 重试失败的数据流运行

>[!IMPORTANT]
>
>批处理源支持重试失败的数据流运行。 您只能重试失败的数据流运行。

本教程介绍有关如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教程要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 重试失败的数据流运行

要重试失败的数据流运行，请向 `/runs` 端点，同时提供数据流和 `re-trigger` 操作。

**API格式**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 参数 | 描述 |
| --- | --- |
| `{RUN_ID}` | 与要重试的数据流运行对应的运行ID。 |
| `op` | 确定要执行的操作。 要重试失败的数据流运行，必须指定 `re-trigger` 作为您的操作。 |

**请求**

以下请求会重试运行运行ID的数据流 `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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

成功的响应会返回新创建的流运行ID及其相应的标记版本。

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
