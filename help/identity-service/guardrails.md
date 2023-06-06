---
keywords: Experience Platform；身份；身份服务；故障排除；护栏；指南；限制；
title: Identity Service的防护
description: 本文档提供了有关Identity Service数据的使用和速率限制的信息，以帮助您优化对身份图的使用。
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: 60bab17d2ecb2e68bf500aea2d68587a125b35bb
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 2%

---

# 护栏 [!DNL Identity Service] 数据

本文档提供了以下各项的使用和速率限制信息： [!DNL Identity Service] 数据，以帮助您优化身份图的使用。 查看以下护栏时，假定您已正确建模数据。 如果您对如何建立数据模型有疑问，请联系您的客户服务代表。

## 快速入门

以下Experience Platform服务涉及对身份数据进行建模：

* [身份](home.md)：将标识摄取到Platform中时桥接不同数据源中的标识。
* [[!DNL Real-Time Customer Profile]](../profile/home.md)：使用来自多个源的数据创建统一的使用者配置文件。

## 数据模型限制

下表提供了有关静态限制的护栏以及身份命名空间要考虑的验证规则的指南。

### 静态限制

下表概述了应用于身份数据的静态限制。

| 护栏 | 限制 | 注释 |
| --- | --- | --- |
| 图表中的身份数 | 150 | 该限制在沙盒级别应用。 一旦标识数达到150个或更多，则不会添加任何新标识，也不会更新标识图。 图形可能显示大于150的标识，这是链接一个或多个具有小于150的标识的图形的结果。 **注释**：标识图中的最大标识数 **对于单个合并的配置文件** 是50 Real-Time Customer Profile中排除了基于具有50多个标识的标识图的合并配置文件。 有关详细信息，请阅读以下指南： [配置文件数据的护栏](../profile/guardrails.md). |
| XDM记录中的标识数 | 20 | 需要的最小XDM记录数为2。 |
| 自定义命名空间的数量 | None | 您可以创建的自定义命名空间的数量没有限制。 |
| 图表数量 | None | 您可以创建的标识图的数量没有限制。 |
| 命名空间显示名称或身份符号的字符数 | None | 命名空间显示名称或身份符号的字符数没有限制。 |

### 身份值验证

下表概述了为确保成功验证标识值而必须遵循的现有规则。

| 命名空间 | 验证规则 | 违反规则时的系统行为 |
| --- | --- | --- |
| ECID | <ul><li>ECID的标识值必须刚好38个字符。</li><li>ECID的标识值必须仅由数字组成。</li></ul> | <ul><li>如果ECID的标识值不是38个字符，则会跳过该记录。</li><li>如果ECID的标识值包含非数字字符，则会跳过该记录。</li></ul> |
| 非ECID | 标识值不能超过1024个字符。 | 如果标识值超过1024个字符，则会跳过该记录。 |

### 身份命名空间摄取

从2023年3月31日开始，Identity Service将阻止为新客户摄取Adobe Analytics ID (AAID)。 此身份通常通过 [Adobe Analytics源](../sources/connectors/adobe-applications/analytics.md) 和 [Adobe Audience Manager源](../sources//connectors/adobe-applications/audience-manager.md) 和是多余的，因为ECID表示相同的Web浏览器。 如果要更改此默认配置，请联系您的Adobe客户团队。

## 后续步骤

有关以下内容的更多信息，请参阅以下文档 [!DNL Identity Service]：

* [[!DNL Identity Service] 概述](home.md)
* [身份图查看器](ui/identity-graph-viewer.md)
