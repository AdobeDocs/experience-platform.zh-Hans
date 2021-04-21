---
keywords: Experience Platform；主页；热门主题；监控数据流；流服务api；流服务
solution: Experience Platform
title: 使用Flow Service API监视数据流
topic-legacy: overview
type: Tutorial
description: 本教程介绍使用流服务API监控流运行数据的完整性、错误和量度的步骤。
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# 使用Flow Service API监视数据流

Adobe Experience Platform允许从外部源摄取数据，同时为您提供使用[!DNL Platform]服务构建、标记和增强传入数据的能力。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、数据库和许多其他来源。 此外，Experience Platform还允许将数据激活给外部合作伙伴。

[!DNL Flow Service] 用于收集和集中来自Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有受支持的源和目标都可从中连接。

本教程介绍使用[[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)监视流运行数据的完整性、错误和量度的步骤。

## 入门指南

本教程要求您具有有效数据流的ID值。 如果您没有有效的数据流ID，请从[sources overview](../../sources/home.md)或[目标概述](../../destinations/catalog/overview.md)中选择您选择的连接器，然后按照尝试本教程之前概述的步骤操作。

本教程还要求您对Adobe Experience Platform的以下组件有充分的了解：

- [目标](../../destinations/home.md):目标是与常用应用程序预建集成，允许从平台无缝激活数据，以实现跨渠道营销活动、电子邮件活动、定向广告和许多其他使用案例。
- [来源](../../sources/home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便使用[!DNL Flow Service] API成功监视流运行。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作将在中执行的沙箱的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

- `Content-Type: application/json`

## 监视流运行

创建GET流后，请对[!DNL Flow Service] API执行数据请求。

**API格式**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 要监视的数据流的唯一`id`值。 |

**请求**

以下请求检索现有数据流的规范。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回有关流运行的详细信息，包括有关其创建日期、源和目标连接的信息，以及流运行的唯一标识符(`id`)。

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
            "imsOrgId": "{IMS_ORG_ID}",
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
| `items` | 包含与特定流运行关联的元数据的单个有效负荷。 |
| `metrics` | 流中数据的特性。 |
| `activities` | 显示数据的转换方式。 |
| `durationSummary` | 流运行的开始和结束时间。 |
| `sizeSummary` | 数据的卷（以字节为单位）。 |
| `recordSummary` | 数据的记录计数。 |
| `fileSummary` | 数据的文件计数。 |
| `fileSummary.extensions` | 包含特定于活动的信息。 例如，`manifest`仅是“升级活动”的一部分，因此它随`extensions`对象一起提供。 |
| `statusSummary` | 显示流运行是成功还是失败。 |

## 后续步骤

通过本教程，您已使用[!DNL Flow Service] API检索了有关数据流的量度和错误信息。 现在，您可以根据您的摄取计划继续监视数据流，以跟踪其状态和摄取速率。 有关如何监视源数据流的信息，请阅读使用用户界面](../ui/monitor-sources.md)教程的[监视源数据流。 有关如何监视目标数据流的详细信息，请阅读使用用户界面](../ui/monitor-destinations.md)教程的[监视目标的数据流。
