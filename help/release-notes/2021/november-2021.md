---
title: Adobe Experience Platform发行说明2021年11月
description: Adobe Experience Platform 2021年11月版发行说明。
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 12%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 11 月 17 日**

## 新增功能

Adobe Experience Platform中的新增功能：

- [Real-Time Customer Data Platform B2B 版](#B2B)
- [（测试版）通过临时激活API将受众区段激活到批量目标](#ad-hoc-activation)

## 现有功能的更新

Adobe Experience Platform 现有功能的更新包括：

- [归因人工智能](#attribution-ai)
- [客户人工智能](#customer-ai)

### Real-Time Customer Data Platform B2B 版 {#B2B}

**发行日期：2021 年 11 月 12 日**

Real-Time CDP B2B版构建于Real-time Customer Data Platform (Real-Time CDP)之上，专为以B2B服务模式运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其合并到人员和帐户配置文件的单一视图中。 此统一数据允许营销人员准确地定位特定受众，并在所有可用渠道中吸引这些受众。

多项Adobe Experience Platform功能都得到了改进，从而将Real-Time CDP B2B版本与其对应的B2C版本区分开来。 这些改进包括改进了用于B2B用例的Experience Data Model (XDM)，升级了身份解析和用户档案分段，以及自定义构建的连接器和用于Marketo Engage的目标。 Marketo连接器允许B2B品牌将其行业领先的B2B参与数据与行为信息连接起来，以培育潜在客户并加强基于帐户的营销操作。

-[新的B2B和B2P版本](#editions)
-[新的Marketo数据源和目标连接器](#marketo)
-[标准B2B XDM](#XDM)

### 新的B2B和B2P版本 {#editions}

现已推出新的B2B和B2P版本，这些版本为Real-Time CDP和Platform Activation产品都提供了B2B数据和功能，可供您购买。

要了解有关Real-Time CDP B2B版本的更多信息，请参阅 [概述](../../rtcdp/overview.md).

### 新的Marketo数据源和目标连接器 {#marketo}

新的Marketo数据源和目标连接器可将Marketo数据流式传输到Platform和Platform受众，然后返回到Marketo。 适用于所有Platform用户。

| 功能 | 描述 |
|----------|-------------|
| Marketo Engage源连接器 | 此 [Marketo Engage源连接器](../../sources/connectors/adobe-applications/marketo/marketo.md) 允许营销人员将数据从一个或多个Marketo实例无缝地摄取到其Adobe Experience Platform实例中，并为商机管理和B2B营销人员提供了完整的解决方案。 |
| Marketo Engage目标 | 此 [Marketo目标](../../destinations/catalog/adobe/marketo-engage.md) 允许营销人员将在Adobe Experience Platform中创建的区段推送到Marketo，并在其中显示为静态列表。 |

### 标准B2B XDM {#XDM}

标准B2B XDM类、字段组和数据类型适用于所有Platform用户。

| 功能 | 描述 |
|-----------|--------------|
| 标准B2B XDM类 | Real-time Customer Data Platform B2B版本提供了多个标准XDM，用于捕获有关基本B2B数据实体（如客户、机会、营销活动等）的详细信息。 |

请参阅 [Real-time Customer Data Platform B2B版本中的架构](../../rtcdp/schemas/b2b.md) 文档，了解有关捕获B2B数据实体的更多信息。

### （测试版）通过临时激活API将受众区段激活到批量目标 {#ad-hoc-activation}

通过临时激活API，营销人员可以快速高效地以编程方式将受众区段激活到目标，以满足立即激活的需求。 仅支持临时受众激活 [基于文件的批处理目标](../../destinations/destination-types.md#file-based) 目前处于测试阶段。 欲了解更多信息，请参见 [临时激活API文档](../../destinations/api/ad-hoc-activation-api.md).

### 归因人工智能 {#attribution-ai}

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

| 功能 | 描述 |
|-----------|---------------|
| 支持多个数据集 | 现在，Attribution AI可以直接在UI中轻松摄取多个数据集，而无需映射和拼合每个数据集。 这一新的省时功能通过来自多个数据集的更丰富数据提供了更强大且更准确的分数。 |
| 媒体渠道和营销活动字段映射 | Attribution AI现在支持媒体渠道和营销活动字段的映射。 数据集之间的媒体渠道映射可改进从Attribution AI推导出的见解，并帮助提供更清晰、易于解释的结果。 |

欲知有关Attribution AI的更多信息，请参见 [Attribution AI文档](../../intelligent-services/attribution-ai/overview.md).

### 客户人工智能 {#customer-ai}

Real-time Customer Data Platform中提供的客户人工智能，用于生成自定义倾向分数，例如大规模单个用户档案的流失和转化率。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

**更新的功能**

| 功能 | 描述 |
|-----------|-------------|
| 支持多个数据集 | 客户人工智能现在可以轻松地直接在UI中摄取多个数据集，而无需映射和拼合每个数据集。 这一新的省时功能通过来自多个数据集的更丰富数据提供了更强大且更准确的分数。 |
| 自定义配置文件属性 | 除了标准事件字段外，客户人工智能现在还支持在数据中定义自定义用户档案数据集字段（带有时间戳）。 利用此选项，可添加您认为有影响力的其他配置文件属性，这些配置文件属性可提高模型的质量并提供更准确的结果。 |

有关客户人工智能的更多信息，请参阅 [客户人工智能文档](../../intelligent-services/customer-ai/overview.md).
