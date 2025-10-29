---
description: 了解如何使用目标测试API为流式目标生成样本配置文件，以用于目标测试。
title: 根据源架构生成样本配置文件
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 1%

---


# 根据源架构生成样本配置文件 {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API终结点**： `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

此页面列出并描述了您可以使用`/authoring/sample-profiles` API端点执行的所有API操作。

## 为不同的API生成不同的配置文件类型 {#different-profiles-different-apis}

>[!IMPORTANT]
>
>使用此API端点为两个不同的用例生成样本配置文件。 您可以：
>
>* 使用[目标ID](create-template.md)作为查询参数，生成要在&#x200B;*编制和测试消息转换模板*&#x200B;时使用的配置文件。
>* 如果目标配置正确，则生成调用[test时使用的配置文件](streaming-destination-testing-overview.md) — 使用&#x200B;*目标实例ID*&#x200B;作为查询参数。

您可以根据Adobe XDM源架构（在测试目标时使用）或目标支持的目标架构（在构建模板时使用）生成示例配置文件。 要了解Adobe XDM源架构与目标架构之间的区别，请阅读[消息格式](../../functionality/destination-server/message-format.md)文章的概述部分。

请注意，示例配置文件的使用目的不可互换。 基于&#x200B;*目标ID*&#x200B;生成的配置文件只能用于制作消息转换模板，基于&#x200B;*目标实例ID*&#x200B;生成的配置文件只能用于测试目标端点。

## 范例配置文件生成API操作快速入门 {#get-started}

在继续之前，请查看[入门指南](../../getting-started.md)以了解成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 根据测试目标时使用的源架构生成样本配置文件 {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>在[测试您的目标](streaming-destination-testing-overview.md)时，将此处生成的样本配置文件添加到HTTP调用。

您可以基于源架构生成样本配置文件，方法是向`authoring/sample-profiles/`端点发出GET请求，并提供您基于要测试的目标配置创建的目标实例的ID。

要获取目标实例的ID，您必须先在Experience Platform UI中创建与目标的连接，然后再尝试测试目标。 阅读[激活目标教程](../../../ui/activation-overview.md)，并查看下面的提示，了解如何获取要用于此API的目标实例ID。

>[!IMPORTANT]
>
>* 要使用此API，您必须在Experience Platform UI中拥有到目标的现有连接。 阅读[连接到目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)和[将配置文件和受众激活到目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html)以了解详细信息。
>* 建立与目标的连接后，获取在[浏览与目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html)的连接时您应在对此端点的API调用中使用的目标实例ID。
>
>![UI图像如何获取目标实例ID](../../assets/testing-api/get-destination-instance-id.png)

**API格式**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| 查询参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 要基于其生成样本配置文件的目标实例的ID。 |
| `{COUNT}` | *可选*。 您正在生成的样本配置文件数。 参数可以接受`1 - 1000`之间的值。 <br>如果未指定count参数，则生成的默认配置文件数由`maxUsersPerRequest`目标服务器配置[中的](../../authoring-api/destination-server/create-destination-server.md)值决定。 如果未定义此属性，则Adobe将生成一个示例配置文件。 |

{style="table-layout:auto"}


**请求**

以下请求生成由`{DESTINATION_INSTANCE_ID}`和`{COUNT}`查询参数配置的示例配置文件。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回具有指定数量的示例配置文件的HTTP状态200，其中包含与源XDM架构对应的受众成员资格、身份和配置文件属性。

>[!TIP]
>
> 响应仅返回目标实例中使用的受众成员资格、身份和配置文件属性。 即使源架构具有其他字段，这些字段也会被忽略。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| 属性 | 描述 |
| -------- | ----------- |
| `segmentMembership` | 描述个人受众成员资格的映射对象。 有关`segmentMembership`的详细信息，请阅读[受众成员资格详细信息](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)。 |
| `lastQualificationTime` | 此配置文件上次符合区段资格的时间戳。 |
| `xdm:status` | 一个字符串字段，指明在当前请求中是否实现了受众成员资格。 接受以下值： <ul><li>`realized`：配置文件是区段的一部分。</li><li>`exited`：配置文件正在作为当前请求的一部分退出受众。</li></ul> |
| `identityMap` | 描述个人各种身份值及其关联命名空间的映射类型字段。 有关`identityMap`的详细信息，请阅读[架构组合的基础](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#identityMap)。 |

{style="table-layout:auto"}

## 根据构建消息转换模板时使用的目标架构生成样本用户档案 {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>在[渲染模板步骤](render-template-api.md#multiple-profiles-with-body)中，使用在构建模板时生成的示例配置文件。

您可以基于目标架构生成样本配置文件，向`authoring/sample-profiles/`端点发出GET请求，并提供要基于其创建模板的目标配置的目标ID。

>[!TIP]
>
>* 您应在此处使用的目标ID是与使用`instanceId`端点创建的目标配置相对应的`/destinations`。 有关详细信息，请参阅[检索目标配置](../../authoring-api/destination-configuration/retrieve-destination-configuration.md)。

**API格式**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| 查询参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 要基于其生成样本配置文件的目标配置的ID。 |
| `{COUNT}` | *可选*。 您正在生成的样本配置文件数。 参数可以接受`1 - 1000`之间的值。 <br>如果未指定count参数，则生成的默认配置文件数由`maxUsersPerRequest`目标服务器配置[中的](../../authoring-api/destination-server/create-destination-server.md)值决定。 如果未定义此属性，则Adobe将生成一个示例配置文件。 |

{style="table-layout:auto"}

**请求**

以下请求生成由`{DESTINATION_ID}`和`{COUNT}`查询参数配置的示例配置文件。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回具有指定数量的示例配置文件的HTTP状态200，其中包含与目标XDM架构对应的受众成员资格、身份和配置文件属性。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## API错误处理 {#api-error-handling}

Destination SDK API端点遵循常规Experience Platform API错误消息原则。 请参阅Experience Platform疑难解答指南中的[API状态代码](../../../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../../../landing/troubleshooting.md#request-header-errors)。

## 后续步骤

阅读本文档后，您现在知道如何生成样本配置文件，以便在[测试消息转换模板](create-template.md)或[测试目标配置是否正确](streaming-destination-testing-overview.md)时使用。
