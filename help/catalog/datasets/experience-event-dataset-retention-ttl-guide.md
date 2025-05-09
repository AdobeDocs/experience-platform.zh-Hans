---
title: 使用TTL在数据湖中管理体验事件数据集保留
description: 了解如何使用生存时间(TTL)配置和Adobe Experience Platform API评估、设置和管理Data Lake中的Experience Event数据集保留。 本指南介绍TTL行级到期如何支持数据保留策略、优化存储效率并确保有效的数据生命周期管理。 它还提供了用例和最佳实践，帮助您有效应用TTL。
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: 13db0477c0f42d0808647937d40c25b47a270894
workflow-type: tm+mt
source-wordcount: '2452'
ht-degree: 0%

---

# 使用TTL在数据湖中管理体验事件数据集保留

高效的数据管理对于优化性能、成本控制和数据完整性至关重要。 使用体验事件数据集保留生存时间(TTL)强制行级过期，从而自动从数据湖中的数据集中删除过期的记录，同时确保最佳存储效率和数据相关性。

本指南介绍如何使用目录服务API评估、设置和管理TTL。 您将了解何时应用TTL以及为何应用，如何使用API调用配置和更新TTL值，以及确保有效实施的最佳实践。

>[!IMPORTANT]
>
>TTL旨在优化数据生命周期管理和存储效率。 它不是法规遵从性工具，不应依赖它来满足管理法规要求。 法规遵从性往往需要更广泛的数据治理战略。

## 为何使用TTL进行行级数据管理

随着数据集的增长，高效的数据管理对于保持性能、控制成本和保持数据的相关性变得越来越重要。 基于TTL的行级数据过期无需手动干预即可删除过期记录，从而自动执行数据清理，帮助优化存储并提高系统效率。

TTL在管理随时间推移失去相关性的时效性数据时非常有用。 如果需要，请考虑实施TTL：

- 通过自动删除过时的记录降低存储成本。
- 通过最小化不相关数据来提高查询性能。
- 通过仅保留相关信息来维护数据卫生。
- 优化数据保留以支持业务目标。

>[!NOTE]
>
>体验事件数据集保留适用于存储在数据湖中的事件数据。 如果您在Real-Time Customer Data Platform中管理保留，请考虑将[体验事件过期](../../profile/event-expirations.md)和[假名配置文件过期](../../profile/pseudonymous-profiles.md)与数据湖保留设置一起使用。

使用TTL配置可根据权限优化存储。 虽然配置文件存储数据(用于Real-Time CDP)可被视为已过期并在30天后删除，但对于Analytics和Data Distiller用例，数据湖中的相同事件数据仍可在12-13个月（或更长时间，根据权限）内可用。

>[!TIP]
>
>权利指您的Adobe订阅和许可协议定义的存储和保留期限。

### 行业示例 {#industry-example}

例如，考虑使用视频流服务来跟踪用户交互，如视频查看、搜索和推荐。 尽管最近的参与数据对个性化至关重要，但旧的活动日志（例如，一年多以前的互动）将失去相关性。 通过使用行级过期，Experience Platform可自动删除过时的日志，从而确保仅将当前且有意义的数据用于分析和推荐。

## 评估TTL适用性 {#evaluate-ttl-suitability}

在应用保留策略之前，请评估您的数据集是否是行级到期的良好候选数据集。 请考虑以下事项：

- 随时间变化的数据相关性：旧数据是否提供价值，还是会过时？
- 对下游流程的影响：删除数据是否会影响报表、分析或集成？
- 存储成本与保留价值：旧数据的价值是否能够证明存储数据的成本合理？

如果历史记录对于长期分析或业务运营至关重要，则TTL可能不是正确的方法。 查看这些因素可确保TTL符合您的数据保留需求，而不会对数据可用性产生负面影响。

## 设置TTL的最佳实践 {#best-practices}

选择适当的TTL值，以确保您的Experience Event数据集保留策略在数据保留、存储效率和分析需求之间取得平衡。 TTL过短可能会导致数据丢失，而过长可能会增加存储成本和不必要的数据累积。 通过考虑访问数据的频率以及数据保持相关的时长，确保TTL与数据集的目的一致。

下表提供了基于数据集类型和使用模式的常见TTL建议：

