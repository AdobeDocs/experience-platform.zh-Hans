---
keywords: Experience Platform；主页；热门主题；流式摄取；摄取；流式多条消息；多条消息；
solution: Experience Platform
title: 在单个HTTP请求中流化多个消息
topic: tutorial
type: Tutorial
description: 此文档提供了一个教程，用于使用流摄取在单个HTTP请求中向Adobe Experience Platform发送多条消息。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 1%

---


# 在单个HTTP请求中发送多条消息

将数据流化到Adobe Experience Platform时，进行大量HTTP调用可能会非常昂贵。 例如，创建1KB有效负荷的1个HTTP请求（每个消息200条，每个消息1KB）比创建200个HTTP请求（单个有效负荷200KB）效率更高。 正确使用时，在单个请求中对多个消息进行分组是优化发送到[!DNL Experience Platform]的数据的最佳方法。

本文档提供了一个教程，用于使用流摄取将多条消息发送到单个HTTP请求中的[!DNL Experience Platform]。

## 入门指南

本教程需要对Adobe Experience Platform[!DNL Data Ingestion]有一定的了解。 在开始本教程之前，请查阅以下文档：

- [数据摄取概述](../home.md):涵盖的核心概念， [!DNL Experience Platform Data Ingestion]包括摄取方法和数据连接器。
- [流摄取概述](../streaming-ingestion/overview.md):流摄取的工作流和构件，如流连接、数据集 [!DNL XDM Individual Profile]和 [!DNL XDM ExperienceEvent]。

