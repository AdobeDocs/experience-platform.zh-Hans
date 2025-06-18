---
keywords: Experience Platform；首页；热门话题
solution: Experience Platform
title: 隐私作业API端点
description: 了解如何使用Privacy Service API管理Experience Cloud应用程序的隐私作业。
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: c2394035dd6bd4fe6dbb443e4db13934a27066a6
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 1%

---

# 隐私作业端点

>[!IMPORTANT]
>
>为了支持数量不断增长的美国州隐私法，Privacy Service正在更改其`regulation_type`值。 使用包含从&#x200B;**2025年6月12日开始的状态缩写（例如`ucpa_ut_usa`）的新值**。 旧值（例如`ucpa_usa`）在&#x200B;**2025年7月28日**&#x200B;之后停止工作。
>
>在此截止日期之前更新您的集成，以避免请求失败。

本文档介绍如何使用API调用处理隐私作业。 具体来说，它涵盖[!DNL Privacy Service] API中`/job`端点的使用。 在阅读本指南之前，请参阅[入门指南](./getting-started.md)以了解成功调用API所需了解的重要信息，包括所需的标头以及如何阅读示例API调用。

>[!NOTE]
>
>如果您尝试管理客户的同意或选择退出请求，请参阅[同意端点指南](./consent.md)。

## 列出所有作业 {#list}

您可以通过对`/jobs`端点发出GET请求来查看组织内所有可用隐私作业的列表。

**API格式**

此请求格式在`/jobs`端点上使用`regulation`查询参数，因此它以问号(`?`)开头，如下所示。 在列出资源时，Privacy Service API最多返回1000个作业并分页响应。 使用其他查询参数（`page`、`size`和日期筛选器）筛选响应。 可以使用&amp;符号(`&`)分隔多个参数。

