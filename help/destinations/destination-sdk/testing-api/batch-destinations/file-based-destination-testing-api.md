---
description: 本页介绍如何使用/testing/destinationInstance API端点来测试是否正确配置了基于文件的目标，以及如何验证流向您配置的目标的数据流的完整性。
title: 使用示例用户档案测试基于文件的目标
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 2%

---

# 使用示例用户档案测试基于文件的目标

## 概述 {#overview}

本页介绍如何使用 `/testing/destinationInstance` 用于测试基于文件的目标是否正确配置，以及验证数据流向您配置的目标的完整性的API端点。

无论是否添加，您都可以向测试端点发出请求 [示例用户档案](file-based-sample-profile-generation-api.md) 呼叫。 如果您未在请求中发送任何用户档案，则API会自动生成一个示例用户档案并将其添加到请求中。

自动生成的示例配置文件包含通用数据。 如果要使用更直观的自定义用户档案数据测试目标，请使用 [配置文件生成API示例](file-based-sample-profile-generation-api.md) 要生成示例用户档案，请自定义其响应，并将其包含在对 `/testing/destinationInstance` 端点。

## 快速入门 {#getting-started}

在继续之前，请查看 [入门指南](../../getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 先决条件 {#prerequisites}

在使用 `/testing/destinationInstance` 端点，确保满足以下条件：

* 您已通过Destination SDK创建了一个基于文件的现有目标，您可以在 [目标目录](../../../ui/destinations-workspace.md).
* 您已在Experience PlatformUI中为目标至少创建了一个激活流程。
* 要成功发出API请求，您需要与要测试的目标实例对应的目标实例ID。 在Platform UI中浏览与目标的连接时，从URL获取应在API调用中使用的目标实例ID。

   ![显示如何从URL获取目标实例ID的UI图像。](../../assets/testing-api/get-destination-instance-id.png)
* *可选*:如果要在测试目标配置时向API调用中添加一个示例配置文件，请使用 [/sample-profiles](file-based-sample-profile-generation-api.md) 端点，以根据您现有的源架构生成示例配置文件。 如果您未提供示例配置文件，API将生成一个配置文件，并在响应中返回该配置文件。

## 在不向调用添加用户档案的情况下测试目标配置 {#test-without-adding-profiles}

**API格式**

```http
POST /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**请求**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| 路径参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 要为其生成示例用户档案的目标实例的ID。 请参阅 [先决条件](#prerequisites) 部分以了解有关如何获取此ID的详细信息。 |

**响应**

成功的响应会返回HTTP状态200以及响应有效负载。

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"crmid-P1A7l"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string",
               "lastName":"string"
            }
         }
      }
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `activations` | 返回每个激活的区段的区段ID和流运行ID。 激活条目数（以及关联的生成文件）等于目标实例上映射的区段数。 <br><br> 示例：如果您将两个区段映射到目标实例，则 `activations` 数组将包含两个条目。 每个激活的区段都将对应一个导出的文件。 |
| `results` | 返回目标实例ID和可用于调用的流运行ID [结果API](file-based-destination-results-api.md)，以进一步测试集成。 |
| `inputProfiles` | 返回由API自动生成的示例用户档案。 |

{style="table-layout:auto"}

## 通过向调用添加的用户档案测试目标配置 {#test-with-added-profiles}

要使用更直观的自定义用户档案数据测试您的目标，您可以自定义从 [/sample-profiles](file-based-sample-profile-generation-api.md) 端点（具有您选择的值），并在对的请求中包含自定义配置文件 `/testing/destinationInstance` 端点。

**API格式**

```http
POST  /testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**请求**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' 
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}'
```

| 参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您正在测试的目标的目标实例ID。  要为其生成示例用户档案的目标实例的ID。 请参阅 [先决条件](#prerequisites) 部分以了解有关如何获取此ID的详细信息。 |
| `profiles` | 可包含一个或多个配置文件的数组。 使用 [配置文件API端点示例](file-based-sample-profile-generation-api.md) 以生成要在此API调用中使用的用户档案。 |

**响应**

成功的响应会返回HTTP状态200以及响应有效负载。

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `activations` | 返回每个激活的区段的区段ID和流运行ID。 激活条目数（以及关联的生成文件）等于目标实例上映射的区段数。 <br><br> 示例：如果您将两个区段映射到目标实例，则 `activations` 数组将包含两个条目。 每个激活的区段都将对应一个导出的文件。 |
| `results` | 返回目标实例ID和可用于调用的流运行ID [结果API](file-based-destination-results-api.md)，以进一步测试集成。 |
| `inputProfiles` | 返回您在API请求中传递的自定义示例用户档案。 |

## API错误处理 {#api-error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤

阅读本文档后，您现在知道如何测试基于文件的目标配置。

如果您收到了有效的API响应，则表明您的目标运行正常。 如果要查看有关激活流程的更多详细信息，可以使用 `results` 属性 [查看详细的激活结果](file-based-destination-results-api.md).

如果您正在构建公共目标，您现在可以 [提交目标配置](../../guides/submit-destination.md) Adobe以供审阅。
