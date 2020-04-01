---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在一个HTTP请求中流化多个消息
topic: tutorial
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# 在一个HTTP请求中发送多个消息

将数据流化到Adobe Experience Platform时，进行大量HTTP调用可能非常昂贵。 例如，创建1KB负载的200个HTTP请求，而不是创建1KB负载的200个HTTP请求，创建1个HTTP请求，每个消息200条，单个负载200KB，效率更高。 正确使用时，在一个请求中对多个消息进行分组是优化发送到Experience Platform的数据的极好方法。

本文档提供了一个教程，用于在使用流摄取的单个HTTP请求中向Experience Platform发送多条消息。

## 入门指南

本教程需要对Adobe Experience Platform数据摄取有充分的了解。 在开始本教程之前，请查看以下文档：

- [数据摄取概述](../home.md):涵盖Experience Platform Data Ingestion的核心概念，包括Ingestion方法和数据连接器。
- [流摄取概述](../streaming-ingestion/overview.md):流摄取的工作流和构建块，如流连接、数据集、XDM个人用户档案和XDM ExperienceEvent。

本教程还要求您完成对Adobe Experience Platform [的身份验证](../../tutorials/authentication.md) ，以成功调用平台API。 完成身份验证教程为本教程中所有API调用所需的授权头提供值。 标题在示例调用中显示如下：

- 授权：承载人 `{ACCESS_TOKEN}`

所有POST请求都需要额外的标题：

- 内容类型：application/json

## 创建流连接

必须首先创建流连接，然后才能将流数据开始到Experience Platform。 阅读创 [建流连接指南](./create-streaming-connection.md) ，了解如何创建流连接。

在注册流连接后，作为数据生成者，您将拥有一个唯一的URL，可用于向平台流化数据。

## 流到数据集

以下示例演示如何在单个HTTP请求中向特定数据集发送多条消息。 在消息标题中插入数据集ID，将该消息直接引入其中。