>[!TIP]
>
>使用其他查询参数进一步筛选特定查询的结果。 例如，您可以使用`status`、`fromDate`和`toDate`查询参数来发现给定时间段内提交的隐私作业数量及其状态。

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
GET /jobs?regulation={REGULATION}&fromDate={FROMDATE}&toDate={TODATE}&status={STATUS}
```

| 参数 | 描述 |
| --- | --- |
| `{REGULATION}` | 要查询的法规类型。 接受的值包括： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpa_co_usa`</li><li>`cpra_ca_usa`</li><li>`ctdpa_ct_usa`</li><li>`dpdpa_de_usa`</li><li>`fdbr_fl_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`icdpa_ia_usa`</li><li>`lgpd_bra`</li><li>`mcdpa_mn_usa`</li><li>`mcdpa_mt_usa`</li><li>`mhmda_wa_usa`</li><li>`ndpa_ne_usa`</li><li>`nhpa_nh_usa`</li><li>`njdpa_nj_usa`</li><li>`nzpa_nzl`</li><li>`ocpa_or_usa`</li><li>`pdpa_tha`</li><li>`ql25_qc_can`</li><li>`tdpsa_tx_usa`</li><li>`tipa_tn_usa`</li><li>`ucpa_ut_usa`</li><li>`vcdpa_va_usa`</li></ul><br>有关上述值表示的隐私法规的更多信息，请参阅[支持的法规](../regulations/overview.md)概述。 |
| `{PAGE}` | 要显示的数据页面，使用基于0的编号。 默认值为 `0`。 |
| `{SIZE}` | 每页上显示的结果数。 默认值为`100`，最大值为`1000`。 超过最大值会导致API返回400代码错误。 |
| `{status}` | 默认行为是包括所有状态。 如果指定状态类型，则请求将仅返回与该状态类型匹配的隐私作业。 接受的值包括： <ul><li>`processing`</li><li>`complete`</li><li>`error`</li></ul> |
| `{toDate}` | 此参数将结果限制为指定日期之前处理的结果。 从发出请求之日起，系统回顾时间可达45天。 但是，范围不能超过30天。<br>它接受YYYY-MM-DD格式。 您提供的日期将解释为以格林威治标准时间(GMT)表示的终止日期。<br>如果未提供此参数（以及相应的`fromDate`），则默认行为将返回过去七天中返回数据的作业。 如果您使用`toDate`，则还必须使用`fromDate`查询参数。 如果不同时使用这两个参数，调用将返回400错误。 |
| `{fromDate}` | 此参数将结果限制为指定日期后处理的结果。 从发出请求之日起，系统回顾时间可达45天。 但是，范围不能超过30天。<br>它接受YYYY-MM-DD格式。 您提供的日期将解释为以格林威治标准时间(GMT)表示的请求来源日期。<br>如果未提供此参数（以及相应的`toDate`），则默认行为将返回过去七天中返回数据的作业。 如果您使用`fromDate`，则还必须使用`toDate`查询参数。 如果不同时使用这两个参数，调用将返回400错误。 |
| `{filterDate}` | 此参数将结果限制为指定日期处理的结果。 它接受YYYY-MM-DD格式。 系统可以回顾过去45天。 |

{style="table-layout:auto"}

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

成功的响应将返回作业列表，每个作业都包含详细信息，如其`jobId`。 在此示例中，响应将包含一个50个作业的列表，从结果的第三页开始。

### 访问后续页面

要在分页响应中获取下一组结果，您必须对同一端点进行另一个API调用，同时将`page`查询参数增加1。

## 创建隐私作业 {#create-job}

>[!IMPORTANT]
>
>Privacy Service仅适用于数据主体和消费者权利请求。 不支持或允许将Privacy Service用于数据清理或维护的任何其他用途。 Adobe有及时履行这些义务的法律义务。 因此，不允许在Privacy Service上进行负载测试，因为它是一个仅用于生产的环境，并会创建有效隐私请求的不必要积压。
>
>现已设定每日硬性上传限制，以防止滥用服务。 发现滥用系统的用户将禁用其对该服务的访问权限。 随后将与他们举行一次会议，讨论他们的行动并讨论Privacy Service的可接受用途。

在创建新的作业请求之前，必须首先收集有关要访问、删除或选择退出销售其数据的数据主体的标识信息。 获得所需数据后，必须在POST请求的有效负载中将其提供给`/jobs`端点。

>[!NOTE]
>
>兼容的Adobe Experience Cloud应用程序使用不同的值来标识数据主体。 请参阅[Privacy Service和Experience Cloud应用程序](../experience-cloud-apps.md)指南，以了解应用程序所需标识符的更多信息。 有关确定将哪些ID发送到[!DNL Privacy Service]的更一般的指导，请参阅隐私请求[&#128279;](../identity-data.md)中有关身份数据的文档。

[!DNL Privacy Service] API支持两种针对个人数据的作业请求：

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
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| 属性 | 描述 |
| --- | --- |
| `companyContexts` **（必需）** | 包含您组织的身份验证信息的数组。 列出的每个标识符都包含以下属性： <ul><li>`namespace`：标识符的命名空间。</li><li>`value`：标识符的值。</li></ul>**必需**，其中一个标识符使用`imsOrgId`作为其`namespace`，其`value`包含您组织的唯一ID。 <br/><br/>其他标识符可以是产品特定的公司限定符（例如，`Campaign`），用于标识与属于您组织的Adobe应用程序的集成。 潜在值包括帐户名称、客户端代码、租户ID或其他应用程序标识符。 |
| `users` **（必需）** | 一个数组，其中包含您要访问或删除其信息的至少一个用户的集合。 单个请求最多可提供1000个用户。 每个用户对象包含以下信息： <ul><li>`key`：用于限定响应数据中各个作业ID的用户的标识符。 最好为此值选择一个唯一的、易于识别的字符串，以便稍后可以轻松引用或查找。</li><li>`action`：一个数组，列出了要对用户数据执行的所需操作。 根据您要执行的操作，此数组必须包括`access`和/或`delete`。</li><li>`userIDs`：用户的标识集合。 单个用户可以拥有的身份数限制为9个。 每个标识都包含`namespace`、`value`和命名空间限定符(`type`)。 有关这些所需属性的更多详细信息，请参阅[附录](appendix.md)。</li></ul> 有关`users`和`userIDs`的更详细说明，请参阅[疑难解答指南](../troubleshooting-guide.md#user-ids)。 |
| `include` **（必需）** | 要包含在处理中的一系列Adobe产品。 如果此值缺失或为空，则将拒绝请求。 仅包括您的组织与之集成的产品。 有关详细信息，请参阅附录中有关[接受的产品值](appendix.md)的部分。 |
| `expandIDs` | 一个可选属性，当设置为`true`时，表示对处理应用程序中的ID进行优化（当前仅受[!DNL Analytics]支持）。 如果忽略，此值将默认为`false`。 |
| `priority` | Adobe Analytics使用的一个可选属性，用于设置处理请求的优先级。 接受的值包括 `normal` 和 `low`。如果忽略`priority`，则默认行为是`normal`。 |
| `mergePolicyId` | 对实时客户个人资料(`profileService`)发出隐私请求时，您可以选择提供要用于ID拼接的特定[合并策略](../../profile/merge-policies/overview.md)的ID。 通过指定合并策略，隐私请求可以在返回客户数据时包含受众信息。 每个请求只能指定一个合并策略。 如果未提供合并策略，则响应中不包含分段信息。 |
| `regulation` **（必需）** | 隐私工作的法规。 接受以下值： <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>有关上述值表示的隐私法规的更多信息，请参阅[支持的法规](../regulations/overview.md)概述。 |

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

成功提交作业请求后，您可以继续下一步操作[检查作业状态](#check-status)。

## 检查作业的状态 {#check-status}

通过在`/jobs`端点的GET请求路径中包含特定作业的`jobId`，您可以检索有关该作业的信息，例如其当前处理状态。

>[!IMPORTANT]
>
>以前创建的作业的数据只能在作业完成日期后的30天内进行检索。

**API格式**

```http
GET /jobs/{JOB_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{JOB_ID}` | 要查找的作业的ID。 在针对[创建作业](#create-job)和[列出所有作业](#list)的成功的API响应中，此ID在`jobId`下返回。 |

{style="table-layout:auto"}

**请求**

以下请求检索在请求路径中提供了`jobId`的作业的详细信息。

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
| `productStatusResponse` | `productResponses`数组中的每个对象都包含有关特定[!DNL Experience Cloud]应用程序的作业当前状态的信息。 |
| `productStatusResponse.status` | 作业的当前状态类别。 有关[可用状态类别](#status-categories)及其相应含义的列表，请参见下表。 |
| `productStatusResponse.message` | 作业的特定状态，对应于状态类别。 |
| `productStatusResponse.responseMsgCode` | [!DNL Privacy Service]收到的产品响应消息的标准代码。 在`responseMsgDetail`下提供了消息的详细信息。 |
| `productStatusResponse.responseMsgDetail` | 有关作业状态的更详细说明。 类似状态的消息可能因产品而异。 |
| `productStatusResponse.results` | 对于某些状态，某些产品可能返回提供`responseMsgDetail`未涵盖的其他信息的`results`对象。 |
| `downloadURL` | 如果作业的状态为`complete`，则此属性会提供一个URL以将作业结果下载为ZIP文件。 在作业完成后60天内可下载此文件。 |

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
>如果提交的作业具有仍在处理的依赖子作业，则该作业可能仍处于`processing`状态。

## 后续步骤

您现在知道如何使用[!DNL Privacy Service] API创建和监视隐私作业。 有关如何使用用户界面执行相同任务的信息，请参阅[Privacy Service UI概述](../ui/overview.md)。
