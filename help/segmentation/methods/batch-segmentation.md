---
title: 批量分段指南
description: 了解批量分段，包括内容、如何创建使用批量分段评估的受众，以及如何查看使用批量分段创建的受众。
exl-id: b6fba2fb-8eec-4429-92fd-ece5c79d379d
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---

# 批量分段指南

批量分段是一种分段评估方法，允许您一次移动所有用户档案数据以创建相应的受众。

通过批处理分段，您可以创建详细且丰富的受众，并运行分段作业以确定何时希望将此数据传播到下游服务。

## 符合条件的查询类型 {#query-types}

所有查询均适合批量分段。

## 创建受众 {#create-audience}

您可以创建通过使用分段服务API或通过UI中的受众门户使用批次分段进行评估的受众。

>[!BEGINTABS]

>[!TAB 分段服务API]

**API格式**

```http
POST /segment/definitions
```

**请求**

+++ 用于创建已启用批量分段分段区段定义的示例请求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": true
            },
            "continuous": {
                "enabled": false
            },
            "synchronous": {
                "enabled": false
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**响应**

成功的响应会返回HTTP状态200以及新创建的区段定义的详细信息。

+++创建区段定义时的示例响应。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

有关使用此端点的详细信息，请参阅[区段定义端点指南](../api/segment-definitions.md)。

>[!TAB 受众门户]

在受众门户中，选择&#x200B;**[!UICONTROL 创建受众]**。

![受众门户中突出显示“创建受众”按钮。](../images/methods/batch/select-create-audience.png)

此时会出现弹出窗口。 选择&#x200B;**[!UICONTROL 生成规则]**&#x200B;以进入区段生成器。

![在“创建受众”弹出框中突出显示“生成规则”按钮。](../images/methods/batch/select-build-rules.png)

创建区段定义后，选择&#x200B;**[!UICONTROL 批次]**&#x200B;作为&#x200B;**[!UICONTROL 评估方法]**。

![将显示区段定义。 评估类型已突出显示，显示可以使用流式分段评估区段定义。](../images/methods/batch/batch-evaluation-method.png)

要了解有关创建区段定义的更多信息，请参阅[区段生成器指南](../ui/segment-builder.md)

>[!ENDTABS]

## 检索受众 {#retrieve-audiences}

您可以在UI中使用分段服务API或通过Audience Portal检索使用批次分段评估的所有受众。

>[!BEGINTABS]

>[!TAB 分段服务API]

通过对`/segment/definitions`端点发出GET请求，检索使用贵组织内的批次分段评估的所有区段定义的列表。

**API格式**

您必须在请求路径中包含查询参数`evaluationInfo.batch.enabled=true`，以检索使用批处理分段评估的区段定义。

```http
GET /segment/definitions?evaluationInfo.batch.enabled=true
```

**请求**

+++ 列出所有已启用批次的区段定义的请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.batch.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应会返回HTTP状态200，其中包含组织中使用批处理分段评估的区段定义数组。

+++一个示例响应，其中包含贵组织中所有经过批量分段评估的区段定义的列表

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

有关返回的区段定义的更多详细信息可在[区段定义终结点指南](../api/segment-definitions.md)中找到。

+++

>[!TAB 受众门户]

通过使用Audience Portal中的筛选条件，您可以检索贵组织中支持批量分段的所有受众。 选择![筛选器图标](../../images/icons/filter.png)图标以显示筛选器列表。

![受众门户中突出显示了过滤器图标。](../images/methods/filter-audiences.png)

在可用筛选器内，转到&#x200B;**[!UICONTROL 更新频率]**&#x200B;并选择“[!UICONTROL 批次]”。 使用此过滤器可显示贵组织中使用批处理分段评估的所有受众。

![选择了批次更新频率，显示组织中使用批次分段评估的所有受众。](../images/methods/batch/filter-batch.png)

要了解有关在Experience Platform中查看受众的更多信息，请阅读[受众门户指南](../ui/audience-portal.md)。

>[!ENDTABS]

## 后续步骤

本指南介绍如何创建可使用Adobe Experience Platform上的批量分段评估的区段定义。

要了解有关使用Experience Platform用户界面的更多信息，请参阅[分段用户指南](../ui/overview.md)。

有关批处理分段的常见问题解答，请阅读常见问题解答[&#128279;](../faq.md#batch-segmentation)的批处理分段部分。
