---
keywords: Experience Platform；身份；身份服务；故障诊断；护栏；准则；限制；
title: Identity服务的防护
description: 本文档提供了有关Identity Service数据的使用和费率限制的信息，以帮助您优化对身份图的使用。
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 2%

---

# 的护栏 [!DNL Identity Service] 数据

本文档提供了有关 [!DNL Identity Service] 数据，帮助您优化对身份图的使用。 在查看以下护栏时，我们假定您已正确建模数据。 如果您对如何建立数据模型有任何疑问，请联系您的客户服务代表。

## 快速入门

以下Experience Platform服务与对身份数据进行建模有关：

* [标识](home.md):在将不同数据源摄取到平台时，将它们的身份桥接起来。
* [[!DNL Real-Time Customer Profile]](../profile/home.md):使用来自多个来源的数据创建统一的消费者用户档案。

## 数据模型限制

下表提供了静态限制的防护以及身份命名空间需要考虑的验证规则。

### 静态限制

下表概述了对身份数据应用的静态限制。

| 瓜德拉伊 | 限制 | 注释 |
| --- | --- | --- |
| 图中的标识数 | 150 | 该限制在沙盒级别应用。 达到限制后，将不会更新标识图。 **注意**:标识图中的最大标识数 **（对于单个合并的用户档案）** 是50。 基于身份图且身份超过50个的合并配置文件将从实时客户配置文件中排除。 有关更多信息，请阅读 [配置文件数据的防护](../profile/guardrails.md). |
| XDM记录中的身份数 | 20 | 所需的XDM记录最少为2个。 |
| 自定义命名空间的数量 | None | 您可以创建的自定义命名空间数量没有限制。 |
| 图数 | None | 您可以创建的身份图的数量没有限制。 |
| 命名空间显示名称或身份符号的字符数 | None | 命名空间显示名称或身份符号的字符数没有限制。 |

### 身份值验证

下表概述了为了确保身份值成功验证必须遵循的现有规则。

| 命名空间 | 验证规则 | 违反规则时的系统行为 |
| --- | --- | --- |
| ECID | <ul><li>ECID的标识值必须恰好为38个字符。</li><li>ECID的标识值只能由数字组成。</li></ul> | <ul><li>如果ECID的标识值不完全为38个字符，则会跳过该记录。</li><li>如果ECID的标识值包含非数字字符，则会跳过该记录。</li></ul> |
| 非ECID | 标识值不能超过1024个字符。 | 如果标识值超过1024个字符，则会跳过该记录。 |

### 身份命名空间摄取

自2023年1月31日起，Identity Service将阻止为新客户摄取Adobe Analytics ID(AAID)。 此标识通常通过 [Adobe Analytics源](../sources/connectors/adobe-applications/analytics.md) 和 [Adobe Audience Manager源](../sources//connectors/adobe-applications/audience-manager.md) 和冗余，因为ECID表示相同的Web浏览器。 如果要更改此默认配置，请联系您的客户经理。

## 后续步骤

有关 [!DNL Identity Service]:

* [[!DNL Identity Service] 概述](home.md)
* [身份图查看器](ui/identity-graph-viewer.md)