| 数据集类型 | 建议的TTL | 典型用例 |
|-----------------------------|------------------------|-------------------|
| 经常访问的数据集 | 30-90天 | 用户参与日志、网站点击流数据、短期促销活动效果数据。 |
| 存档数据集 | 1年或以上 | 财务交易记录、合规性数据、长期趋势分析、机器学习训练数据集。 |
| 应用程序管理的数据集 | 长达13个月 | 系统管理的数据集具有预定义的TTL限制，将自动强制实施这些限制以遵守系统施加的限制。 |
| 客户管理的数据集 | 30天 — 最大TTL | 通过UI、API或数据Distiller创建的数据集。 TTL必须至少为30天并且位于定义的最大TTL内。 |

请定期检查TTL设置，以确保它们持续与您的存储策略、分析需要和业务需求保持一致。

### 设置TTL时的关键注意事项 {#key-considerations}

请遵循以下最佳实践，确保TTL设置与您的数据保留策略一致：

- 定期审核TTL更改。 每次TTL更新都会触发审核事件。 使用审核日志跟踪TTL修改，以实现合规性、数据治理和疑难解答。
- 如果数据必须无限期保留，则禁用TTL。 要禁用TTL，请将`ttlValue`设置为`null`。 这样可防止自动过期并永久保留所有记录。 在进行此更改之前，请考虑对存储的影响。

## TTL的限制 {#limitations}

使用TTL时，请注意以下限制：

- 使用TTL的&#x200B;**体验事件数据集保留适用于行级过期**，而不适用于数据集删除。 TTL会根据定义的保留期删除记录，但不会删除整个数据集。 要删除数据集，请使用[数据集到期终结点](../../hygiene/api/dataset-expiration.md)或手动删除。
- **TTL配置保持活动状态，直到显式禁用**。 在禁用该配置之前，该配置将一直有效。 禁用TTL将停止过期，并确保保留数据集中的所有记录。
- **TTL不是合规性工具**。 在TTL优化存储和生命周期管理的同时，您必须实施更广泛的治理策略以确保法规遵从性。

## 在应用TTL之前分析数据集大小和相关性 {#analyze-dataset-size}

在应用TTL之前，请使用查询分析数据集大小和相关性。 运行定向查询（如对特定日期范围内的记录进行计数）以预览各种TTL值的影响。 然后，使用此信息选择最佳保留期，以平衡数据效用和经济效益。

![在体验事件数据集上实施TTL的可视化工作流。 步骤包括：评估数据生命周期和删除的影响，使用查询验证TTL设置，通过目录服务API配置TTL，以及持续监视TTL影响并进行调整。](../images/datasets/dataset-retention-ttl-guide/manage-experience-event-dataset-retention-in-the-data-lake.png)

运行定位查询有助于确定在不同的TTL配置下将保留或删除的数据量。 例如，以下SQL查询计算过去30天内创建的记录数：

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

对不同时间间隔运行类似的查询有助于验证TTL设置，并确保它们在存储效率和数据可访问性之间取得平衡。

## TTL管理入门

您必须了解如何正确设置请求格式，然后才能使用目录服务API评估、设置和管理Experience Event数据集保留。 这包括了解API路径、提供所需的标头以及格式化请求负载。 请参阅[目录服务API快速入门指南](../api/getting-started.md)以了解此基本信息。

>[!NOTE]
>
>本文档介绍了行级过期，即删除数据集中个别已过期的行，同时保持数据集本身不变。 它不适用于数据集过期，该功能会删除整个数据集，并受一个单独的功能管理。 有关数据集级别的过期，请参阅[数据集过期API文档](../../hygiene/api/dataset-expiration.md)。

### 检查TTL约束 {#check-ttl-constraints}

使用数据卫生API `/ttl/{DATASET_ID}`端点帮助规划TTL配置。 此端点返回您的组织支持的最小TTL值和最大TTL值，以及数据集类型的推荐值(`defaultValue`)。

