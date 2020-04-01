---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 作业
topic: developer guide
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 隐私工作

以下各节将介绍您可以使用Privacy Service API中的根端点(`/`)进行的调用。 每个调用包括常规API格式、显示所需标题的示例请求和示例响应。

## 创建隐私工作

在创建新作业请求之前，您必须首先收集有关要访问、删除或销售其数据的数据主体的选择退出标识信息。 获得所需数据后，必须在发往根端点的POST请求的有效负荷中提供该数据。

>[!NOTE] 兼容的Adobe Experience Cloud应用程序使用不同的值来识别数据主体。 有关您的应用程 [序所需标识符的更多信息](../experience-cloud-apps.md) ，请参阅隐私服务和Experience Cloud应用程序指南。

隐私服务API支持两种类型的个人数据作业请求：

* [访问和／或删除](#access-delete):访问（读取）或删除个人数据。
* [选择退出出售](#opt-out):将个人数据标记为不出售。

>[!IMPORTANT] 虽然访问和删除请求可以合并为单个API调用，但是必须单独发出退出请求。

### 创建访问／删除作业 {#access-delete}

本节演示如何使用API发出访问／删除作业请求。

**API格式**

```http
POST /
```

**请求**

以下请求将创建新的作业请求，该请求由有效负荷中提供的属性进行配置，如下所述。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| 属性 | 描述 |
| --- | --- |
| `companyContexts` **（必需）** | 包含单位身份验证信息的数组。 列出的每个标识符都包括以下属性： <ul><li>`namespace`:标识符的命名空间。</li><li>`value`:标识符的值。</li></ul>必须 **使用** ，其中一个标识符 `imsOrgId` 作为其 `namespace`名称，并包含 `value` IMS组织的唯一ID。 <br/><br/>其他标识符可以是特定于产品的公司限定符(例如， `Campaign`)，用于标识与属于您组织的Adobe应用程序的集成。 潜在值包括帐户名、客户端代码、租户ID或其他应用程序标识符。 |
| `users` **（必需）** | 一个数组，其中包含至少一个用户的集合，您希望访问或删除其信息。 在单个请求中最多可提供1000个用户ID。 每个用户对象都包含以下信息： <ul><li>`key`:用于限定响应数据中的单独作业ID的标识符。 为此值选择唯一、易于识别的字符串是最佳做法，这样便可轻松引用或稍后查找。</li><li>`action`:一个数组，它列表对数据执行所需的操作。 根据您要执行的操作，此数组必须包括、 `access`或 `delete`两者。</li><li>`userIDs`:特定用户的身份集合。 单个用户可以拥有的身份数量限制为9个。 每个标识都包 `namespace`含一个、 `value`一个和一个命名空间限定符(`type`)。 有关这些 [必需属性的更多详细信息](appendix.md) ，请参阅附录。</li></ul> |
| `include` **（必需）** | 要包含在您的处理中的一系列Adobe产品。 如果此值缺失或为空，则请求将被拒绝。 仅包括您的组织与之集成的产品。 有关详细信息，请 [参阅附录中](appendix.md) “已接受的产品值”一节。 |
| `expandIDs` | 一个可选属性，当设置为 `true`时，它表示处理应用程序中ID的优化（目前仅受Analytics支持）。 If omitted, this value defaults to `false`. |
| `priority` | Adobe Analytics使用的可选属性，用于设置处理请求的优先级。 接受的值 `normal` 是和 `low`。 如果 `priority` 忽略，则默认行为为 `normal`。 |
| `analyticsDeleteMethod` | 一个可选属性，它指定Adobe Analytics如何处理个人数据。 此属性接受两个可能的值： <ul><li>`anonymize`:给定的用户ID集合引用的所有数据均设为匿名。 如果 `analyticsDeleteMethod` 忽略，则这是默认行为。</li><li>`purge`:所有数据都被完全删除。</li></ul> |
| `regulation` **（必需）** | 请求的规定（必须为“gdpr”或“ccpa”）。 |

**响应**

成功的响应会返回新创建的作业的详细信息。

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| 属性 | 描述 |
| --- | --- |
| `jobId` | 作业的只读、唯一的系统生成ID。 该值用于查找特定作业的下一步。 |

成功提交作业请求后，您可以继续执行检查作 [业状态的下一步](#check-the-status-of-a-job)。

### 创建选择退出销售的作业 {#opt-out}

本节演示了如何使用API发出选择退出销售作业请求。

**API格式**

```http
POST /
```

**请求**

以下请求将创建新的作业请求，该请求由有效负荷中提供的属性进行配置，如下所述。

```shell
curl -X POST \
  https://platform.adobe.io/data/privacy/gdpr/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| 属性 | 描述 |
| --- | --- |
| `companyContexts` **（必需）** | 包含单位身份验证信息的数组。 列出的每个标识符都包括以下属性： <ul><li>`namespace`:标识符的命名空间。</li><li>`value`:标识符的值。</li></ul>必须 **使用** ，其中一个标识符 `imsOrgId` 作为其 `namespace`名称，并包含 `value` IMS组织的唯一ID。 <br/><br/>其他标识符可以是特定于产品的公司限定符(例如， `Campaign`)，用于标识与属于您组织的Adobe应用程序的集成。 潜在值包括帐户名、客户端代码、租户ID或其他应用程序标识符。 |
| `users` **（必需）** | 一个数组，其中包含至少一个用户的集合，您希望访问或删除其信息。 在单个请求中最多可提供1000个用户ID。 每个用户对象都包含以下信息： <ul><li>`key`:用于限定响应数据中的单独作业ID的标识符。 为此值选择唯一、易于识别的字符串是最佳做法，这样便可轻松引用或稍后查找。</li><li>`action`:一个数组，它列表对数据执行所需的操作。 对于选择退出销售请求，阵列必须仅包含该值 `opt-out-of-sale`。</li><li>`userIDs`:特定用户的身份集合。 单个用户可以拥有的身份数量限制为9个。 每个标识都包 `namespace`含一个、 `value`一个和一个命名空间限定符(`type`)。 有关这些 [必需属性的更多详细信息](appendix.md) ，请参阅附录。</li></ul> |
| `include` **（必需）** | 要包含在您的处理中的一系列Adobe产品。 如果此值缺失或为空，则请求将被拒绝。 仅包括您的组织与之集成的产品。 有关详细信息，请 [参阅附录中](appendix.md) “已接受的产品值”一节。 |
| `expandIDs` | 一个可选属性，当设置为 `true`时，它表示处理应用程序中ID的优化（目前仅受Analytics支持）。 If omitted, this value defaults to `false`. |
| `priority` | Adobe Analytics使用的可选属性，用于设置处理请求的优先级。 接受的值 `normal` 是和 `low`。 如果 `priority` 忽略，则默认行为为 `normal`。 |
| `analyticsDeleteMethod` | 一个可选属性，它指定Adobe Analytics如何处理个人数据。 此属性接受两个可能的值： <ul><li>`anonymize`:给定的用户ID集合引用的所有数据均设为匿名。 如果 `analyticsDeleteMethod` 忽略，则这是默认行为。</li><li>`purge`:所有数据都被完全删除。</li></ul> |
| `regulation` **（必需）** | 请求的规定（必须为“gdpr”或“ccpa”）。 |

**响应**

成功的响应会返回新创建的作业的详细信息。

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd9vjs0",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bes0ewj2",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 2
}
```

| 属性 | 描述 |
| --- | --- |
| `jobId` | 作业的只读、唯一的系统生成ID。 此值用于在下一步中查找特定作业。 |

成功提交作业请求后，您可以继续执行检查作业状态的下一步。

## 检查作业的状态

使用上一步 `jobId` 中返回的值之一，您可以检索有关该作业的信息，如其当前处理状态。

>[!IMPORTANT] 之前创建的作业的数据仅可在作业完成日期后的30天内进行检索。

**API格式**

```http
GET /{JOB_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{JOB_ID}` | 要查找的作业的ID，在上一步 `jobId` 的响应下返 [回](#create-a-job-request)。 |

**请求**

以下请求将检索请求路径中提供的 `jobId` 作业的详细信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**响应**

成功的响应会返回指定作业的详细信息。

```json
{
    "jobId": "527ef92d-6cd9-45cc-9bf1-477cfa1e2ca2",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "error",
    "submittedBy": "02b38adf-6573-401e-b4cc-6b08dbc0e61c@techacct.adobe.com",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "submitted",
                "message": "processing"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "submitted",
                "message": "processing"
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| 属性 | 描述 |
| --- | --- |
| `productStatusResponse` | 作业的当前状态。 下表提供了有关每种可能状态的详细信息。 |
| `downloadURL` | 如果作业的状态为，则此属 `complete`性会提供一个URL，以ZIP文件形式下载作业结果。 此文件在作业完成后60天内可供下载。 |

### 作业状态响应

下表列表了不同的可能作业状态及其相应的含义：

| 状态代码 | 状态消息 | 意义 |
| ----------- | -------------- | -------- |
| 1 | 完成 | 作业已完成，并且（如果需要）文件从每个应用程序上传。 |
| 2 | 处理时间 | 应用程序已确认作业，并且当前正在处理。 |
| 3 | 已提交 | 作业会提交到每个适用的应用程序。 |
| 4 | 错误 | 处理作业时失败的内容——通过检索单个作业详细信息可以获得更具体的信息。 |

>[!NOTE] 如果提交的作业具有仍在处理的从属子作业，则该作业可能仍处于处理状态。

## 列表所有作业

您可以通过向根()端点发出GET请求，视图组织内所有可用作业请求的`/`列表。

**API格式**

此请求格式在根( `regulation``/`)端点上使用查询参数，因此它以问号(`?`)开头，如下所示。 响应会分页，这样您便可以使用其他查询参数(`page` 和 `size`)筛选响应。 您可以使用&amp;符号()分隔多个`&`参数。

```http
GET ?regulation={REGULATION}
GET ?regulation={REGULATION}&page={PAGE}
GET ?regulation={REGULATION}&size={SIZE}
GET ?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 参数 | 描述 |
| --- | --- |
| `{REGULATION}` | 要查询的调节类型。 接受的值 `gdpr` 是和 `ccpa`。 |
| `{PAGE}` | 要显示的数据页，使用基于0的编号。 默认值为 `0`。 |
| `{SIZE}` | 每页上显示的结果数。 默认值为， `1` 最大值为 `100`。 超过最大值将导致API返回400代码错误。 |

**请求**

以下请求从页面大小为50的第三页开始检索IMS组织内所有作业的分页列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**响应**

成功的响应会返回一列表作业，每个作业都包含详细信息（如其） `jobId`。 在此示例中，响应将包含50个作业的列表，从结果的第三页开始。

### 访问后续页面

要在分页响应中获取下一组结果，您必须对同一端点进行另一个API调用，同时将 `page` 查询参数增加1。

## 后续步骤

您现在了解如何使用隐私服务API创建和监控隐私作业。 有关如何使用用户界面执行相同任务的信息，请参阅隐 [私服务UI概述](../ui/overview.md)。