您可以使用平台UI或使用API中的列表操作获取现有数据集的ID。 可以在 [Experience Platform](https://platform.adobe.com) ，通过转到“数据集”选项卡，单击您要为其提供ID的数据集，然后从 **Dataset ID** Field复制数据集ID(位于 ******** InfoAdobest选项卡上)字段中的数据集ID。 有关如 [何使用API检索数据集的信息](../../catalog/home.md) ，请参阅Catalog Service概述。

您可以创建新数据集，而不是使用现有数据集。 有关使用API [创建数据集的更多信息](../../catalog/api/create-dataset.md) ，请阅读使用API创建数据集教程。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 创建的流连接的ID。 |

**请求**

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Fernie Snow",
              "quantity": 30,
              "priceTotal": 7.8
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "gregdorcey@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "7af6adcc-dc9e-4692-b826-55d2abe68c11",
          "timestamp": "2019-02-23T22:07:31Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "emilyong@example.com"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**响应**

成功的响应会返回HTTP状态207（多状态）。 查看响应主体可提供有关请求中执行的每个方法的成功或失败的更多详细信息。 为请求消息数组的每个元素返回响应。 以下是一个成功响应且没有消息失败的示例：

```json
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565628583792:1485:153",
    "receivedTimeMs": 1565628583854,
    "responses": [
        {
            "xactionId": "1565628583792:1485:153:0"
        },
        {
            "xactionId": "1565628583792:1485:153:1"
        }
    ]
}
```

有关状态代码的详细信息，请参阅本教 [程附录中](#response-codes) “响应代码”表。

## 识别失败的消息

与使用单条消息发送请求相比，当发送具有多条消息的HTTP请求时，需要考虑其他因素，例如：如何识别数据何时无法发送、哪些特定消息无法发送以及如何检索它们，以及当同一请求中的其他消息失败时成功的数据会发生什么情况。

继续本教程之前，建议先查看检索失败 [的批次指南](../quality/retrieve-failed-batches.md) 。

### 发送包含有效和无效消息的请求有效负荷

以下示例显示了当批处理包含有效和无效消息时会发生什么情况。

请求有效负荷是表示XDM事件中的模式的JSON对象的数组。 请注意，要成功验证消息，需要满足以下条件：
- 消 `imsOrgId` 息标题中的字段必须与入口定义匹配。 如果请求有效负荷不包括字 `imsOrgId` 段，则Data Collection Core Service(DCCS)将自动添加该字段。
- 消息标头应引用在平台UI中创建的现有XDM模式。
- 字 `datasetId` 段需要引用平台中的现有数据集，其模式需要匹配请求主体中包含的每条消息中对象 `header` 中提供的模式。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 创建的数据引入的ID。 |

**请求**

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "rogerkanagawa@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "mohandeewar@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
   {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          }
        }
      }
    },
    {
      "header": {
        "msgType": "xdmEntityCreate",
        "msgId": "79d2e715-f25f-4c36",
        "xdmSchema": {
          "name": "_xdm.context.experienceevent"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "xdmSchema": {
            "name": "_xdm.context.experienceevent"
          }
        },
        "xdmEntity": {
          "_id": "abc",
          "dataSource": {
            "_id": "http://abc.com/abc"
          },
          "timestamp": "2018-05-18T15:28:25Z",
          "endUserIDs": {
            "_vendor": {
              "adobe": {
                "experience": {
                  "mcId": {
                    "id": "http://abc.com/abc"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**响应**

响应有效负荷包括每条消息的状态，以及可用于跟踪 `xactionId` 的GUID。

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        }
    ]
}
```

上面的示例响应显示了上一个请求的错误消息。 通过将此响应与之前的有效响应进行比较，您可以发现请求导致部分成功，成功摄取了一条消息，并有三条消息导致失败。 请注意，这两个响应都返回“207”状态代码。 有关状态代码的详细信息，请参阅本教 [程附录中](#response-codes) “响应代码”表。

第一条消息已成功发送到平台，并且不受其他消息结果的影响。 因此，在尝试重新发送失败的消息时，您无需重新包含此消息。

第二条消息之所以失败，是因为它缺少消息正文。 集合请求要求消息元素具有有效的标题和正文部分。 在第二条消息中的标头之后添加以下代码将修复请求，使第二条消息通过验证：

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

第三条消息失败，因为标题中使用的IMS组织ID无效。 IMS组织必须与您尝试发布到的{CONNECTION_ID}匹配。 要确定哪个IMS组织ID与您使用的流连接匹配，您可以使用数 `GET inlet` 据摄取API [执行请求](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)。 有关 [如何检索先前创建的流连接的示例](./create-streaming-connection.md#get-data-collection-url) ，请参阅检索流连接。

第四条消息失败，因为它未遵循预期的XDM模式。 请 `xdmSchema` 求的标头和正文中包含的内容与的XDM模式不匹配 `{DATASET_ID}`。 更正消息标头和正文中的模式允许其通过DCS验证并成功发送到平台。 还必须更新消息正文以匹配消息的XDM模式，以 `{DATASET_ID}` 便其通过平台上的流验证。 有关成功流到平台的消息会发生什么情况的详细信息，请参阅本教 [程中收录的确认消息](#confirm-messages-ingested) 一节。

### 从平台检索失败消息

故障消息由响应数组中的错误状态代码标识。
无效消息将收集并存储在由指定的数据集内的“错误”批次中 `{DATASET_ID}`。

有关恢复 [失败的批消息的更多信息](../quality/retrieve-failed-batches.md) ，请阅读检索失败的批消息指南。

## 确认已摄取的消息

通过DCS验证的消息会流式传输到平台。 在Platform上，批量消息在被引入数据湖之前，通过流验证进行测试。 批次状态（无论成功与否）显示在由指定的数据集中 `{DATASET_ID}`。

您可以视图使用 [Experience Platform UI成功流化到平台的批量消息状态，方法是转到“数据集”选项卡，单击要流化到的数据集，然后检查“数据集活动”选项](https://platform.adobe.com) 卡 ******** 。

通过平台流验证的批量消息会被引入数据湖中。 这些消息随后可供分析或导出。

## 后续步骤

现在，您知道如何在一个请求中发送多个消息并验证消息何时成功引入目标数据集，因此可以开始将您自己的数据流化到平台。 有关如何从平台查询和检索摄取的数据的概述，请参阅《数据访 [问指南](../../data-access/tutorials/dataset-data.md) 》。

## 附录

本节包含教程的补充信息。

### 响应代码

下表显示了成功和失败的响应消息返回的状态代码。

| 状态代码 | 描述 |
| :---: | --- |
| 207 | 尽管使用“207”作为整体响应状态代码，但收件人需要查阅多状态响应主体的内容以进一步了解关于方法执行的成功或失败的信息。 响应代码用于成功、部分成功以及失败情况。 |
| 400 | 请求有问题。 有关更具体的错误消息，请参阅响应正文（例如，消息有效负荷缺少必填字段，或消息为未知的xdm格式）。 |
| 401 | 未授权：请求缺少有效的授权头。 仅对启用了身份验证的入口返回。 |
| 403 | 未授权： 提供的授权令牌无效或已过期。 仅对启用了身份验证的入口返回。 |
| 413 | 负载过大——当总负载请求大于1MB时引发。 |
| 429 | 在指定的时长内请求过多。 |
| 500 | 处理有效负荷时出错。 有关更具体的错误消息，请参阅响应正文(例如，未指定消息有效负荷模式，或与平台中的XDM定义不匹配)。 |
| 503 | 服务当前不可用。 客户端应使用指数后退策略至少重试3次。 |