---
title: Identity Service的护栏（使用删除逻辑）
description: 了解Identity Service的护栏。
hide: true
hidefromtoc: true
source-git-commit: db8edbbc3ea5d8fcec3de95b9a37387bea493693
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 2%

---

# 护栏 [!DNL Identity Service] 数据（具有删除逻辑）

本文档提供了有关以下各项的使用和速率限制的信息： [!DNL Identity Service] 数据，以帮助您优化身份图的使用。 查看以下护栏时，假定您已正确建模数据。 如果您对如何建立数据模型有疑问，请联系您的客户服务代表。

## 快速入门

以下Experience Platform服务与身份数据建模有关：

* [身份](home.md)：在身份被摄取到Platform中时桥接来自不同数据源的身份。
* [[!DNL Real-Time Customer Profile]](../profile/home.md)：使用来自多个源的数据创建统一的使用者配置文件。

## 数据模型限制

下表提供了有关静态限制的护栏以及要考虑用于身份命名空间的验证规则的指南。

### 静态限制

下表概述了应用于身份数据的静态限制。

| 护栏 | 限制 | 注释 |
| --- | --- | --- |
| 图形中的身份数 [!BADGE 测试版]{type=Informative} | 50 | 更新具有50个链接身份的图形时，Identity Service将应用“先进先出”机制并删除最早的身份，为最新身份腾出空间。 删除基于身份类型和时间戳。 该限制在沙盒级别应用。 阅读 [附录](#appendix) 有关Identity服务如何在达到限制后删除身份的详细信息。 |
| XDM记录中的标识数 | 20 | 所需的XDM记录的最小数量为2。 |
| 自定义命名空间的数量 | None | 可创建的自定义命名空间数量没有限制。 |
| 图表数量 | None | 可创建的标识图的数量没有限制。 |
| 命名空间显示名称或身份符号的字符数 | None | 命名空间显示名称或身份符号的字符数没有限制。 |

### 身份值验证

下表概述了必须遵循的现有规则，以确保成功验证标识值。

| 命名空间 | 验证规则 | 违反规则时的系统行为 |
| --- | --- | --- |
| ECID | <ul><li>ECID的标识值必须刚好38个字符。</li><li>ECID的标识值必须仅由数字组成。</li></ul> | <ul><li>如果ECID的标识值不完全为38个字符，则会跳过该记录。</li><li>如果ECID的标识值包含非数字字符，则会跳过记录。</li></ul> |
| 非ECID | 标识值不能超过1024个字符。 | 如果标识值超过1024个字符，则会跳过该记录。 |

### 身份命名空间摄取

从2023年3月31日开始，Identity Service将阻止为新客户摄取Adobe Analytics ID (AAID)。 此身份通常通过 [Adobe Analytics源](../sources/connectors/adobe-applications/analytics.md) 和 [Adobe Audience Manager源](../sources//connectors/adobe-applications/audience-manager.md) 和是多余的，因为ECID表示相同的Web浏览器。 如果要更改此默认配置，请联系您的Adobe客户团队。

## 后续步骤

有关以下内容的更多信息，请参阅以下文档 [!DNL Identity Service]：

* [[!DNL Identity Service] 概述](home.md)
* [身份图查看器](ui/identity-graph-viewer.md)

## 附录 {#appendix}

以下部分包含有关Identity Service护栏的其他信息。

### [!BADGE 测试版]{type=Informational}了解在容量身份图形更新时的删除逻辑 {#deletion-logic}

更新完整的身份图后，Identity Service会先删除图中最旧的身份，然后再添加最新的身份。 这是为了保持身份数据的准确性和相关性。 此删除过程遵循两个主要规则：

#### 删除规则#1根据命名空间的身份类型确定优先顺序

删除优先级如下：

1. Cookie ID
2. 设备ID
3. 跨设备ID、电子邮件和电话

#### 删除规则#2基于存储在身份上的时间戳

图形中链接的每个标识都有其自己的相应时间戳。 更新完整图形时，Identity Service会删除具有最旧时间戳的标识。

当更新了具有新标识的完整图形时，这两个规则协同工作以指定将删除哪个旧标识。 Identity Service会先删除最早的Cookie ID，然后删除最旧的设备ID，最后删除最旧的跨设备ID/电子邮件/电话。

>[!NOTE]
>
>如果指定要删除的标识链接到图形中的多个其他标识，则连接该标识的链接也将被删除。

在下面的示例中，在可以使用新标识更新左侧的图形之前，Identity Service必须首先删除具有最旧时间戳的现有标识。 但是，由于最早的标识是设备ID，因此Identity Service会跳过该标识，直到到达删除优先级列表中具有更高类型的命名空间（在本例中为） `ecid-3`. 一旦删除了具有更高删除优先级类型的最旧身份，该图形就会更新为新链接， `ecid-51`.

>[!NOTE]
>
>在极少数情况下，两个身份具有相同的时间戳和身份类型，Identity Service将根据XID对ID进行排序并进行删除。

![为容纳最新标识而删除的最旧标识的示例](./images/graph-limits-v3.png)