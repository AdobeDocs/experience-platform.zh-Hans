---
title: Adobe Experience Platform发行说明2021年11月
description: 2021年11月版Adobe Experience Platform发行说明。
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 12%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 11 月 17 日**

## 新增功能

Adobe Experience Platform的新增功能：

- [Real-Time Customer Data Platform B2B 版](#B2B)
- [（测试版）通过临时激活API将受众区段激活到批量目标](#ad-hoc-activation)

## 现有功能的更新

Adobe Experience Platform 现有功能的更新包括：

- [归因人工智能](#attribution-ai)
- [客户人工智能](#customer-ai)

### Real-Time Customer Data Platform B2B 版 {#B2B}

**发行日期：2021 年 11 月 12 日**

Real-Time CDP B2B Edition基于Real-time Customer Data Platform(Real-Time CDP)而构建，专为以企业对企业服务模式运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其整合为人员和帐户配置文件的单一视图。 通过这种统一的数据，营销人员可以准确定位特定受众并在所有可用渠道中吸引这些受众。

Real-Time CDP B2B Edition与其B2C版本相比，Adobe Experience Platform的各种功能都有所改进。 这些功能包括对B2B用例的体验数据模型(XDM)进行了改进、对身份分辨率和配置文件分段进行了升级，以及自定义的连接器和Marketo Engage目标。 Marketo连接器允许B2B品牌将其行业领先的B2B参与数据与行为信息连接起来，以培养潜在客户并增强基于帐户的营销操作。

-[新的B2B和B2P版本](#editions)
-[新的Marketo数据源和目标连接器](#marketo)
-[标准B2B XDM](#XDM)

### 新的B2B和B2P版本 {#editions}

可购买为Real-Time CDP和平台激活产品带来B2B数据和功能的新B2B和B2P版本。

要了解有关Real-Time CDP B2B Edition的更多信息，请参阅 [概述](../../rtcdp/overview.md).

### 新的Marketo数据源和目标连接器 {#marketo}

新的Marketo数据源和目标连接器将Marketo数据流式传输到平台受众和平台受众，并返回到Marketo。 适用于所有平台用户。

| 功能 | 描述 |
|----------|-------------|
| Marketo Engage源连接器 | 的 [Marketo Engage源连接器](../../sources/connectors/adobe-applications/marketo/marketo.md) 允许营销人员将一个或多个Marketo实例的数据无缝摄取到其Adobe Experience Platform实例中，并为潜在客户管理和B2B营销人员提供完整的解决方案。 |
| Marketo Engage目标 | 的 [Marketo目标](../../destinations/catalog/adobe/marketo-engage.md) 允许营销人员将在Adobe Experience Platform中创建的区段推送到Marketo，以将其显示为静态列表。 |

### 标准B2B XDM {#XDM}

标准B2B XDM类、字段组和数据类型可供所有Platform用户使用。

| 功能 | 描述 |
|-----------|--------------|
| 标准B2B XDM类 | Real-time Customer Data Platform B2B Edition提供了多个标准XDM，用于捕获有关基本B2B数据实体（如帐户、机会、营销活动等）的详细信息。 |

请参阅 [Real-time Customer Data Platform B2B版中的模式](../../rtcdp/schemas/b2b.md) 文档，了解有关捕获B2B数据实体的更多信息。

### （测试版）通过临时激活API将受众区段激活到批量目标 {#ad-hoc-activation}

临时激活API允许营销人员以编程方式快速高效地将受众区段激活到目标，以应对需要立即激活的情况。 Ad-hoc audience激活仅受 [批量基于文件的目标](../../destinations/destination-types.md#file-based) 和目前处于测试阶段。 有关更多信息，请参阅 [临时激活API文档](../../destinations/api/ad-hoc-activation-api.md).

### 归因人工智能 {#attribution-ai}

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

| 功能 | 描述 |
|-----------|---------------|
| 支持多个数据集 | Attribution AI现在可以轻松地直接在UI中摄取多个数据集，而无需映射和拼合每个数据集。 这一新的省时功能通过来自多个数据集的更丰富数据，提供了更强大、更准确的分数。 |
| 媒体渠道和促销活动字段映射 | Attribution AI现在支持媒体渠道和营销活动字段的映射。 数据集之间的媒体渠道映射可改进从Attribution AI派生的分析，并有助于提供更清晰、易于解读的结果。 |

有关Attribution AI的更多信息，请参阅 [Attribution AI文档](../../intelligent-services/attribution-ai/overview.md).

### 客户人工智能 {#customer-ai}

Real-time Customer Data Platform中提供的Customer AI用于生成自定义倾向得分，例如大规模单个用户档案的流失率和转化。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

**更新功能**

| 功能 | 描述 |
|-----------|-------------|
| 支持多个数据集 | Customer AI现在可以轻松地直接在UI中摄取多个数据集，而无需映射和拼合每个数据集。 这一新的省时功能通过来自多个数据集的更丰富数据，提供了更强大、更准确的分数。 |
| 自定义配置文件属性 | 除标准事件字段外，Customer AI现在还支持在您的数据中定义自定义用户档案数据集字段（带有时间戳）。 通过使用此选项，您可以添加其他您认为具有影响力的配置文件属性，这些属性可能会提高模型质量并提供更准确的结果。 |

有关Customer AI的更多信息，请参阅 [客户AI文档](../../intelligent-services/customer-ai/overview.md).
