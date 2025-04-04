---
title: Adobe Experience Platform 发行说明（2021 年 11 月）
description: Adobe Experience Platform 2021 年 11 月发行说明。
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 23%

---

# Adobe Experience Platform 发行说明

**发行日期： 2021年11月17日**

## 新增功能

Adobe Experience Platform 的新功能：

- [Real-Time Customer Data Platform B2B 版](#B2B)
- [(Beta)通过临时激活API将受众区段激活到批处理目标](#ad-hoc-activation)

## 现有功能的更新

Adobe Experience Platform 中现有功能的更新：

- [归因人工智能](#attribution-ai)
- [客户人工智能](#customer-ai)

### Real-Time Customer Data Platform B2B 版 {#B2B}

**发行日期： 2021年11月12日**

Real-Time CDP B2B 版本基于 Real-Time Customer Data Platform (Real-Time CDP) 构建，专为采用业务对业务服务模式运营的营销人员而构建。它将来自多个来源的数据汇集在一起&#x200B;，并将其组合成人员和帐户轮廓的单一视图。这种统一的数据使营销人员能够精确锁定特定受众，并通过所有可用渠道吸引这些受众。

Adobe Experience Platform的各项功能都有改进，可将Real-Time CDP B2B edition与其B2C对应功能区分开来。 其中包括改进用于B2B用例的体验数据模型(XDM)、升级身份解析和用户档案分段，以及适用于Marketo Engage的自定义连接器和目标。 Marketo连接器允许B2B品牌将其行业领先的B2B参与数据与行为信息连接起来，以培育潜在客户并加强基于帐户的营销运营。

-[新的B2B和B2P版本](#editions)
-[新的Marketo数据源和目标连接器](#marketo)
-[标准B2B XDM](#XDM)

### 新的B2B和B2P版本 {#editions}

现已推出新的B2B和B2P版本，这些版本将B2B数据和功能引入Real-Time CDP和Experience Platform激活产品，可供您购买。

要进一步了解Real-Time CDP B2B edition，请参阅[概述](../../rtcdp/overview.md)。

### 新的Marketo数据源和目标连接器 {#marketo}

新的Marketo数据源和目标连接器可将Marketo数据流式传输到Experience Platform，并将Experience Platform受众返回到Marketo。 适用于所有Experience Platform用户。

| 功能 | 描述 |
|----------|-------------|
| Marketo Engage源连接器 | [Marketo Engage源连接器](../../sources/connectors/adobe-applications/marketo/marketo.md)允许营销人员从一个或多个Marketo实例中无缝地摄取数据到其Adobe Experience Platform实例，并为潜在客户管理和B2B营销人员提供完整的解决方案。 |
| Marketo Engage目标 | [Marketo目标](../../destinations/catalog/adobe/marketo-engage.md)允许营销人员将在Adobe Experience Platform中创建的区段推送到Marketo，并在其中显示为静态列表。 |

### 标准B2B XDM {#XDM}

标准B2B XDM类、字段组和数据类型适用于所有Experience Platform用户。

| 功能 | 描述 |
|-----------|--------------|
| 标准B2B XDM类 | Real-Time Customer Data Platform B2B edition提供了多个标准XDM，可捕获有关基本B2B数据实体（如帐户、机会、营销活动等）的详细信息。 |

请参阅Real-Time Customer Data Platform B2B edition中的[架构](../../rtcdp/schemas/b2b.md)文档，了解有关捕获B2B数据实体的更多信息。

### (Beta)通过临时激活API将受众区段激活到批处理目标 {#ad-hoc-activation}

通过临时激活API，营销人员可以快速高效地以编程方式将受众区段激活到目标，以满足立即激活的需求。 仅基于[批处理文件的目标](../../destinations/destination-types.md#file-based)支持临时受众激活，该受众激活当前处于测试阶段。 有关详细信息，请参阅[临时激活API文档](../../destinations/api/ad-hoc-activation-api.md)。

### 归因人工智能 {#attribution-ai}

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户历程中每个营销接触点的营销影响。

| 功能 | 描述 |
|-----------|---------------|
| 支持多个数据集 | 归因人工智能现在可以轻松地直接在UI中摄取多个数据集，而无需映射和拼合每个数据集。 这项新的省时功能通过来自多个数据集的更丰富数据提供了更强大且更准确的分数。 |
| 媒体渠道和营销活动字段映射 | Attribution AI现在支持映射媒体渠道和活动字段。 数据集之间的媒体渠道映射改进了从Attribution AI派生的见解，并帮助提供更清晰且易于解释的结果。 |

有关归因人工智能的更多信息，请参阅[归因人工智能文档](../../intelligent-services/attribution-ai/overview.md)。

### 客户人工智能 {#customer-ai}

Real-Time Customer Data Platform中提供的客户人工智能，用于生成自定义倾向分数，例如大规模单个用户档案的流失和转化率。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

**更新的功能**

| 功能 | 描述 |
|-----------|-------------|
| 支持多个数据集 | 客户人工智能现在可以直接在UI中轻松摄取多个数据集，而无需映射和拼合每个数据集。 这项新的省时功能通过来自多个数据集的更丰富数据提供了更强大且更准确的分数。 |
| 自定义配置文件属性 | 除了标准事件字段外，客户人工智能现在还支持在数据中定义自定义用户档案数据集字段（带有时间戳）。 使用此选项可添加您认为具有影响力的其他配置文件属性，这些配置文件属性可提高模型的质量并提供更准确的结果。 |

有关客户人工智能的更多信息，请参阅[客户人工智能文档](../../intelligent-services/customer-ai/overview.md)。
