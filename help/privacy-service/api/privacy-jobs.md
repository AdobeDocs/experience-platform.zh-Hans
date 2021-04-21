---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 隐私作业API端点
topic-legacy: developer guide
description: 了解如何使用Experience Cloud API管理Privacy Service应用程序的隐私作业。
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 1%

---

# 隐私作业端点

本文档介绍如何使用API调用处理隐私作业。 具体而言，它涵盖在[!DNL Privacy Service] API中使用`/job`端点。 在阅读本指南之前，请参阅[快速入门部分](./getting-started.md#getting-started)以了解成功调用API所需的重要信息，包括必需的标头以及如何读取示例API调用。

>[!NOTE]
>
>如果您试图管理客户的同意或退出请求，请参阅[同意端点指南](./consent.md)。

## 列表所有作业{#list}

您可以通过向`/jobs`端点发出GET请求，视图组织内所有可用隐私作业的列表。

**API格式**

此请求格式在`/jobs`端点上使用`regulation`查询参数，因此它以问号(`?`)开头，如下所示。 该响应将分页，允许您使用其他查询参数（`page`和`size`）来筛选响应。 可以使用&amp;符(`&`)分隔多个参数。

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 参数 | 描述 |
| --- | --- |
| `{REGULATION}` | 要查询的调节类型。 接受的值包括： <ul><li>`gdpr` (欧洲合并)</li><li>`ccpa` （加利福尼亚）</li><li>`lgpd_bra` （巴西）</li><li>`nzpa_nzl` （新西兰）</li><li>`pdpa_tha` （泰国）</li></ul> |
| `{PAGE}` | 要显示的数据页，使用基于0的编号。 默认值为 `0`。 |
| `{SIZE}` | 每个页面上要显示的结果数。 默认值为`1`，最大值为`100`。 超过最大值会导致API返回400代码错误。 |

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

成功的响应会返回一列表作业，每个作业都包含详细信息，如`jobId`。 在此示例中，响应将包含50个作业的列表，从结果的第三页开始。

### 访问后续页面

要在分页响应中获取下一组结果，您必须对同一端点进行另一个API调用，同时将`page`查询参数增加1。

## 创建隐私作业{#create-job}

在创建新作业请求之前，您必须首先收集有关要访问、删除或销售其数据的数据主体选择退出的标识信息。 获得所需数据后，必须在POST请求到`/jobs`端点的负载中提供该数据。

>[!NOTE]
>
>兼容的Adobe Experience Cloud应用程序使用不同的值来标识数据主体。 有关应用程序所需标识符的详细信息，请参阅[Privacy Service和Experience Cloud应用程序](../experience-cloud-apps.md)指南。 有关确定要发送到[!DNL Privacy Service]的ID的更一般指导，请参阅有关隐私请求](../identity-data.md)中[标识数据的文档。

[!DNL Privacy Service] API支持两种类型的个人数据作业请求：

* [访问和/或删除](#access-delete):访问（读取）或删除个人数据。
* [选择退出销售](#opt-out):将个人数据标记为不出售。

>[!IMPORTANT]
>
>虽然访问和删除请求可以合并为单个API调用，但是必须单独发出退出请求。

### 创建访问/删除作业{#access-delete}

本节说明如何使用API发出访问/删除作业请求。

**API格式**

```http
POST /jobs
```

**请求**

以下请求将创建新作业请求，该请求由有效负荷中提供的属性进行配置，如下所述。

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
| `companyContexts` **（必需）** | 包含组织的身份验证信息的数组。 列出的每个标识符都包含以下属性： <ul><li>`namespace`:标识符的命名空间。</li><li>`value`:标识符的值。</li></ul>其中一个标识符使用`imsOrgId`作为其`namespace`的&#x200B;**必需**，其`value`包含IMS组织的唯一ID。 <br/><br/>其他标识符可以是特定于产品的公司限定符(例如 `Campaign`)，它标识与属于您组织的Adobe应用程序的集成。潜在值包括帐户名、客户端代码、租户ID或其他应用程序标识符。 |
| `users` **（必需）** | 包含至少一个用户集合的数组，您希望访问或删除其信息。 单个请求中最多可提供1000个用户ID。 每个用户对象都包含以下信息： <ul><li>`key`:用户的标识符，用于限定响应数据中的单独作业ID。最好为此值选择一个唯一、易于识别的字符串，以便稍后可以轻松引用或查找它。</li><li>`action`:一个数组，列表对用户数据执行所需操作。根据要执行的操作，此数组必须包括`access`、`delete`或两者。</li><li>`userIDs`:用户的身份集合。单个用户可以拥有的身份数量限制为9个。 每个标识都由`namespace`、`value`和命名空间限定符(`type`)组成。 有关这些必需属性的详细信息，请参阅[附录](appendix.md)。</li></ul> 有关`users`和`userIDs`的更详细说明，请参阅[疑难解答指南](../troubleshooting-guide.md#user-ids)。 |
| `include` **（必需）** | 要包含在您的处理中的Adobe产品阵列。 如果此值缺失或为空，则请求将被拒绝。 仅包括您的组织与之集成的产品。 有关详细信息，请参阅附录中关于[已接受产品值](appendix.md)的部分。 |
| `expandIDs` | 一个可选属性，当设置为`true`时，它表示处理应用程序中ID的优化（当前仅受[!DNL Analytics]支持）。 如果省略，则此值默认为`false`。 |
| `priority` | Adobe Analytics使用的可选属性，用于设置处理请求的优先级。 接受的值为`normal`和`low`。 如果省略`priority`，则默认行为为`normal`。 |
| `analyticsDeleteMethod` | 一个可选属性，它指定Adobe Analytics如何处理个人数据。 此属性接受两个可能的值： <ul><li>`anonymize`:给定用户ID集合引用的所有数据均为匿名数据。如果省略`analyticsDeleteMethod`，则这是默认行为。</li><li>`purge`:所有数据都被完全删除。</li></ul> |
| `regulation` **（必需）** | 隐私工作的规定。 接受以下值： <ul><li>`gdpr` (欧洲合并)</li><li>`ccpa` （加利福尼亚）</li><li>`lgpd_bra` （巴西）</li><li>`nzpa_nzl` （新西兰）</li><li>`pdpa_tha` （泰国）</li></ul> |

**响应**

成功的响应会返回新创建作业的详细信息。

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
| `jobId` | 作业的只读、唯一的系统生成的ID。 该值用于查找特定作业的下一步。 |

成功提交作业请求后，可以继续执行下一步[检查作业状态](#check-status)。

## 检查作业{#check-status}的状态

通过将特定作业的`jobId`包含在到`/jobs`端点的GET请求路径中，可以检索有关该作业的信息，如其当前处理状态。

>[!IMPORTANT]
>
>之前创建的作业的数据仅可在作业完成日期后30天内进行检索。

**API格式**

```http
GET /jobs/{JOB_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{JOB_ID}` | 要查找的作业的ID。 在[成功创建作业](#create-job)和[列出所有作业](#list)的API响应下返回此ID。`jobId` |

**请求**

以下请求将检索其`jobId`在请求路径中提供的作业的详细信息。

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
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
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
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| 属性 | 描述 |
| --- | --- |
| `productStatusResponse` | `productResponses`数组中的每个对象都包含有关特定[!DNL Experience Cloud]应用程序的作业当前状态的信息。 |
| `productStatusResponse.status` | 作业的当前状态类别。 有关[可用状态类别](#status-categories)的列表及其相应含义，请参阅下表。 |
| `productStatusResponse.message` | 与状态类别对应的作业的特定状态。 |
| `productStatusResponse.responseMsgCode` | 由[!DNL Privacy Service]接收的产品响应消息的标准代码。 消息详细信息在`responseMsgDetail`下提供。 |
| `productStatusResponse.responseMsgDetail` | 对工作状态的更详细说明。 处于类似状态的消息可能因产品而异。 |
| `productStatusResponse.results` | 对于某些状态，某些产品可能会返回一个`results`对象，该对象提供`responseMsgDetail`未涵盖的其他信息。 |
| `downloadURL` | 如果作业的状态为`complete`，则此属性提供URL以将作业结果作为ZIP文件下载。 作业完成后60天内可下载此文件。 |

### 作业状态类别{#status-categories}

下表列表了不同的可能作业状态类别及其相应含义：

| 状态类别 | 意义 |
| -------------- | -------- |
| `complete` | 作业已完成，并且（如果需要）文件会从每个应用程序上载。 |
| `processing` | 应用程序已确认该作业，并且当前正在处理。 |
| `submitted` | 作业会提交到每个适用的应用程序。 |
| `error` | 在处理作业时发生故障 — 通过检索单个作业详细信息可以获得更具体的信息。 |

>[!NOTE]
>
>如果提交的作业具有仍在处理的从属子作业，则该作业可能仍处于`processing`状态。

## 后续步骤

您现在知道如何使用[!DNL Privacy Service] API创建和监视隐私作业。 有关如何使用用户界面执行相同任务的信息，请参阅[Privacy ServiceUI概述](../ui/overview.md)。
