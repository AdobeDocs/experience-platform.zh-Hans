---
title: Real-Time CDP B2B edition的架构升级
description: 请阅读本文档，了解对Real-Time CDP B2B edition的全面架构升级。
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: d958a947-e195-4dd4-a04c-63ad82829728
source-git-commit: a48196d369cec9e9927d9320475e06457e575691
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 1%

---

# 架构升级到Real-Time CDP B2B edition

>[!IMPORTANT]
>
>本文档概述了Real-Time CDP B2B和B2P版本的架构升级。 升级不需要大多数客户执行任何操作。 但是，有些受众无法自动升级。 Adobe将直接与您合作来应对这些场景。 有关升级将对Adobe Experience Platform现有功能有何影响的信息，请参阅本文档。 如果您有任何问题，请联系您的Adobe客户团队。

Adobe重新设计了Real-Time CDP B2B和B2P版本，以增强可扩展性、性能和可靠性，同时还支持更高级的B2B用例。 为确保所有客户都能从这些改进中受益，Adobe将把所有现有的B2B和B2P客户升级到新架构。

使用增强型架构具有以下优势：

* **数据摄取的可扩展性**：改进了对高基数B2B关系的支持，例如与数千人连接的帐户。
* **性能和可靠的受众评估**：针对复杂的B2B受众进行更快、更灵活的分段。
* **实体解析**：增强了B2B实体的标识解析，提高了数据质量，减少了重复，以实现更准确的分段和聚合。

## 新增功能

请阅读以下内容，了解体系结构升级中包含的关键增强功能。

### 受众会员资格的帐户快照

在新的B2B架构中，受众成员资格详细信息现在包含在快照导出中的帐户实体。 通过此功能，可访问帐户级别的受众状态、时间戳和成员资格指标。

通过此升级，您现在可以：

* 使营销和运营团队可直接验证帐户受众成员资格。
* 实现用户档案（人员）和帐户分段模型之间的功能对等性，确保跨实体的一致体验。

有关详细信息，请阅读有关[帐户受众](../segmentation/types/account-audiences.md)的文档。

### 包含B2B实体的受众受众规模

现在，可以精确计算具有B2B实体的受众的估计受众规模。 这些估计值可在预览期间使用，并为涉及复杂B2B关系的受众提供更准确和可靠的见解。

通过此升级，您现在可以：

* 在受众创建过程中，利用精确的受众规模估计值提供的见解来改进规划和决策。
* 自信地设计复杂的B2B受众，并了解更准确的受众估计。
* 支持更智能的活动规划、更精确的定位和更好的资源分配。

有关详细信息，请阅读有关[帐户受众](../segmentation/types/account-audiences.md)的文档。

## 升级到现有功能

在B2B架构升级过程中，更新了以下功能。

### 更新了具有B2B属性和体验事件的多实体受众

作为新架构升级的一部分，体验事件过滤器不能再用于包含B2B属性的单个多实体受众。

要获得相同的受众逻辑，您可以使用区段生成器[添加受众和引用受众](../segmentation/ui/segment-builder.md#adding-audiences)

例如：

* 创建体验事件受众
   * 单独定义行为条件。 例如：“过去三天访问定价页面的用户。”
* 创建具有B2B属性的多实体受众。
   * 在此，您可以引用体验事件受众作为此受众标准的一部分。 例如：“作为客户属于&#x200B;**&#39;财务&#39;**&#x200B;行业的任何机会的&#x200B;**&#39;决策者&#39;**&#x200B;的人员，以及过去三天访问定价页面的受众成员。

升级完成后，必须使用[segment-of-segment](../segmentation/methods/edge-segmentation.md#edge-segmentation-query-types)方法创建任何具有B2B属性和体验事件的新多实体受众。

>[!TIP]
>
>区段&#x200B;**的**&#x200B;区段是包含一个或多个批次或边缘区段的任意区段定义。 **注意**：如果您使用区段区段，则配置文件取消资格将&#x200B;**每24小时发生一次**。

### B2B受众中的实体分辨率和时间优先级合并

作为架构升级的一部分，Adobe将推出针对“客户”和“机会”的实体解决方案。 实体解析基于确定性ID匹配和基于最新数据。 实体解析作业在批量分段期间每天运行，然后再评估具有B2B属性的多实体受众。

>[!BEGINSHADEBOX]

#### 实体解析如何工作？

* **在**&#x200B;之前：如果将数据通用编号系统(DUNS)编号用作附加标识，并且在源系统（如CRM）中更新了帐户的DUNS编号，则帐户ID将同时链接到旧和新的DUNS编号。
* **After**：如果将DUNS编号用作附加标识，并且在源系统（如CRM）中更新了帐户的DUNS编号，则帐户ID将仅链接到新的DUNS编号，从而更准确地反映帐户的当前状态。

>[!ENDSHADEBOX]

通过此升级，您现在可以：

* 每日实体解析作业完成后，使用[!DNL Profile Access] API查看最新的合并配置文件。
* 利用客户数据和商机数据改进的准确性和一致性，进行分段、激活和分析。

有关详细信息，请阅读[[!DNL Profile Access] API](../profile/api/entities.md)。

### 在多实体B2B受众中支持合并策略

具有B2B属性的多实体受众现在支持单个合并策略（即您配置的默认合并策略），而不是多个合并策略。

有关详细信息，请参阅Real-Time CDP B2B edition[的](./segmentation/b2b.md)分段用例指南。

### 在[!DNL Profile Access] API中弃用B2B实体查找和删除

使用[!DNL Profile Access] API的B2B实体的以下查找功能已被弃用：

* 帐户 — 人员关系
* 机会 — 人员关系
* 促销活动
* 营销活动成员
* 营销列表
* 营销列表成员

使用[!DNL Profile Access] API删除以下B2B实体的请求已被弃用：

* 帐户
* 帐户 — 人员关系
* 机会
* 机会 — 人员关系
* 促销活动
* 营销活动成员
* 营销列表
* 营销列表成员

有关详细信息，请阅读[[!DNL Profile Access] API](../profile/api/entities.md)。

### 弃用区段作业API

在新架构下，*不支持“创建区段作业”端点和灵活的受众评估。

### 帐户和机会配置文件查找

现在，只有在帐户和机会架构完成每日实体解析过程后，才能将其检索为查找维度实体。 新摄取的记录将不可用于配置文件扩充或区段定义，直到下一个实体解析周期完成（通常每24小时一次）为止。

<!-- ### Deprecation of audience creation via API for B2B entities

Creation of audiences using B2B entities via API is being deprecated. The list of affected B2B entities include:

* Account
* Opportunity
* Account-Person Relation
* Opportunity-Person Relation
* Campaign
* Campaign Member
* Marketing List
* Marketing List Member

Read the [segment definitions endpoint API guide](../segmentation/api/segment-definitions.md) for more information. -->

### 对沙盒工具中的多实体受众导入的更改

在架构升级后，如果在升级之前发布了包含这些受众的包，您将无法再导入具有B2B属性和体验事件的多实体受众。 这些受众将无法导入，且无法自动转换为新架构。 要解决此限制，您必须创建一个具有更新受众的新包，然后使用沙盒工具将它们导入各自的目标沙盒中。

开发沙盒将升级到新架构。 可以自动更新的受众将升级；无法禁用的受众将升级。 升级后必须重新创建禁用的受众。

有关详细信息，请阅读[沙盒工具指南](../sandboxes/ui/sandbox-tooling.md)。