本教程还要求您完成对Adobe Experience Platform的[身份验证](https://www.adobe.com/go/platform-api-authentication-en)教程，以成功调用[!DNL Platform] API。 完成身份验证教程将提供本教程中所有API调用所需的授权头值。 示例调用中显示标题，如下所示：

- 授权：载体`{ACCESS_TOKEN}`

所有POST请求都需要附加标题：

- 内容类型：application/json

## 创建流连接

必须先创建流连接，然后才能将流数据开始到[!DNL Experience Platform]。 阅读[创建流连接指南](./create-streaming-connection.md)，了解如何创建流连接。

注册流连接后，作为数据生成者，您将拥有一个唯一的URL，可用于将数据流化到平台。

## 流到数据集

以下示例演示如何在单个HTTP请求中向特定数据集发送多条消息。 将数据集ID插入消息标题中，直接将该消息引入该消息中。

您可以使用[!DNL Platform] UI或在API中使用列表操作获取现有数据集的ID。 在[Experience Platform](https://platform.adobe.com)上可找到数据集ID，方法是转到&#x200B;**[!UICONTROL 数据集]**&#x200B;选项卡，单击您想要ID的数据集，然后从&#x200B;**[!UICONTROL 信息]**&#x200B;选项卡的数据集ID字段复制字符串。 有关如何使用API检索数据集的信息，请参见[目录服务概述](../../catalog/home.md)。

您可以创建新数据集，而不是使用现有数据集。 请阅读[使用API创建数据集](../../catalog/api/create-dataset.md)教程，了解有关使用API创建数据集的详细信息。

**API格式**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 创建的流连接的ID。 |

**请求**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
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

成功的响应返回HTTP状态207（多状态）。 查看响应主体可提供有关请求中执行的每个方法的成功或失败的详细信息。 为请求消息数组的每个元素返回响应。 以下是一个成功响应且没有消息失败的示例：

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

有关状态代码的详细信息，请参见本教程附录中的[响应代码](#response-codes)表。

## 识别失败消息

与使用单个消息发送请求相比，当发送包含多个消息的HTTP请求时，需要考虑其他因素，例如：如何识别数据何时无法发送、哪些特定消息无法发送以及如何检索它们，以及当同一请求中的其他消息失败时成功的数据会发生什么情况。

在继续本教程之前，建议先查看[检索失败批次](../quality/retrieve-failed-batches.md)指南。

### 发送包含有效和无效消息的请求有效负荷

以下示例显示了当批处理包含有效和无效消息时会发生什么情况。

请求有效负荷是表示XDM事件中的模式的JSON对象的数组。 请注意，要成功验证消息，需要满足以下条件：
- 消息标头中的`imsOrgId`字段必须与入口定义匹配。 如果请求有效负荷不包含`imsOrgId`字段，则[!DNL Data Collection Core Service](DCCS)将自动添加该字段。
- 消息标头应引用在[!DNL Platform] UI中创建的现有XDM模式。
- `datasetId`字段需要引用[!DNL Platform]中的现有数据集，其模式符需要与请求主体中包含的每条消息中`header`对象中提供的模式符相匹配。

**API格式**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 创建的数据入口的ID。 |

**请求**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
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

响应有效负荷包括每条消息的状态以及`xactionId`中可用于跟踪的GUID。

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

上面的示例响应显示前一请求的错误消息。 通过将此响应与先前的有效响应进行比较，您可以发现该请求导致部分成功，其中一条消息被成功摄取，三条消息导致失败。 请注意，这两个响应都返回“207”状态代码。 有关状态代码的详细信息，请参见本教程附录中的[响应代码](#response-codes)表。

第一条消息已成功发送到[!DNL Platform]，并且不受其他消息结果的影响。 因此，在尝试重新发送失败的消息时，无需重新包含此消息。

第二条消息失败，因为它缺少消息正文。 集合请求要求消息元素具有有效的标题和正文部分。 在第二条消息的标头之后添加以下代码将修复请求，使第二条消息能够通过验证：

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

第三条消息失败，因为标头中使用的IMS组织ID无效。 IMS组织必须与您尝试发布到的{CONNECTION_ID}匹配。 要确定哪个IMS组织ID与您所使用的流连接相匹配，您可以使用[[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)执行`GET inlet`请求。 有关如何检索先前创建的流连接的示例，请参见[检索流连接](./create-streaming-connection.md#get-data-collection-url)。

第四条消息失败，因为它未遵循预期的XDM模式。 请求标头和正文中包含的`xdmSchema`与`{DATASET_ID}`的XDM模式不匹配。 更正消息标头和正文中的模式允许其通过DCCS验证并成功发送到[!DNL Platform]。 还必须更新消息正文以匹配`{DATASET_ID}`的XDM模式，它才能通过[!DNL Platform]的流验证。 有关成功流入平台的消息会发生什么情况的详细信息，请参见本教程的[确认收录的消息](#confirm-messages-ingested)部分。

### 从[!DNL Platform]检索失败消息

失败消息由响应数组中的错误状态代码标识。
无效消息将收集并存储在`{DATASET_ID}`指定的数据集内的“error”批中。

有关恢复失败的批处理消息的详细信息，请阅读[检索失败的批处理](../quality/retrieve-failed-batches.md)指南。

## 确认已摄取的消息

通过DCCS验证的消息将流式传输到[!DNL Platform]。 在[!DNL Platform]上，在将批邮件引入[!DNL Data Lake]之前，通过流验证对批邮件进行测试。 批状态（无论成功与否）显示在由`{DATASET_ID}`指定的数据集中。

您可以使用[Experience PlatformUI](https://platform.adobe.com)视图成功流入[!DNL Platform]的批处理消息的状态，方法是转到&#x200B;**[!UICONTROL 数据集]**&#x200B;选项卡，单击要流入的数据集，然后检查&#x200B;**[!UICONTROL 数据集活动]**&#x200B;选项卡。

通过[!DNL Platform]流验证的批处理消息将被引入[!DNL Data Lake]。 消息随后可供分析或导出。

## 后续步骤

现在，您了解如何在单个请求中发送多个消息并验证消息何时成功引入目标数据集，因此可以开始将您自己的数据流化到[!DNL Platform]。 有关如何从[!DNL Platform]查询和检索所摄取数据的概述，请参阅[[!DNL Data Access]](../../data-access/tutorials/dataset-data.md)指南。

## 附录

本节包含教程的补充信息。

### 响应代码

下表显示了成功和失败响应消息返回的状态代码。

| 状态代码 | 描述 |
| :---: | --- |
| 207 | 尽管使用“207”作为整体响应状态代码，但收件人需要查阅多状态响应机构的内容，以进一步了解方法执行的成功或失败。 响应代码用于成功、部分成功以及失败情况。 |
| 400 | 请求有问题。 有关更具体的错误消息，请参阅响应正文（例如，消息有效负荷缺少必填字段，或消息为未知xdm格式）。 |
| 401 | 未经授权：请求缺少有效的授权头。 仅对启用身份验证的入口返回此值。 |
| 403 | 未经授权： 提供的授权令牌无效或已过期。 仅对启用身份验证的入口返回此值。 |
| 413 | 负载过大——当总负载请求大于1MB时引发。 |
| 429 | 在指定的时长内请求过多。 |
| 500 | 处理负载时出错。 有关更具体的错误消息，请参阅响应正文(例如，未指定消息有效负荷模式，或与[!DNL Platform]中的XDM定义不匹配)。 |
| 503 | 服务当前不可用。 客户端应使用指数退避策略至少重试3次。 |