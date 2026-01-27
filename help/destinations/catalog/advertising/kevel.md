---
title: Kevel连接
description: 使用Kevel流目标将受众直接激活到Kevel的UserDB和区段管理API中，并支持在决策时实时定位。
source-git-commit: d820485fd81efd08d8626f8476338558c4585c20
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 3%

---


# [!DNL Kevel]连接 {#kevel}

## 概述 {#overview}

[[!DNL Kevel]](https://www.kevel.com/)提供支持人工智能的技术和专家指导，帮助创新的商业领袖在零售媒体中启动、扩展和取得成功。 [!DNL Kevel]的Retail Media Cloud功能支持针对网站内和网站外广告采用可归因的可自定义广告格式。

Adobe Experience Platform的[!DNL Kevel]流目标允许客户将Adobe受众直接激活到[!DNL Kevel]的UserDB和区段管理API中，以支持在广告决策时进行实时定位。

>[!IMPORTANT]
> 
>如果您有问题或希望请求有关[!DNL Kevel]目标或其文档的更新，请通过[!DNL Kevel]support@kevel.com[向](mailto:support@kevel.com)团队发送电子邮件。

## 用例 {#use-cases}

您可以在零售媒体体验中激活丰富的第一方行为受众，以提供更相关的广告和更强大的性能。 在Experience Platform中，您可以构建高价值、基于意图的受众（例如经常访问类别的购物者或最近对产品感兴趣的用户），并将这些成员资格实时同步到[!DNL Kevel]。 [!DNL Kevel]立即使这些区段可用于ad decisioning，从而在搜索、浏览和应用程序体验间为赞助的产品和其他格式实现准确定位。 一旦用户符合条件，您就可以按照这些信号采取行动，提高相关的展示次数、改善定位效果，并改进测量和ROAS。

## 先决条件 {#prerequisites}

要准备使用[!DNL Kevel]目标，请确保满足以下先决条件：

- 您必须具有活动的&#x200B;**[!DNL Kevel]网络**&#x200B;和API访问权限。
- 您需要具有创建区段和更新UserDB记录权限的&#x200B;**[!DNL Kevel]API密钥**。
- 您必须在Experience Platform中配置标识命名空间，以将其映射到您的网站或应用程序在[!DNL Kevel]广告请求期间发送的标识（例如，ECID、GAID、IDFA、忠诚度ID等）。
- Adobe客户应仅映射在实时广告请求中使用的身份，因为每个身份都将生成UserDB记录。

## 支持的身份 {#supported-identities}

[!DNL Kevel]目标支持激活应用程序在向[!DNL Kevel]发送广告请求时可能使用的任何标识。 最多可以映射三个标识命名空间来生成相应的UserDB记录。

[!DNL Kevel]支持以下Experience Platform标识命名空间：

| 身份标识命名空间 | 描述 | 典型用法 |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | Experience Cloud ID | 用于现场个性化和跨Adobe识别。 |
| **GAID** | GOOGLE ADVERTISING ID | 用于Android应用程序/设备流量。 |
| **IDFA** | APPLE ADVERTISING ID | 用于iOS应用程序/设备流量（需经ATT同意）。 |
| **外部ID** | 外部ID（自定义标识符） | 传递专有或后端生成的ID。 |

{style="table-layout:auto"}

### 支持自定义身份命名空间

[!DNL Kevel]目标&#x200B;**还接受在Experience Platform实现中定义的自定义命名空间**。

这意味着：

- 您可以映射&#x200B;**特定于客户的标识命名空间**（例如： `loyalty_id`、`gigya_id`或您在Identity Service中定义的任何自定义标识）。
- 这些命名空间可以像全局命名空间一样分配给`kevel_user_key1`、`kevel_user_key2`或`kevel_user_key3`。
- [!DNL Kevel]将为每个映射的标识&#x200B;**的每个实例生成**&#x200B;一个UserDB记录，从而允许您在广告决策时实时匹配系统发送的每个标识。

### 身份映射行为

- 您最多可以将&#x200B;**个三个**&#x200B;个Experience Platform标识命名空间映射到[!DNL Kevel]的三个标识插槽。
- 对于每个激活的配置文件，[!DNL Kevel]将接收每个映射标识&#x200B;**的每个实例的**&#x200B;一个UserDB记录。
- 客户应仅将其实际发送的广告请求标识映射到[!DNL Kevel]，以避免不必要的UserDB存储。

Kevel目标![的](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)映射示例

## 支持的受众 {#supported-audiences}

| 受众来源 | 支持 | 描述 |
|-----------------------|-----------|---------------------------------------------------------- |
| Segmentation Service | 是 | 分段引擎评估的Adobe配置文件受众。 |
| 自定义上传 | 否 | 目前不支持。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

| 项目 | 类型 | 注释 |
|------|------|-------|
| 导出类型 | **区段导出** | 每当配置文件符合或退出受众时，[!DNL Kevel]都会收到更新。 |
| 导出频率 | **正在流式传输** | 使用Destination SDK流框架实时发送更新。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

按照标准Experience Platform [连接目标](../../ui/connect-destination.md)工作流。

>[!IMPORTANT]
> 
>您必须具有&#x200B;**查看目标**&#x200B;和&#x200B;**管理目标**&#x200B;权限。

### 验证目标 {#authenticate}

连接到[!DNL Kevel]时，请提供以下字段：

- **持有者令牌** — 您的[!DNL Kevel] API密钥。

Kevel目标的![身份验证选项](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### 填写目标详细信息 {#destination-details}

身份验证后，配置：

- **名称** — 用于标识此目标实例的标签。
- **描述** — 描述此目标实例的可选文本。
- **[!DNL Kevel]网络ID** — 您的[!DNL Kevel]网络标识符。

Kevel目标的![目标详细信息](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)

## 将区段激活到此目标 {#activate}

要将受众发送到[!DNL Kevel]，请遵循中的工作流\
[将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 停用受众 {#deactivate}

当在Experience Platform中停用受众或从[!DNL Kevel]目标中删除受众时，Experience Platform停止为该受众发送进一步的配置文件资格更新。 在[!DNL Kevel]中创建的任何现有区段仍然可用，不会自动删除。

如果[!DNL Kevel]区段当前正用于活动的营销活动中，则[!DNL Kevel]可阻止删除以避免中断实时投放。 在这种情况下，Experience Platform中的停用会导致以下情况：

- Experience Platform数据流停止
- [!DNL Kevel]区段继续存在，并且可能一直附加到营销活动，直到手动移除或更新营销活动为止

要完全停止[!DNL Kevel]中的定位，请确保从[!DNL Kevel]的营销活动管理系统中的任何活动营销活动中移除该区段。

### 映射属性和身份 {#map}

[!DNL Kevel]需要：

- **身份命名空间** — 最多三个映射到[!DNL Kevel]身份插槽的身份命名空间。
- **区段成员资格** — 无需手动映射；Experience Platform会自动传递区段成员资格标识符和别名。

在激活期间，选择已为[!DNL Kevel]配置的身份命名空间。 每个标识将生成自己的UserDB更新调用。

## 导出的数据/验证数据导出 {#exported-data}

当配置文件符合或退出受众时，Experience Platform会向[!DNL Kevel]发送流式更新。

### [!DNL Kevel] UserDB收到的样本有效负载

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345
{
  "segments": [1723, 3344, 9988]
}
```

| 参数 | 描述 |
|-----------|-------------|
| **用户密钥** | 从映射的Adobe标识派生。 |
| **区段** | 对应于当前已实现配置文件的Adobe受众的[!DNL Kevel]区段ID集。 |

{style="table-layout:auto"}

### 导出期间使用的Experience Platform配置文件示例 {#sample-profile}

将受众激活到[!DNL Kevel]目标时，Experience Platform将包含&#x200B;**区段资格**&#x200B;和客户&#x200B;**映射的**&#x200B;身份的配置文件片段发送到[!DNL Kevel]的标识插槽。

以下是导出的配置文件的示例：

- 多个标识命名空间映射到`kevel_user_key1`、`kevel_user_key2`和`kevel_user_key3`
- `ups`命名空间中的单个激活区段

```json
{
  "segmentMembership": {
    "ups": {
      "9d161bbb-c785-474a-965b-7d7bc2adf879": {
        "status": "realized",
        "lastQualificationTime": "2025-12-10T21:43:38.541076Z"
      }
    }
  },
  "identityMap": {
    "kevel_user_key1": [
      {
        "id": "ECID-fN1zo"
      },
      {
        "id": "ECID-9Xr2p"
      }
    ],
    "kevel_user_key2": [
      {
        "id": "GAID-4oic4"
      }
    ],
    "kevel_user_key3": [
      {
        "id": "IDFA-nB5fU"
      }
    ]
  }
}
```

#### [!DNL Kevel]如何解释此配置文件

使用[!DNL Kevel]目标配置，每个映射的标识都会生成一个不同的UserDB记录，这意味着[!DNL Kevel]将接收：

- `ECID-fN1zo`的一次更新
- `ECID-9Xr2p`的一次更新
- `GAID-4oic4`的一次更新
- `IDFA-nB5fU`的一次更新

这允许使用任意可用身份在广告决策时识别同一人员，每个身份具有一组相同的区段成员资格。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

- [[!DNL Kevel] UserDB引用](https://dev.kevel.com/reference/userdb)
- [[!DNL Kevel] 用户区段定位](https://dev.kevel.com/docs/segment-targeting)
