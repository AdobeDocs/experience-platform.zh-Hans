---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 隐私作业API端点
description: 了解如何使用Privacy ServiceAPI管理Experience Cloud应用程序的隐私作业。
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 9d05752f3db78d9d10fd91fd0d3fed924217199c
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 1%

---

# 隐私作业端点

本文档介绍如何使用API调用处理隐私作业。 具体来说，它涵盖了 `/job` 中的端点 [!DNL Privacy Service] API。 在阅读本指南之前，请参阅 [快速入门指南](./getting-started.md) 有关成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

>[!NOTE]
>
>如果您尝试管理客户的同意或选择退出请求，请参阅 [同意端点指南](./consent.md).

## 列出所有作业 {#list}

您可以向以下网站发出GET请求，查看贵组织内所有可用隐私作业的列表： `/jobs` 端点。

**API格式**

此请求格式使用 `regulation` 上的查询参数 `/jobs` 端点，因此它以问号(`?`)，如下所示。 响应采用分页方式，允许您使用其他查询参数(`page` 和 `size`)以筛选响应。 可以使用与号(`&`)。

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| 参数 | 描述 |
| --- | --- |
| `{REGULATION}` | 要查询的法规类型。 接受的值包括： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpa`</li><li>`cpra_usa`</li><li>`ctdpa`</li><li>`ctdpa_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`ucpa_usa`</li><li>`vcdpa_usa`</li></ul><br>有关更多详细信息，请参阅 [受支持的法规](../regulations/overview.md) 有关上述值代表的隐私法规的更多信息。 |
| `{PAGE}` | 要显示的数据页面，使用基于0的编号。 默认值为 `0`。 |
| `{SIZE}` | 每页上显示的结果数。 默认为 `1` 最大值为 `100`. 超过最大值会导致API返回400代码错误。 |

{style="table-layout:auto"}

<!-- Not released yet:
<li>`pdpd_vnm`</li>
 -->

**请求**

以下请求检索组织内所有作业的分页列表，从页面大小为50的第三个页面开始。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的响应将返回作业列表，每个作业都包含详细信息，例如 `jobId`. 在此示例中，响应将包含一个50个作业的列表，从结果的第三页开始。

### 访问后续页面

要在分页响应中获取下一组结果，您必须对同一端点进行另一个API调用，同时增加 `page` 按1查询参数。

## 创建隐私作业 {#create-job}

>[!IMPORTANT]
>
>Privacy Service仅适用于数据主体和消费者权利请求。 不支持或允许将Privacy Service用于数据清理或维护。 Adobe有及时履行这些义务的法律义务。 因此，不允许对Privacy Service进行负载测试，因为它是仅用于生产的环境，并会创建有效隐私请求的不必要积压。
>
>现已设定每日硬性上传限制，以防止滥用服务。 发现滥用系统的用户将禁用其对该服务的访问权限。 随后将与他们举行一次会议，讨论他们的行动并讨论可接受的Privacy Service用途。

在创建新的作业请求之前，必须首先收集有关要访问、删除或选择退出销售其数据的数据主体的标识信息。 获得所需数据后，必须在POST请求的有效负载中提供，以便 `/jobs` 端点。

>[!NOTE]
>
>兼容的Adobe Experience Cloud应用程序使用不同的值来标识数据主体。 请参阅指南，网址为 [Privacy Service和Experience Cloud应用程序](../experience-cloud-apps.md) 以了解有关应用程序所需的标识符的更多信息。 有关确定要将哪些ID发送到的更一般的指导 [!DNL Privacy Service]，请参阅上的文档 [隐私请求中的身份数据](../identity-data.md).

此 [!DNL Privacy Service] API支持两种针对个人数据的作业请求：

