---
description: 本页列出并介绍了可使用“/authoring/sample-profiles” API端点执行的所有API操作，以生成要在目标测试中使用的示例配置文件。
title: 配置文件生成API操作示例
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 2%

---

# 配置文件生成API操作示例 {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API端点**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

本页列出并介绍了您可以使用 `/authoring/sample-profiles` API端点。

## 为不同的API生成不同的配置文件类型 {#different-profiles-different-apis}

>[!IMPORTANT]
>
>使用此API端点可为两个不同的用例生成示例配置文件。 您可以：
>* 生成用于 [构建和测试报文转换模板](./create-template.md)  — 使用 *目标ID* 作为查询参数。
>* 生成要在进行调用时使用的用户档案 [测试目标是否配置正确](./test-destination.md)  — 使用 *目标实例ID* 作为查询参数。


您可以根据AdobeXDM源架构（在测试目标时使用）或目标支持的目标架构（在制作模板时使用）生成示例用户档案。 要了解AdobeXDM源架构与目标架构之间的差异，请阅读 [消息格式](./message-format.md) 文章。

请注意，可用于使用示例用户档案的目的不可互换。 根据 *目标ID* 只能用于编写基于生成的消息转换模板和用户档案 *目标实例ID* 只能用于测试目标端点。

## 配置文件生成API操作示例快速入门 {#get-started}

在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 根据测试目标时使用的源架构生成示例用户档案 {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>将此处生成的示例配置文件添加到HTTP调用(当 [测试目标](./test-destination.md).

您可以通过向 `authoring/sample-profiles/` 端点，并提供您根据要测试的目标配置创建的目标实例的ID。

要获取目标实例的ID，您必须先在Experience PlatformUI中创建与目标的连接，然后才能尝试测试目标。 阅读 [激活目标教程](/help/destinations/ui/activation-overview.md) 并查看下面的提示，了解如何获取要用于此API的目标实例ID。

>[!TIP]
>
>* 从URL中获取您在浏览与目标的连接时应在此处使用的目标实例ID。
   >![UI图像如何获取目标实例ID](./assets/get-destination-instance-id.png)


**API格式**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| 查询参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您生成示例用户档案所依据的目标实例的ID。 |
| `{COUNT}` | *可选*. 要生成的示例用户档案数。 参数可以采用 `1 - 1000`. <br> 如果未指定count参数，则生成的配置文件的默认数量由 `maxUsersPerRequest` 值 [目标服务器配置](./destination-server-api.md#create). 如果未定义此属性，则Adobe将生成一个示例配置文件。 |

{style=&quot;table-layout:auto&quot;}


**请求**

以下请求会生成由 `{DESTINATION_INSTANCE_ID}` 和 `{COUNT}` 查询参数。

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

成功响应会返回具有指定数量的示例配置文件的HTTP状态200，其中区段成员资格、标识和配置文件属性与源XDM架构相对应。

>[!TIP]
>
> 响应仅返回在目标实例中使用的区段成员资格、标识和配置文件属性。 即使源架构具有其他字段，也会忽略这些字段。

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
| `segmentMembership` | 描述个人区段成员资格的映射对象。 有关 `segmentMembership`，读取 [区段成员资格详细信息](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | 此用户档案上次符合区段资格条件的时间戳。 |
| `xdm:status` | 指示区段成员资格是否已作为当前请求的一部分实现。 接受以下值： <ul><li>`existing`:在请求之前，用户档案已经是区段的一部分，并将继续保持其会员资格。</li><li>`realized`:用户档案将在当前请求中输入区段。</li><li>`exited`:该用户档案将作为当前请求的一部分退出该区段。</li></ul> |
| `identityMap` | 映射类型字段，用于描述个人的各种身份值及其关联的命名空间。 有关 `identityMap`，读取 [模式组合的基础](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style=&quot;table-layout:auto&quot;}

## 根据构建消息转换模板时要使用的目标模式生成示例用户档案 {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>使用在构建模板时在此处生成的示例用户档案，位于 [渲染模板步骤](./render-template-api.md#multiple-profiles-with-body).

您可以根据向发送GET请求的目标架构生成示例用户档案 `authoring/sample-profiles/` 端点，并提供基于您创建模板的目标配置的目标ID。

>[!TIP]
>
>* 您在此应使用的目标ID是 `instanceId` 对应于目标配置的 `/destinations` 端点。 请参阅 [目标配置API引用](./destination-configuration-api.md#retrieve-list).


**API格式**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| 查询参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 基于生成示例用户档案的目标配置的ID。 |
| `{COUNT}` | *可选*. 要生成的示例用户档案数。 参数可以采用 `1 - 1000`. <br> 如果未指定count参数，则生成的配置文件的默认数量由 `maxUsersPerRequest` 值 [目标服务器配置](./destination-server-api.md#create). 如果未定义此属性，则Adobe将生成一个示例配置文件。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会生成由 `{DESTINATION_ID}` 和 `{COUNT}` 查询参数。

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

成功响应会返回HTTP状态200，其中包含指定数量的示例配置文件，以及与目标XDM架构对应的区段成员资格、标识和配置文件属性。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "existing"
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
                    "status": "existing"
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
                    "status": "existing"
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

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤

阅读本文档后，您现在知道如何生成要在 [测试消息转换模板](./create-template.md) 或 [测试目标是否配置正确](./test-destination.md).
