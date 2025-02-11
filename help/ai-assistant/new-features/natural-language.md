---
title: AI辅助的自然语言估计
description: 了解如何使用AI Assistant的自然语言估计功能。
badge: Alpha
source-git-commit: aef3be05ca23abe9ed8275aa562fdd3313a7e2d0
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# 使用AI助理进行自然语言估计

>[!AVAILABILITY]
>
>此功能已Alpha，可能不可用于您的组织。 要参与Alpha计划并访问此功能，请联系您的Adobe客户团队。

您可以使用Adobe Experience Platform AI Assistant的自然语言估计功能，根据简单的对话问题估计受众规模并预测受众倾向。 利用此功能，您可以使受众分析更易于访问和直观。 这对于您的业务和营销运营用例特别有用，尤其是在您每天管理受众并依赖这些见解来制定有效营销策略的情况下。

借助AI Assistant的自然语言处理功能，您可以提出以下问题：“我在25到35岁的加利福尼亚有多少用户档案”或“我们有多少高价值客户？” 甚至“下个月内，我的受众中会购买多少百分比的商品？” 然后，AI Assistant解释这些问题并返回可用于做出基于数据的决策的估计值或倾向分数。

请阅读本文档，了解如何使用AI Assistant的自然语言估计功能。

## 关键术语和定义 {#key-terminology-and-definitions}

请参阅下表所列重要术语及其相应定义。

| 术语 | 定义 |
| --- | --- |
| 受众规模估计 | 根据定义的标准计算特定受众中的成员数的过程。 您可以根据配置文件数据（包括不在受众中的配置文件）估算大小。 此外，您还可以检索受众规模估计值，而无需首先创建受众。 利用这一洞察力，您可以了解针对性促销活动的覆盖范围。 |
| 倾向估计 | 预测受众中的成员在特定时间范围内表现出特定行为（例如：进行购买、流失）的可能性。 倾向估计特定于Real-time Customer Data Platform中的受众，但可以包括用户档案数据，包括任何受众中的用户档案。 在优化营销活动和管理受众保留策略时，您可以参考此见解。 |
| 自然语言处理 | AI Assistant能够解释和回答日常语言提出的问题，使您能够进行对话并接收相关见解，而无需使用技术查询。 |
| 预定义的时间范围 | AI Assistant支持的用于估计受众规模和倾向的标准时间范围（“上个月”、“未来30天”）。 **注意**：在Alpha阶段可能不完全支持自定义时间范围。 |
| 快照数据 | AI助手用于提供估算的数据集。 此数据每24-48小时从Real-time Customer Data Platform中更新一次，因此，分析可能不会反映实时受众更改。 |

{style="table-layout:auto"}

## 用例示例 {#use-case-examples}

AI Assistant的自然语言估计功能对于以下用例特别有用：

### 营销操作

作为营销运营专业人员，您的职责可能包括管理和监控受众数据，以确保数据与业务目标保持一致。 利用AI Assistant的自然语言估计功能，您可以快速收集有关受众规模和倾向性的见解，而无需先创建受众，也不必广泛具备数据分析知识。

帮助他们在其工作流中维护一致的数据驱动方法。

### 商业用户和营销人员

作为商业用户和营销人员，快速访问受众数据对于成功规划、定位和评估活动可能至关重要。 利用AI Assistant的自然语言估计功能，您可以简化受众信息的访问，提出简单的问题，并获得有助于受众创建和活动优化的可操作见解。

## 主要功能

>[!IMPORTANT]
>
>以下特性Alpha，并侧重于自然语言估计的基础功能。 由于此功能正在Alpha，您必须确保仔细检查您从AI Assistant收到的响应是否正确。

### 受众规模估计

您可以使用自然语言查询来要求AI助手估计特定受众的大小。 此功能对于评估目标受众的覆盖范围和影响特别有用。 例如，作为营销策划，您可以提出以下问题：

* “纽约有多少个人资料？”
* “我有多少用户档案通过电子邮件收发并同意发送？”

使用此功能可简化估计受众规模并获得即时答案的过程，而无需导航复杂的数据过滤器或区段定义。

### 受众倾向估计

>[!TIP]
>
>您的Experience Platform帐户必须配置[客户人工智能](../../intelligent-services/customer-ai/overview.md)，才能使用AI助理的倾向估计功能。

您可以使用受众倾向估计来识别受众中特定行为或操作的可能性。 例如，您可以提出以下问题：

* “我当前受众中有多少百分比可能在下个月购买？”
* “我有多少具有高度转化倾向的用户档案？”

通过询问自然语言问题，您可以检索表示受众成员展示特定行为的百分比或可能性的倾向分数，从而帮助您主动调整促销活动或保留策略。

## 受众规模和倾向估计的示例问题

以下是您可以向AI Assistant询问的示例问题，以帮助您了解受众规模和行为倾向：

### 受众规模估计

* “我的电子邮件或手机号码有多少个用户档案？”
* “我在纽约有多少个人资料？”
* “我的客户居住的前5个州是哪个？”

### 受众倾向估计

* “下个月内，我的受众中可能购买产品的比例是多少？”
* “预计下一季度会有多少客户转产？”

您可以使用自然语言查询提供的灵活性，快速了解受众动态，而无需技术专业知识。

## 常见问题解答

阅读本节内容，了解有关使用AI助手进行自然语言估计的常见问题解答。

### AI Assistant刷新受众数据的频率如何？

AI助手的数据每24-48小时刷新一次。 因此，估计数可能反映稍有延误。 这意味着当您询问“当前”数据时，响应将反映最新的快照，该快照可能长达48小时。

### 我可以通过自定义日期范围询问受众规模或倾向吗？

目前，AI助手支持预定义的日期范围，例如“上个月”或“未来30天”。 Alpha阶段不完全支持这些预定义选项之外的自定义日期范围。 如果请求自定义时间范围，AI助手将根据最接近的可用时间范围提供见解。

### AI Assistant如何计算倾向分数？

倾向分数是使用[客户人工智能](../../intelligent-services/customer-ai/overview.md)计算的。 AI Assistant使用机器学习模型来预测特定受众行为在请求时间范围内的可能性，例如购买和流失。 在Alpha阶段，AI Assistant中的倾向分数计算不使用体验事件或行为数据。

### AI Assistant是否会根据实时数据估算受众规模或倾向？

不，实时数据目前不可用。 估算基于最近的数据快照，每24-48小时更新一次。 在Alpha阶段，实时更新不在范围之内。

### 如何计算倾向性？

AI Assistant依赖客户人工智能模型来回答任何可能性或倾向分数。

## 超出范围的功能

当前不支持以下功能：

### 基于行为数据事件的受众规模估计

AI助手当前无法回答基于行为数据的问题，例如&#x200B;**“过去30天内有多少用户将产品添加到购物车”**。 但是，您可以在Real-Time CDP中创建计算属性，以预先计算此类值。 然后，这些计算属性可在AI Assistant中使用。 有关详细信息，请阅读有关[计算属性](../../profile/computed-attributes/overview.md)的文档。

### 实时数据更新

AI助理提供的估计是基于最近的数据快照，而不是实时数据快照。 数据每24-48小时刷新一次，因此见解可反映此延迟。 此限制意味着，如果区段或数据集在短时间内发生显着变化，用户将无法收到即时更新。