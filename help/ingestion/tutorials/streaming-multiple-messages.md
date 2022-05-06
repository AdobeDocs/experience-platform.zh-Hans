---
keywords: Experience Platform；主页；热门主题；流式引入；摄取；流式传送多条消息；多条消息；
solution: Experience Platform
title: 在一个HTTP请求中发送多条消息
topic-legacy: tutorial
type: Tutorial
description: 本文档提供了一个教程，用于使用流摄取在单个HTTP请求内向Adobe Experience Platform发送多条消息。
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---

# 在一个HTTP请求中发送多条消息

在将数据流式传输到Adobe Experience Platform时，进行大量HTTP调用可能会非常昂贵。 例如，创建1个HTTP请求（每个消息200 KB），单个负载200 KB，而不是创建200个负载为1 KB的HTTP请求，这样会更加有效。 正确使用时，在单个请求内对多个消息进行分组是优化发送到的数据的绝佳方法 [!DNL Experience Platform].

本文档提供了将多条消息发送到的教程 [!DNL Experience Platform] 流摄取在单个HTTP请求中。

## 快速入门

本教程需要对Adobe Experience Platform有一定的了解 [!DNL Data Ingestion]. 在开始使用本教程之前，请查阅以下文档：

- [数据摄取概述](../home.md):涵盖 [!DNL Experience Platform Data Ingestion]，包括摄取方法和Data Connectors。
- [流摄取概述](../streaming-ingestion/overview.md):流摄取的工作流和构建基块，例如流连接、数据集、 [!DNL XDM Individual Profile]和 [!DNL XDM ExperienceEvent].

