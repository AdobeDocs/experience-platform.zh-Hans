---
keywords: Experience Platform；主页；热门主题；流式摄取；摄取；流式传输多条消息；多条消息；
solution: Experience Platform
title: 在一个HTTP请求中发送多条消息
type: Tutorial
description: 本文档提供了一个教程，介绍如何使用流摄取，在一个HTTP请求中向Adobe Experience Platform发送多条消息。
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 3ad5c06db07b360df255d3afb1c177cc5de613bb
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 1%

---

# 在一个HTTP请求中发送多条消息

将数据流式传输到Adobe Experience Platform时，进行大量HTTP调用可能会很昂贵。 例如，创建1个HTTP请求（每个请求200条1 KB的消息，单个有效负载为200 KB）要比创建200个1 KB的HTTP请求有效得多。 正确使用时，在单个请求中对多个消息进行分组是优化发送数据的好方法 [!DNL Experience Platform].

本文档提供了有关将多条消息发送到的教程 [!DNL Experience Platform] 使用流式摄取在一个HTTP请求中。

## 快速入门

本教程需要您对Adobe Experience Platform有一定的了解 [!DNL Data Ingestion]. 在开始本教程之前，请查看以下文档：

- [数据引入概述](../home.md)：涵盖 [!DNL Experience Platform Data Ingestion]，包括摄取方法和Data Connectors。
- [流式摄取概述](../streaming-ingestion/overview.md)：流摄取的工作流程和构建块，例如流连接、数据集、 [!DNL XDM Individual Profile]、和 [!DNL XDM ExperienceEvent].

