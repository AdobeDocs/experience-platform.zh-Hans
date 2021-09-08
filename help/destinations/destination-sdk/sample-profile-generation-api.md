---
description: 本页列出并介绍了可使用“/authoring/sample-profiles” API端点执行的所有API操作，以生成要在目标测试中使用的示例配置文件。
title: 配置文件生成API操作示例
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---

# 配置文件生成API操作示例 {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API端点**:  `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

本页列出并描述了可使用`/authoring/sample-profiles` API端点执行的所有API操作。

此API端点允许您生成要使用的示例配置文件：
* 测试消息转换模板时。 有关更多信息，请参阅[创建和测试消息转换模板](./create-template.md)。
* 测试目标配置是否正确时。 有关更多信息，请参阅[测试目标配置](./test-destination.md)。

您可以根据AdobeXDM源架构或目标支持的目标架构生成示例配置文件。 要了解AdobeXDM源架构和目标架构之间的差异，请阅读[消息格式](./message-format.md)一文。

## 配置文件生成API操作示例快速入门 {#get-started}

在继续操作之前，请查看[快速入门指南](./getting-started.md) ，了解成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 根据源架构生成示例用户档案 {#generate-sample-profiles-source-schema}

您可以根据源架构生成示例配置文件，方法是向`authoring/sample-profiles/`端点发出GET请求，并提供您根据要测试的目标配置创建的目标实例的ID。

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
| `{COUNT}` | *可选*. 要生成的示例用户档案数。 参数可采用`1 - 1000`之间的值。 <br> 如果未指定count参数，则生成的配置文件的默认数量由目标服务 `maxUsersPerRequest` 器配置中 [的值确定](./destination-server-api.md#create)。如果未定义此属性，则Adobe将生成一个示例配置文件。 |


**请求**

以下请求生成由`{DESTINATION_INSTANCE_ID}`和`{COUNT}`查询参数配置的示例配置文件。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `segmentMembership` | 描述个人区段成员资格的映射对象。 有关`segmentMembership`的更多信息，请阅读[区段成员资格详细信息](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)。 |
| `lastQualificationTime` | 此用户档案上次符合区段资格条件的时间戳。 |
| `xdm:status` | 指示区段成员资格是否已作为当前请求的一部分实现。 接受以下值： <ul><li>`existing`:在请求之前，用户档案已经是区段的一部分，并将继续保持其会员资格。</li><li>`realized`:用户档案将在当前请求中输入区段。</li><li>`exited`:该用户档案将作为当前请求的一部分退出该区段。</li></ul> |
| `identityMap` | 映射类型字段，用于描述个人的各种身份值及其关联的命名空间。 有关`identityMap`的更多信息，请阅读[架构组合的基础](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap)。 |


## 根据目标架构生成示例用户档案 {#generate-sample-profiles-target-schema}

您可以根据向`authoring/sample-profiles/`端点发出GET请求的目标架构生成示例配置文件，并根据您创建模板的目标配置提供目标ID。

>[!TIP]
>
>* 您在此应使用的目标ID是与使用`/destinations`端点创建的目标配置对应的`instanceId`。 请参阅[目标配置API引用](./destination-configuration-api.md#retrieve-list)。


**API格式**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| 查询参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 基于生成示例用户档案的目标配置的ID。 |
| `{COUNT}` | *可选*. 要生成的示例用户档案数。 参数可采用`1 - 1000`之间的值。 <br> 如果未指定count参数，则生成的配置文件的默认数量由目标服务 `maxUsersPerRequest` 器配置中 [的值确定](./destination-server-api.md#create)。如果未定义此属性，则Adobe将生成一个示例配置文件。 |

**请求**

以下请求生成由`{DESTINATION_ID}`和`{COUNT}`查询参数配置的示例配置文件。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

目标SDK API端点遵循常规Experience PlatformAPI错误消息原则。 请参阅平台疑难解答指南中的[API状态代码](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes)和[请求标头错误](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)。

## 后续步骤

在阅读本文档后，您现在知道如何生成示例用户档案，以在[测试消息转换模板](./create-template.md)时或在[测试目标是否正确配置](./test-destination.md)时使用。