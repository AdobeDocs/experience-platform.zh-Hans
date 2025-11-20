---
title: 灵活的受众评估指南
description: 了解如何使用灵活的受众评估来按需运行批量分段作业。
role: Developer, User
exl-id: b85bf735-be02-4bf7-bd63-8d74ae905e58
source-git-commit: 7a0a98ea035892943a0e9a9a2b059701f6f1f612
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 5%

---

# 灵活的受众评估指南

>[!AVAILABILITY]
>
>灵活的受众评估是&#x200B;**仅限**，在[!DNL Microsoft Azure]上运行的Experience Platform实例上可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../landing/multi-cloud.md)。
>
>此外，灵活的受众评估是&#x200B;**仅限**&#x200B;可用于Real-Time CDP B2C Edition。

灵活的受众评估允许您按需运行批量分段作业。 通过灵活的受众评估，您可以运行临时活动发布、及时通信或其他时效性活动。

## 护栏 {#guardrails}

>[!CONTEXTUALHELP]
>id="platform_segmentation_browse_flexibleaudienceevaluation"
>title="灵活的受众评估限制"
>abstract="您可以在一次灵活的受众评估中评估最多 20 位受众。<br/><br/>此外，虽然评估作业会尽快运行，但由于按需评估<b>不能</b>与另一个按需或批次评估同时运行，因此可能会出现系统延迟。"

在运行灵活的受众评估时，请牢记以下条件：

- 每个沙盒每天只能使用灵活的受众评估&#x200B;**两次**。 此限制在午夜(UTC)重置。
- 您每&#x200B;**生产**&#x200B;沙盒每年最多有&#x200B;**个**&#x200B;灵活的受众评估运行，共50个。
- 您每&#x200B;**开发**&#x200B;沙盒每年最多有&#x200B;**次**&#x200B;运行100次灵活受众评估。
- 所有受众&#x200B;**都必须**&#x200B;具有“分段服务”的来源。
- 必须使用批处理分段评估所有受众&#x200B;**&#x200B;**。
- 所有受众&#x200B;**必须**&#x200B;是基于人员的受众。
- 每个灵活受众评估运行最多只能选择20个受众。

>[!NOTE]
>
>您可以每年购买额外的灵活受众评估运行。 有关更多信息，请联系Adobe客户关怀部门。

## 访问 {#access}

要使用灵活的受众评估，您必须具有以下权限：

- **[!UICONTROL Evaluate Segment to an Audience]**&#x200B;部分下的&#x200B;**[!DNL Profile Management]**。

有关基于角色的访问控制的详细信息，请阅读[访问控制概述](../../access-control/home.md)。

## 运行灵活的受众评估

您可以使用Experience Platform API或UI运行灵活的受众评估。

>[!BEGINTABS]

>[!TAB Experience Platform API]

要在Experience Platform API中运行灵活的受众评估，您需要创建一个区段作业，其中包含您要评估的所有区段定义（受众）的ID。

>[!NOTE]
>
>您只能为每个区段作业API调用添加&#x200B;**个最多**&#x200B;个20个区段定义ID。

您可以通过向`/segment/jobs`端点发出POST请求并在请求正文中包含区段定义的ID来创建新的区段作业。

+++用于创建新区段作业的示例请求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `segmentId` | 要评估的区段定义的ID。 这些区段定义可以属于不同的合并策略。 |

+++

成功的响应返回HTTP状态200，其中包含有关新创建的区段作业的信息。

+++ 创建新区段作业时的示例响应。

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

+++

创建区段作业后，您可以通过向`/segment/jobs`端点发出GET请求来检查其状态，在请求路径中提供新创建的区段作业的ID。

+++检索区段作业的示例请求

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

成功的响应返回HTTP状态200，其中包含有关指定区段作业的详细信息。


+++ 用于检索区段作业的示例响应。

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

+++

>[!TAB Experience Platform UI]