本教程还要求您完成 [验证到Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) 教程以成功调用 [!DNL Platform] API。 完成身份验证教程将为本教程中所有API调用所需的授权标头提供值。 标头显示在示例调用中，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`

所有POST请求都需要一个额外的标头：

- Content-Type:application/json

## 创建流连接

必须先创建流连接，然后才能开始将数据流式传输到 [!DNL Experience Platform]. 阅读 [创建流连接](./create-streaming-connection.md) 指南，了解如何创建流连接。

注册流连接后，作为数据生成者，您将拥有一个唯一的URL，可用于将数据流式传输到Platform。

## 流到数据集

以下示例显示如何在单个HTTP请求内向特定数据集发送多条消息。 在消息标题中插入数据集ID，以直接将该消息摄取到该数据集中。

您可以使用 [!DNL Platform] UI或在API中使用列表操作。 数据集ID可在 [Experience Platform](https://platform.adobe.com) 通过 **[!UICONTROL 数据集]** 选项卡上，单击所需ID的数据集，然后从 **[!UICONTROL 信息]** 选项卡。 请参阅 [目录服务概述](../../catalog/home.md) 有关如何使用API检索数据集的信息。

您可以创建新数据集，而不是使用现有数据集。 请阅读 [使用API创建数据集](../../catalog/api/create-dataset.md) 教程，以了解有关使用API创建数据集的更多信息。

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

成功响应会返回HTTP状态207（多状态）。 查看响应正文可提供有关请求中执行的每个方法是否成功的更多详细信息。 为请求消息数组的每个元素返回响应。 以下是无消息失败的成功响应示例：

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

有关状态代码的详细信息，请参阅 [响应代码](#response-codes) 表。

## 识别失败的消息

与使用单条消息发送请求相比，在发送包含多条消息的HTTP请求时，需要考虑其他因素，例如：如何识别数据何时发送失败、哪些特定消息未能发送以及如何检索这些消息，以及当同一请求中的其他消息失败时成功的数据会发生什么情况。

在继续本教程之前，建议先查看 [检索失败批次](../quality/retrieve-failed-batches.md) 的双曲余切值。

### 发送包含有效消息和无效消息的请求负载

以下示例显示了当批处理包含有效和无效消息时会发生什么情况。

请求有效负载是一个JSON对象数组，表示XDM架构中的事件。 请注意，成功验证消息需要满足以下条件：
- 的 `imsOrgId` 字段必须匹配入口定义。 如果请求有效负载不包括 `imsOrgId` 字段， [!DNL Data Collection Core Service] (DCCS)将自动添加该字段。
- 消息的标头应引用在 [!DNL Platform] UI。
- 的 `datasetId` 字段需要引用 [!DNL Platform]，且其架构需要与 `header` 请求正文中包含的每个消息中的对象。

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

响应负载包括每个消息的状态以及 `xactionId` 可用于跟踪。

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

上面的示例响应显示了上一个请求的错误消息。 通过将此响应与先前的有效响应进行比较，您可以发现请求会部分成功，成功摄取一条消息，并导致失败三条消息。 请注意，两个响应都会返回“207”状态代码。 有关状态代码的详细信息，请参阅 [响应代码](#response-codes) 表。

第一条消息已成功发送到 [!DNL Platform] 和不受其他消息结果的影响。 因此，在尝试重新发送失败的消息时，您无需重新包含此消息。

第二条消息失败，因为它缺少消息正文。 收集请求要求消息元素具有有效的标题和正文部分。 在第二条消息的标头之后添加以下代码将修复请求，从而允许第二条消息通过验证：

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

第三条消息失败，原因是标头中使用的IMS组织ID无效。 IMS组织必须与您尝试发布到的{CONNECTION_ID}匹配。 要确定哪个IMS组织ID与您使用的流连接相匹配，您可以执行 `GET inlet` 使用 [[!DNL Data Ingestion API]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). 请参阅 [检索流连接](./create-streaming-connection.md#get-data-collection-url) 有关如何检索之前创建的流连接的示例。

第四条消息失败，因为它未遵循预期的XDM架构。 的 `xdmSchema` 请求的标头和正文中包含的XDM架构与 `{DATASET_ID}`. 更正消息标头和正文中的架构后，该架构可通过DCCS验证并成功发送至 [!DNL Platform]. 还必须更新消息正文，以匹配 `{DATASET_ID}` 通过流式验证 [!DNL Platform]. 有关成功流入平台的消息会发生什么情况的更多信息，请参阅 [确认消息已摄取](#confirm-messages-ingested) 部分。

### 从检索失败的消息 [!DNL Platform]

失败的消息由响应数组中的错误状态代码标识。
无效消息会收集并存储在指定的数据集内的“error”批次中 `{DATASET_ID}`.

阅读 [检索失败批次](../quality/retrieve-failed-batches.md) 有关恢复失败批量消息的详细信息。

## 确认摄取的消息

通过DCCS验证的消息会被流式传输到 [!DNL Platform]. 开 [!DNL Platform]，则批量消息在摄取到 [!DNL Data Lake]. 批次的状态（无论是否成功）都会显示在指定的数据集中 `{DATASET_ID}`.

您可以查看成功流入的批量消息的状态 [!DNL Platform] 使用 [Experience PlatformUI](https://platform.adobe.com) 通过 **[!UICONTROL 数据集]** 选项卡上，单击要流式处理到的数据集，然后检查 **[!UICONTROL 数据集活动]** 选项卡。

通过流验证的批量消息 [!DNL Platform] 被摄取到 [!DNL Data Lake]. 然后，即可分析或导出这些消息。

## 后续步骤

现在，您已了解如何在单个请求中发送多条消息，并验证消息何时被成功摄取到目标数据集，接下来可以开始将您自己的数据流式传输到 [!DNL Platform]. 有关如何从中查询和检索摄取数据的概述 [!DNL Platform]，请参阅 [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) 的双曲余切值。

## 附录

本节包含教程的补充信息。

### 响应代码

下表显示了成功和失败响应消息返回的状态代码。

| 状态代码 | 描述 |
| :---: | --- |
| 207 | 尽管将“207”用作整体响应状态代码，但接收者需要查阅多状态响应主体的内容，以进一步了解有关方法执行的成功或失败的信息。 响应代码用于成功、部分成功以及失败情况。 |
| 400 | 请求有问题。 有关更具体的错误消息，请参阅响应正文（例如，消息有效负荷缺少必填字段，或消息为未知xdm格式）。 |
| 401 | 未授权：请求缺少有效的授权标头。 仅对启用了身份验证的入口返回此值。 |
| 403 | 未授权：提供的授权令牌无效或已过期。 仅对启用了身份验证的入口返回此值。 |
| 413 | 负载过大 — 当负载请求总负载大于1MB时引发。 |
| 429 | 指定时间段内的请求过多。 |
| 500 | 处理负载时出错。 有关更具体的错误消息(例如，未指定消息有效负载架构，或与 [!DNL Platform])。 |
| 503 | 服务当前不可用。 客户端应使用指数回退策略至少重试3次。 |