有关详细信息，请参阅Adobe Developer [数据卫生API](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/#operation/getTtl)文档。

要[检查当前应用于数据集](#check-applied-ttl-values)的TTL，请改为向[目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/) `/dataSets/{DATASET_ID}`端点发出GET请求。

>[!TIP]
>
>目录服务API的Experience Platform网关URL和基本路径为： `https://platform.adobe.io/data/foundation/catalog`。 数据卫生API的基本路径为： `https://platform.adobe.io/data/core/hygiene`

**API格式**

```http
GET /ttl/{DATASET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 系统生成的字符串，唯一标识数据集。 要查找数据集ID，请使用`/datasets`端点。 有关筛选相关数据集的响应的说明，请参阅[列表目录对象API指南](../api/list-objects.md)。 |

**请求**

以下请求检索贵组织针对特定数据集的TTL限制。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**响应**

成功的响应会根据您组织的权限返回建议的、最大和最小的TTL值，以及数据集的建议TTL (`defaultValue`)。 此`defaultValue`是建议的TTL持续时间，仅供参考。 除非您明确配置，否则不会应用它。 响应不包含任何可能已设置的自定义TTL值。 要查看数据集的当前TTL，请使用GET `/catalog/dataSets/{DATASET_ID}`端点。

+++选择以查看响应

```json
{
  "extensions": {
    "adobe_lakeHouse": {
      "rowExpiration": {
        "defaultValue": "P12M",
        "maxValue": "P12M",
        "minValue": "P7D"
      }
    }
  }
}
```

+++

| 属性 | 描述 |
|--------------|-------------|
| `defaultValue` | 为数据集推荐的TTL值。 此值为&#x200B;**不是自动应用的**。 必须明确设置TTL才能使其生效。 |
| `maxValue` | 您组织的权利允许的最长TTL持续时间。 通常，此持续时间为10年(`P10Y`)。 |
| `minValue` | 您组织的权利允许的最短TTL持续时间。 通常，此持续时间为30天(`P30D`)。 |

### 如何检查应用的TTL值 {#check-applied-ttl-values}

要检查已应用于数据集的当前TTL值，请使用以下API调用：

```http
GET /dataSets/{DATASET_ID}
```

此调用返回`extensions.adobe_lakeHouse.rowExpiration`分区中的当前`ttlValue`（如果已设置）。

**请求**

以下请求检索贵组织的特定数据集的TTL值。

```shell
curl -X GET \
https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包括`extensions`对象，该对象包含应用于数据集的当前TTL配置。 为简短起见，下面的响应示例被截断。

```json
{
    "{DATASET_ID}": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M",
            }
            }
        }
        ...
    }
}
```

### 设置或更新数据集的TTL {#set-update-ttl}

>[!IMPORTANT]
>
>基于TTL的行级过期仅适用于使用时间序列架构的事件数据集。 这包括基于标准XDM ExperienceEvent类的数据集，以及扩展时间序列架构(`https://ns.adobe.com/xdm/data/time-series`)的自定义架构。
>
>在应用TTL之前，请使用架构注册表API通过检查`meta:extends`属性来验证数据集的架构是否包含正确的扩展。 有关如何执行此操作的指导，请参阅[架构终结点文档](../../xdm/api/schemas.md#lookup)。

您可以通过设置新的TTL或使用相同的API方法更新现有TTL来配置Experience Event数据集保留。 使用对`/v2/datasets/{DATASET_ID}`端点的PATCH请求来应用或调整TTL。

**API格式**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要为其更新TTL值的数据集的ID。 |

**请求**

在以下示例中，`ttlValue`设置为`P3M`。 这意味着超过3个月的记录将被自动删除。 调整保留期以满足您的业务需求（例如，`P6M`保留六个月或`P12M`保留一年）。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M"  // A 3 month retention period
            }
        }
    }
}
```

| 属性 | 描述 |
|----------------------------------|-------------|
| `rowExpiration.ttlValue` | 定义自动移除数据集中的记录之前的持续时间。 使用ISO-8601期间格式（例如，`P3M`表示3个月，`P30D`表示30天）。 |

**响应**

成功的响应会返回对更新数据集的引用，但不明确包含TTL设置。 要确认TTL配置，请跟进`GET /dataSets/{DATASET_ID}`请求。

```JSON
[
  "@/dataSets/{DATASET_ID}"
]
```

#### 示例场景 {#example-scenario}

考虑一个视频流平台，该平台最初将TTL设置为三个月，以确保提供最新的个性化参与数据。 但是，如果后续分析显示旧交互仍可提供有价值的洞察，则可以通过以下请求将TTL延长到六个月：

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P6M"  // Extend to 6 months
            }
        }
    }
}
```

## 数据集保留策略常见问题解答 {#faqs}

此常见问题解答涵盖有关数据集保留作业、TTL更改的即时影响、恢复选项以及保留期在Platform服务中的不同之处等实际问题。

### 可以将保留策略规则应用到哪些类型的数据集？