要在Experience Platform UI中运行灵活的受众评估，请在&#x200B;**[!UICONTROL Audiences]**&#x200B;部分中选择&#x200B;**[!UICONTROL Customers]**。

![“客户”部分中的“受众”按钮高亮显示。 将显示客户配置文件的受众门户。](../images/methods/fae/audience-portal.png)

此时将显示“受众门户”，其中包含组织内所有人员受众的列表。 在Audience Portal中，您可以选择要评估的受众并选择&#x200B;**[!UICONTROL Evaluate audience]**。

![已选择您要对其使用灵活受众评估的受众。](../images/methods/fae/evaluate-audiences.png)

此时将显示&#x200B;**[!UICONTROL Evaluate audiences on demand]**&#x200B;弹出框，其中显示了将使用按需区段作业评估的受众列表。 如果受众不符合按需评估的条件，则它将被自动从评估作业中删除。 确认列出的受众就是您要评估的受众。

![显示可以使用灵活受众评估进行评估的受众。](../images/methods/fae/evaluate-audiences-modal.png)

确认列出了正确的受众后，您可以继续请求，并将开始灵活的受众评估。 您可以在[评估作业监视视图](../../dataflows/ui/monitor-audiences.md#evaluation-job-details)中查看此受众评估的状态。

>[!NOTE]
>
>区段作业的状态可能会在监控仪表板中报告为“已排队”状态。 您可以查看区段作业的最新状态，方法是向`/segment/jobs`端点发出GET请求，并在请求路径中提供区段作业的ID。 在“API”选项卡中可找到有关使用此端点的更多信息。
>
>如果您运行灵活的受众评估，并希望评估将受众激活到目标，则需要确保将频率设置为&#x200B;**[!UICONTROL After segment evaluation]**。 对已设置为在区段评估[后](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files)激活的受众运行灵活的受众评估，将在灵活的受众评估作业完成后立即激活受众，而不考虑任何之前的每日激活作业。

>[!ENDTABS]

## 视频 {#video}

以下视频演示了如何在Experience Platform中访问和使用灵活的受众评估。

>[!VIDEO](https://video.tv.adobe.com/v/3453650?captions=chi_hans&)

## 常见问题解答 {#faq}

以下部分列出了与灵活受众评估相关的常见问题解答。

### 使用灵活的受众评估多久才能激活受众？

+++ 回答

您可以在创建受众后立即使用灵活的受众评估激活受众。

+++

### 灵活的受众评估需要多长时间？

+++ 回答

灵活的受众评估工作最多可能需要四个小时才能完成。

+++

### 我能否通过灵活的受众评估运行计划？

+++ 回答

不可以，计划无法用于灵活的受众评估。

+++

### 使用灵活的受众评估时，是否需要运行额外的导出作业？

+++ 回答

不会，导出作业将在相应的区段作业完成后自动运行。

+++

### 我可以使用通过灵活受众评估评估的受众来获取哪些服务？

+++ 回答

您可以在所有下游服务(包括目标和Adobe Journey Optimizer历程)中使用受众。

+++

### 何时重置灵活的受众评估限制？

+++ 回答

每日限制在午夜(UTC)重置。 年度限制将在合同的周年日期重置。

+++

### 灵活的受众评估支持哪些类型的受众？

+++ 回答

灵活的受众评估仅支持分段服务来源的受众。 灵活的受众评估不支持其他受众，例如组合、自定义上传或数据Distiller。

+++

### 哪些运行有助于我的灵活受众评估运行计数？

+++ 回答

使用API或UI创建的灵活受众评估运行接近最大限制。 但是，夜间运行的每日批处理分段作业不会&#x200B;**导致**&#x200B;超出此限制。

+++

### 通过灵活的受众评估来评估主要受众时，是否需要评估所有依赖的受众？

+++ 回答

不是。灵活的受众评估将自动评估所有依赖的受众。 例如，如果受众A依赖于受众B，则您只需要评估受众B。灵活的受众评估将自动评估受众A，然后评估受众B。

+++
