---
keywords: Experience Platform；主页；热门主题；监视数据流；流服务API；流服务
solution: Experience Platform
title: 使用流服务API监控数据流
topic-legacy: overview
type: Tutorial
description: 本教程介绍了使用流服务API监控流程运行数据是否完整、错误和量度的步骤。
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# 使用流服务API监控数据流

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用构建、标记和增强传入数据 [!DNL Platform] 服务。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。 此外，Experience Platform还允许将数据激活给外部合作伙伴。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供了用户界面和RESTful API，所有受支持的源和目标都可从中连接。

本教程介绍使用 [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教程要求您具有有效数据流的ID值。 如果您没有有效的数据流ID，请从 [源概述](../../sources/home.md) 或 [目标概述](../../destinations/catalog/overview.md) ，然后按照在尝试使用本教程之前列出的步骤操作。

此外，本教程还要求您对Adobe Experience Platform的以下组件有一定的了解：

- [目标](../../destinations/home.md):目标是与常用应用程序的预建集成，允许从平台无缝激活数据以用于跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例。
- [源](../../sources/home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便成功地使用 [!DNL Flow Service] API。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Flow Service]，与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

- `Content-Type: application/json`

## 监视器流运行

发出GET流后，请向 [!DNL Flow Service] API。

**API格式**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 独特 `id` 值。 |

**请求**

以下请求检索现有数据流的规范。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回有关流运行的详细信息，包括有关其创建日期、源连接和目标连接以及流运行的唯一标识符(`id`)。

```json
{
    "items": [
        {
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `items` | 包含与您的特定流程运行关联的元数据的单个有效负荷。 |
| `metrics` | 流运行中数据的特性。 |
| `activities` | 显示数据是如何转换的。 |
| `durationSummary` | 流运行的开始和结束时间。 |
| `sizeSummary` | 数据的卷（以字节为单位）。 |
| `recordSummary` | 数据的记录计数。 |
| `fileSummary` | 数据的文件计数。 |
| `fileSummary.extensions` | 包含特定于活动的信息。 例如， `manifest` 只是“促销活动”的一部分，因此会包含在 `extensions` 对象。 |
| `statusSummary` | 显示流量运行是成功还是失败。 |

## 后续步骤

通过阅读本教程，您可以使用 [!DNL Flow Service] API。 您现在可以根据您的摄取计划继续监控数据流，以跟踪其状态和摄取率。 有关如何监视源数据流的信息，请阅读 [使用用户界面监控源的数据流](../ui/monitor-sources.md) 教程。 有关如何监控目标数据流的更多信息，请阅读 [使用用户界面监控目标的数据流](../ui/monitor-destinations.md) 教程。