* [访问和/或删除](#access-delete)：访问（读取）或删除个人数据。
* [选择退出销售](#opt-out)：将个人数据标记为不出售。

>[!IMPORTANT]
>
>虽然访问和删除请求可以作为单个API调用进行组合，但必须单独发出选择退出请求。

### 创建访问/删除作业 {#access-delete}

此部分演示了如何使用API发出访问/删除作业请求。

**API格式**

```http
POST /jobs
```

**请求**

以下请求创建新的作业请求，该请求由有效负载中提供的属性进行配置，如下所述。

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
| `companyContexts` **（必需）** | 包含您组织的身份验证信息的数组。 列出的每个标识符都包含以下属性： <ul><li>`namespace`：标识符的命名空间。</li><li>`value`：标识符的值。</li></ul>它是 **必填** 其中一个标识符使用 `imsOrgId` 作为 `namespace`，及其 `value` 包含贵组织的唯一ID。 <br/><br/>其他标识符可以是产品特定的公司限定符(例如， `Campaign`)，用于标识与属于您组织的Adobe应用程序的集成。 潜在值包括帐户名称、客户端代码、租户ID或其他应用程序标识符。 |
| `users` **（必需）** | 一个数组，其中包含您要访问或删除其信息的至少一个用户的集合。 单个请求中最多可提供1000个用户ID。 每个用户对象包含以下信息： <ul><li>`key`：用于限定响应数据中各个作业ID的用户的标识符。 最好为此值选择一个唯一的、易于识别的字符串，以便稍后可以轻松引用或查找。</li><li>`action`：一个数组，列出了要对用户数据执行的所需操作。 根据您要执行的操作，此阵列必须包括 `access`， `delete`，或同时使用两者。</li><li>`userIDs`：用户的身份集合。 单个用户可以拥有的身份数限制为9个。 每个标识都包含 `namespace`， a `value`和命名空间限定符(`type`)。 请参阅 [附录](appendix.md) 以了解有关这些必需属性的更多详细信息。</li></ul> 有关更多详细信息，请参阅 `users` 和 `userIDs`，请参见 [疑难解答指南](../troubleshooting-guide.md#user-ids). |
| `include` **（必需）** | 要包含在处理中的一系列Adobe产品。 如果此值缺失或为空，则将拒绝请求。 仅包括您的组织与之集成的产品。 请参阅以下部分 [接受的产品值](appendix.md) ，以了解更多信息。 |
| `expandIDs` | 可选属性，设置为时 `true`，表示对应用程序中处理ID的优化(当前仅受支持 [!DNL Analytics])。 如果忽略，此值将默认为 `false`. |
| `priority` | Adobe Analytics使用的一个可选属性，用于设置处理请求的优先级。 接受的值包括 `normal` 和 `low`. 如果 `priority` 将被忽略，默认行为为 `normal`. |
| `analyticsDeleteMethod` | 一个可选属性，指定Adobe Analytics应如何处理个人数据。 此属性可接受两个可能的值： <ul><li>`anonymize`：给定用户ID集合引用的所有数据均采用匿名形式。 如果 `analyticsDeleteMethod` 将被忽略，这是默认行为。</li><li>`purge`：完全删除所有数据。</li></ul> |
| `mergePolicyId` | 对实时客户个人资料发出隐私请求时(`profileService`)，您可以选择提供特定 [合并策略](../../profile/merge-policies/overview.md) 要用于ID拼接的区段。 通过指定合并策略，隐私请求可以在返回客户数据时包含受众信息。 每个请求只能指定一个合并策略。 如果未提供合并策略，则响应中不包含分段信息。 |
| `regulation` **（必需）** | 隐私工作的法规。 接受以下值： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>有关更多详细信息，请参阅 [受支持的法规](../regulations/overview.md) 有关上述值代表的隐私法规的更多信息。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回新创建的作业的详细信息。

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
| `jobId` | 系统为作业生成的只读ID。 此值将在查找特定作业的下一个步骤中使用。 |

{style="table-layout:auto"}

成功提交作业请求后，您可以继续的下一步 [检查作业状态](#check-status).

## 检查作业的状态 {#check-status}

通过包含特定作业的信息，您可以检索该作业的信息，例如其当前处理状态 `jobId` 在GET请求的路径中 `/jobs` 端点。

>[!IMPORTANT]
>
>以前创建的作业的数据只能在作业完成日期后的30天内进行检索。

**API格式**

```http
GET /jobs/{JOB_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{JOB_ID}` | 要查找的作业的ID。 此ID返回到 `jobId` 在成功的API响应中 [创建作业](#create-job) 和 [列出所有作业](#list). |

{style="table-layout:auto"}

**请求**

以下请求检索其作业的详细信息 `jobId` 在请求路径中提供。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的响应将返回指定作业的详细信息。

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
| `productStatusResponse` | 内的每个对象 `productResponses` 数组包含有关特定作业当前状态的信息 [!DNL Experience Cloud] 应用程序。 |
| `productStatusResponse.status` | 作业的当前状态类别。 请参阅下表中的列表 [可用状态类别](#status-categories) 以及它们的相应含义。 |
| `productStatusResponse.message` | 作业的特定状态，对应于状态类别。 |
| `productStatusResponse.responseMsgCode` | 接收的产品响应消息的标准代码 [!DNL Privacy Service]. 报文详情在下提供 `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | 有关作业状态的更详细说明。 类似状态的消息可能因产品而异。 |
| `productStatusResponse.results` | 对于某些状态，某些产品可能会返回 `results` 提供未涵盖的其他信息的对象 `responseMsgDetail`. |
| `downloadURL` | 如果作业的状态为 `complete`，此属性会提供一个URL以将作业结果下载为ZIP文件。 在作业完成后60天内可下载此文件。 |

{style="table-layout:auto"}

### 作业状态类别 {#status-categories}

下表列出了不同的可能作业状态类别及其相应含义：

| 状态类别 | 含义 |
| -------------- | -------- |
| `complete` | 作业已完成，并（如果需要）从每个应用程序上传文件。 |
| `processing` | 应用程序已确认该作业，当前正在处理。 |
| `submitted` | 作业将提交给每个适用的应用程序。 |
| `error` | 处理作业时出现问题 — 通过检索各个作业详细信息可能会获得更具体的信息。 |

{style="table-layout:auto"}

>[!NOTE]
>
>提交的作业可能保留在 `processing` 表明它是否具有仍在处理的依赖子作业。

## 后续步骤

您现在知道如何使用 [!DNL Privacy Service] API。 有关如何使用用户界面执行相同任务的信息，请参见 [Privacy ServiceUI概述](../ui/overview.md).