+++回答
您可以将基于TTL的保留策略应用到任何使用时间序列行为的数据集。 这包括基于标准XDM ExperienceEvent类的数据集，以及旨在捕获时间序列数据的自定义架构。

行级过期需要满足以下技术条件：

- 架构必须设计为捕获时间序列数据。
- 架构必须包含用于评估过期时间的时间戳字段。
- 数据集应存储事件级数据，通常使用或扩展XDM ExperienceEvent类。
- 数据集必须在目录服务中注册，因为通过`extensions.adobe_lakeHouse.rowExpiration`应用TTL设置。
- TTL值必须使用ISO-8601持续时间格式（例如，`P30D`、`P6M`、`P1Y`）。
+++

### 数据集保留作业多久将从数据湖服务中删除数据？

+++回答
每30天评估和处理一次数据集TTL，并删除所有过期的记录。 如果事件摄取到Experience Platform超过30天（摄取日期> 30天）并且其事件日期超过定义的保留期(TTL)，则该事件被视为已过期。
+++

<!-- ### How soon will the Dataset Retention job delete data from Profile services?

+++Answer
Once a retention policy is set, existing events that already exceed the newly defined TTL are immediately deleted. Newer events remain until their timestamps surpass the retention period.

For example, if you apply a 30-day expiration policy on May 15th, the following occurs:

- New events receive a 30-day expiration as they are ingested.
- Existing events with a timestamp older than April 15th are immediately deleted.
- Existing events with a timestamp after April 15th are set to expire 30 days after their timestamp (for example, an event from April 18th would be deleted on May 18th).
+++ -->

### 我是否可以为数据湖和配置文件服务设置不同的保留策略？

+++回答
可以，您可以为Data Lake和Profile Services设置不同的保留策略。 但是，配置文件的保留期不得短于为数据湖设置的保留期。
+++

### 如何检查我当前的数据集使用情况？

+++回答
您可以在[!UICONTROL 数据集]清单工作区中检查数据湖和配置文件存储作为单独指标的最新数据集存储大小。 对列进行排序，以确定最大的数据集，并验证是否应用了保留策略。

有关沙盒级别的使用情况，请参阅许可证使用仪表板。 有关详细信息，请参阅[许可证使用文档](../../dashboards/guides/license-usage.md)。
+++

### 如何验证数据保留作业是否成功？

+++回答
您可以通过在[数据集保留配置UI](./user-guide.md#data-retention-policy)中或在“数据清单”页面上检查其时间戳来验证最后一个数据保留作业。

或者，您可以向以下端点发出GET请求：

`GET https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID}`

响应包括属性`extensions.adobe_lakeHouse.rowExpiration.lastCompleted`，该属性指示最近一次完成TTL作业时的Unix时间戳（以毫秒为单位）。

历史数据集使用情况报表当前不可用。
+++

### 能否恢复已删除的数据？

+++回答
不会，应用保留策略后，任何超过保留期的数据都会被永久删除，并且无法恢复。
+++

### 我可以在Data Lake Experience Event数据集上配置的最低TTL是多少？

+++回答
数据湖体验事件数据集的最小TTL为30天。 数据湖在初始摄取和处理期间充当处理备份和恢复系统。 因此，数据必须在摄取后在数据湖中保留至少30天，然后才能过期。
+++

### 如果需要保留某些Data Lake字段的时间长于我的TTL策略允许的时间，该怎么办？

+++回答
使用Data Distiller可保留超出数据集TTL的特定字段，同时不超出利用率限制。 创建一个定期仅将必要字段写入派生数据集的作业。 此工作流可确保遵循更短的TTL，同时保留关键数据以供扩展使用。

有关详细信息，请参阅[使用SQL创建派生数据集指南](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md)。
+++

## 后续步骤 {#next-steps}

现在您已了解如何管理行级过期的TTL设置，请查看以下文档以进一步了解TTL管理：

- 保留作业：了解如何使用[数据生命周期UI指南](../../hygiene/ui/dataset-expiration.md)在Experience Platform UI中计划和自动化数据集过期，或检查数据集保留配置并验证是否删除了过期的记录。
- [数据集过期API终结点指南](../../hygiene/api/dataset-expiration.md)：了解如何删除整个数据集，而不仅仅是删除行。 了解如何使用API计划、管理和自动化数据集过期以确保有效的数据保留。
- [数据使用策略概述](../../data-governance/policies/overview.md)：了解如何使您的数据保留策略与更广泛的合规性要求和营销使用限制保持一致。
