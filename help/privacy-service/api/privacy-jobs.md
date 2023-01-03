---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 隐私作业API端点
topic-legacy: developer guide
description: 了解如何使用Experience CloudAPI管理Privacy Service应用程序的隐私作业。
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 2%

---

# 隐私作业端点

本文档介绍如何使用API调用处理隐私作业。 具体而言，它涵盖 `/job` 的端点 [!DNL Privacy Service] API。 在阅读本指南之前，请参阅 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括所需的标头以及如何读取示例API调用。

>[!NOTE]
>
>如果您尝试管理客户的同意或选择退出请求，请参阅 [consent endpoint指南](./consent.md).

## 列出所有作业 {#list}

您可以通过向 `/jobs` 端点。

**API格式**

此请求格式使用 `regulation` 查询参数 `/jobs` 端点，因此以问号(`?`)，如下所示。 响应将分页，以便您使用其他查询参数(`page` 和 `size`)来筛选响应。 您可以使用与号(`&`)。

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 参数 | 描述 |
| --- | --- |
| `{REGULATION}` | 要查询的规则类型。 接受的值包括： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>请参阅 [受支持法规](../regulations/overview.md) 有关上述值代表的隐私法规的更多信息。 |
| `{PAGE}` | 要显示的数据页面，使用基于0的编号。 默认值为 `0`。 |
| `{SIZE}` | 要在每个页面上显示的结果数。 默认值为 `1` 最大值是 `100`. 超过最大值会导致API返回400代码错误。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求从页面大小为50的第三个页面开始，检索IMS组织内所有作业的分页列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的响应会返回作业列表，每个作业都包含其 `jobId`. 在此示例中，响应将包含从结果第三页开始的50个作业列表。

### 访问后续页面

要在分页响应中获取下一组结果，您必须对同一端点再进行一次API调用，同时将 `page` 按1查询参数。

## 创建隐私作业 {#create-job}

在创建新作业请求之前，您必须首先收集有关要访问、删除或选择退出销售其数据的数据主体的标识信息。 获得所需数据后，必须在向发送的POST请求的有效负载中提供该数据 `/jobs` 端点。

>[!NOTE]
>
>兼容的Adobe Experience Cloud应用程序使用不同的值来识别数据主体。 请参阅 [Privacy Service和Experience Cloud应用程序](../experience-cloud-apps.md) 有关应用程序所需标识符的更多信息。 有关确定要发送到的ID的更一般指导 [!DNL Privacy Service]，请参阅 [隐私请求中的身份数据](../identity-data.md).

的 [!DNL Privacy Service] API支持两种类型的个人数据作业请求：