此外，本教程还要求您已完成 [对Adobe Experience Platform的身份验证](https://www.adobe.com/go/platform-api-authentication-en) 要成功调用到的教程 [!DNL Platform] API。 完成身份验证教程将为本教程中所有API调用所需的Authorization标头提供值。 标头在示例调用中如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`

所有POST请求都需要额外的标头：

- Content-Type： application/json

## 创建流连接

必须先创建流连接，然后才能开始将数据流式传输到 [!DNL Experience Platform]. 阅读 [创建流连接](./create-streaming-connection.md) 有关如何创建流连接的指南。

注册流连接后，作为数据制作者，您将拥有一个唯一的URL，可用于将数据流式传输到Platform。

## 流到数据集

以下示例显示如何在单个HTTP请求中向特定数据集发送多条消息。 在消息标头中插入数据集ID，以便将该消息直接摄取到其中。

您可以使用获取现有数据集的ID [!DNL Platform] UI或使用API中的列表操作。 数据集ID可在上找到 [Experience Platform](https://platform.adobe.com) 通过转到 **[!UICONTROL 数据集]** 选项卡，单击要为其创建ID的数据集，然后从 **[!UICONTROL 信息]** 选项卡。 请参阅 [目录服务概述](../../catalog/home.md) 有关如何使用API检索数据集的信息。

您可以创建新数据集，而不是使用现有数据集。 请阅读 [使用API创建数据集](../../catalog/api/create-dataset.md) 有关使用API创建数据集的更多信息，请参阅教程。

**API格式**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 已创建的流连接的ID。 |

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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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

成功的响应返回HTTP状态207（多状态）。 查看响应正文提供了有关在请求中执行的每种方法成功或失败的更多详细信息。 将为请求消息数组的每个元素返回响应。 以下是成功响应且无消息失败的示例：

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

有关状态代码的更多信息，请参阅 [响应代码](#response-codes) 表。

## 识别失败消息

与通过单个消息发送请求相比，在发送包含多个消息的HTTP请求时，还需要考虑其他因素，例如：如何识别数据何时无法发送、哪些特定消息无法发送以及如何检索这些消息，以及当同一请求中的其他消息失败时，成功的数据会发生什么情况。

在继续本教程之前，建议先查看 [检索失败的批次](../quality/retrieve-failed-batches.md) 指南。

### 发送包含有效消息和无效消息的请求有效负载

以下示例显示了当批次包含有效消息和无效消息时发生的情况。

请求有效负载是表示XDM架构中事件的JSON对象数组。 请注意，要成功验证报文，需要满足以下条件：
- 此 `imsOrgId` 消息标头中的字段必须与入口定义匹配。 如果请求有效负载不包含 `imsOrgId` 字段， [!DNL Data Collection Core Service] (DCCS)将自动添加字段。
- 消息的标头应引用在中创建的现有XDM架构 [!DNL Platform] UI。
- 此 `datasetId` 字段需要引用中的现有数据集 [!DNL Platform]，其架构需要与 `header` 请求正文中包含的每个消息中的对象。

**API格式**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 已创建的数据入口的ID。 |

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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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

响应有效负载包含每条消息的状态以及 `xactionId` 可用于跟踪。

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
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        }
    ]
}
```

上面的示例响应显示了上一个请求的错误消息。 通过将此响应与先前的有效响应进行比较，您可以发现请求导致部分成功，其中一条消息摄取成功，三条消息导致失败。 请注意，这两个响应都返回“207”状态代码。 有关状态代码的更多信息，请参阅 [响应代码](#response-codes) 表。

第一条　消息已成功发送至 [!DNL Platform] 并且不受其他消息结果的影响。 因此，在尝试重新发送失败的消息时，您无需重新包含此消息。

第二个消息失败，因为它缺少消息正文。 集合请求要求消息元素具有有效的标头和正文部分。 在第二条消息的标头之后添加以下代码将修复请求，从而允许第二条消息通过验证：

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

第三个消息失败，因为标头中使用了无效的组织ID。 组织必须与您尝试发布到的{CONNECTION_ID}匹配。 要确定哪个组织ID与您使用的流连接匹配，您可以执行 `GET inlet` 使用 [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/). 参见 [检索流连接](./create-streaming-connection.md#get-data-collection-url) 有关如何检索之前创建的流连接的示例。

第四条　消息失败，因为它未遵循预期的XDM架构。 此 `xdmSchema` 请求的标头和正文中包含的与的XDM架构不匹配 `{DATASET_ID}`. 更正消息标头和正文中的架构后，可以使其通过DCCS验证并成功发送到 [!DNL Platform]. 还必须更新消息正文以匹配的XDM架构 `{DATASET_ID}` 以通过流验证 [!DNL Platform]. 有关成功流式传输到Platform的消息有何影响的更多信息，请参阅 [确认消息已摄取](#confirm-messages-ingested) 部分。

### 从检索失败的邮件 [!DNL Platform]

失败的消息由响应数组中的错误状态代码标识。
无效消息将被收集并存储在指定的数据集中的“错误”批次 `{DATASET_ID}`.

阅读 [检索失败的批次](../quality/retrieve-failed-batches.md) 指南，以了解有关恢复失败的批处理消息的详细信息。

## 确认消息已摄取

通过DCCS验证的消息将流式传输到 [!DNL Platform]. 日期 [!DNL Platform]，批量消息在被摄取到之前通过流验证进行测试 [!DNL Data Lake]. 批次的状态（无论是否成功）将显示在由指定的数据集内 `{DATASET_ID}`.

您可以查看成功作为流接收方的批处理消息的状态 [!DNL Platform] 使用 [EXPERIENCE PLATFORMUI](https://platform.adobe.com) 通过转到 **[!UICONTROL 数据集]** 选项卡，单击要流式传输到的数据集，然后检查 **[!UICONTROL 数据集活动]** 选项卡。

通过流验证的批量消息 [!DNL Platform] 被摄取到 [!DNL Data Lake]. 然后，即可分析或导出消息。

## 后续步骤

现在您知道如何在单个请求中发送多条消息并验证何时将消息成功引入到目标数据集中，接下来您可以开始将自己的数据流式传输到 [!DNL Platform]. 有关如何从查询和检索提取的数据的概述 [!DNL Platform]，请参见 [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) 指南。

## 附录

本节包含本教程的补充信息。

### 响应代码

下表显示了成功和失败响应消息返回的状态代码。

| 状态代码 | 描述 |
| :---: | --- |
| 207 | 尽管使用“207”作为整体响应状态代码，但收件人需要查阅多状态响应主体的内容，以获得有关方法执行成功或失败的更多信息。 响应代码在成功、部分成功以及失败情况下使用。 |
| 400 | 请求有问题。 有关更具体的错误消息，请参阅响应正文（例如，消息有效负载缺少必填字段，或消息的xdm格式未知）。 |
| 401 | 未授权：请求缺少有效的授权标头。 仅对启用身份验证的Inlet返回此值。 |
| 403 | 未授权：提供的授权令牌无效或已过期。 仅对启用身份验证的Inlet返回此值。 |
| 413 | 有效负载太大 — 当总有效负载请求大于1MB时引发。 |
| 429 | 指定持续时间内的请求过多。 |
| 500 | 处理有效负载时出错。 有关更具体的错误消息，请参阅响应正文(例如，未指定消息有效负载架构，或者与中的XDM定义不匹配 [!DNL Platform])。 |
| 503 | 服务当前不可用。 客户端应使用指数回退策略至少重试3次。 |