* [访问和/或删除](#access-delete):访问（读取）或删除个人数据。
* [选择退出销售](#opt-out):将个人数据标记为不出售。

>[!IMPORTANT]
>
>虽然访问和删除请求可以合并为单个API调用，但是必须单独发出选择退出请求。

### 创建访问/删除作业 {#access-delete}

本节演示如何使用API发出访问/删除作业请求。

**API格式**

```http
POST /jobs
```

**请求**

以下请求会创建一个新的作业请求，该请求由有效负载中提供的属性进行配置，如下所述。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| 属性 | 描述 |
| --- | --- |
| `companyContexts` **（必需）** | 包含贵组织的身份验证信息的数组。 列出的每个标识符都包含以下属性： <ul><li>`namespace`:标识符的命名空间。</li><li>`value`:标识符的值。</li></ul>是 **必需** 标识符之一使用 `imsOrgId` as `namespace`, `value` 包含IMS组织的唯一ID。 <br/><br/>其他标识符可以是特定于产品的公司限定符(例如， `Campaign`)，用于识别与属于贵组织的Adobe应用程序的集成。 潜在值包括帐户名称、客户端代码、租户ID或其他应用程序标识符。 |
| `users` **（必需）** | 一个数组，其中包含至少一个用户的集合，您要访问或删除其信息。 在单个请求中最多可以提供1000个用户ID。 每个用户对象包含以下信息： <ul><li>`key`:用户的标识符，用于限定响应数据中单独的作业ID。 最好为此值选择一个唯一且易于识别的字符串，以便以后可以轻松引用或查找该字符串。</li><li>`action`:一个数组，其中列出了对用户数据执行的所需操作。 根据您要执行的操作，此数组必须包括 `access`, `delete`，或两者兼有。</li><li>`userIDs`:用户的标识集合。 单个用户可以拥有的身份数量最多为9个。 每个标识都包含 `namespace`, a `value`，和命名空间限定符(`type`)。 请参阅 [附录](appendix.md) 以了解有关这些必需属性的更多详细信息。</li></ul> 更详细的说明 `users` 和 `userIDs`，请参阅 [疑难解答指南](../troubleshooting-guide.md#user-ids). |
| `include` **（必需）** | 要包含在处理中的Adobe产品数组。 如果此值缺失或为空，则请求将被拒绝。 仅包括贵组织与集成的产品。 请参阅 [接受的产品值](appendix.md) ，以了解详细信息。 |
| `expandIDs` | 可选属性，当设置为 `true`，表示针对处理应用程序中的ID而进行的优化(当前仅受 [!DNL Analytics])。 如果忽略，则此值默认为 `false`. |
| `priority` | Adobe Analytics使用的可选属性，用于设置处理请求的优先级。 接受的值为 `normal` 和 `low`. 如果 `priority` ，则默认行为为 `normal`. |
| `analyticsDeleteMethod` | 一个可选属性，用于指定Adobe Analytics如何处理个人数据。 此属性可接受两个可能的值： <ul><li>`anonymize`:给定用户ID集合引用的所有数据均设为匿名。 如果 `analyticsDeleteMethod` ，这是默认行为。</li><li>`purge`:所有数据都将被完全删除。</li></ul> |
| `mergePolicyId` | 在对实时客户资料(`profileService`)，则可以选择提供特定 [合并策略](../../profile/merge-policies/overview.md) 用于ID拼合的ID。 通过指定合并策略，在返回客户数据时，隐私请求可以包含区段信息。 每个请求只能指定一个合并策略。 如果未提供合并策略，则响应中不会包含分段信息。 |
| `regulation` **（必需）** | 隐私工作的法规。 接受以下值： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>请参阅 [受支持法规](../regulations/overview.md) 有关上述值代表的隐私法规的更多信息。 |

{style=&quot;table-layout:auto&quot;}

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
| `jobId` | 作业的只读、唯一的系统生成ID。 此值用于查找特定作业的下一步。 |

{style=&quot;table-layout:auto&quot;}

成功提交作业请求后，可以继续执行 [检查作业的状态](#check-status).

## 检查作业的状态 {#check-status}

您可以通过包含特定作业的来检索有关特定作业的信息，如其当前处理状态 `jobId` 在GET请求的路径中 `/jobs` 端点。

>[!IMPORTANT]
>
>之前创建的作业的数据只能在作业完成日期后的30天内检索。

**API格式**

```http
GET /jobs/{JOB_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{JOB_ID}` | 要查找的作业的ID。 此ID在 `jobId` 成功响应 [创建工作](#create-job) 和 [列出所有作业](#list). |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求可检索其 `jobId` 在请求路径中提供。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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
| `productStatusResponse` | 中的每个对象 `productResponses` 数组包含有关作业当前状态(与特定 [!DNL Experience Cloud] 应用程序。 |
| `productStatusResponse.status` | 作业的当前状态类别。 有关 [可用状态类别](#status-categories) 以及它们的对应含义。 |
| `productStatusResponse.message` | 作业的特定状态，对应于状态类别。 |
| `productStatusResponse.responseMsgCode` | 收到的产品响应消息的标准代码 [!DNL Privacy Service]. 详情请见 `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | 有关作业状态的更详细说明。 不同产品中状态相似的消息可能会有所不同。 |
| `productStatusResponse.results` | 对于某些状态，某些产品可能会返回 `results` 提供未涵盖的其他信息的对象 `responseMsgDetail`. |
| `downloadURL` | 如果作业的状态为 `complete`，此属性会提供一个URL，用于将作业结果下载为ZIP文件。 此文件可在作业完成后60天内下载。 |

{style=&quot;table-layout:auto&quot;}

### 作业状态类别 {#status-categories}

下表列出了不同的可能职务状态类别及其相应含义：

| 状态类别 | 含义 |
| -------------- | -------- |
| `complete` | 作业已完成，并且（如果需要）会从每个应用程序上传文件。 |
| `processing` | 应用程序已确认该作业，并且当前正在处理。 |
| `submitted` | 作业会提交到每个适用的应用程序。 |
| `error` | 处理作业时出现故障 — 可通过检索单个作业详细信息来获取更具体的信息。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>提交的作业可能保留在 `processing` 状态（如果它有一个从属子作业仍在处理）。

## 后续步骤

您现在知道如何使用 [!DNL Privacy Service] API。 有关如何使用用户界面执行相同任务的信息，请参阅 [Privacy ServiceUI概述](../ui/overview.md).
