---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据使用策略概述
topic: policies
translation-type: tm+mt
source-git-commit: d08f06b3c2bdb21e0f4935bbcb6f163892ab9842

---


# 数据使用策略概述

为了使数据使用标签能够有效支持数据合规性，必须实施数据使用策略。 数据使用策略是描述您允许或限制您对Experience Platform内的数据执行的营销操作类型的规则。

营销操作的一个示例可能是希望将数据集导出到第三方服务。 如果存在一项策略，指出无法导出特定类型的数据(如个人识别信息(PII))，且已将“I”标签（标识数据）应用于数据集，则您将收到来自策略服务的响应，通知您已违反数据使用策略。

## 如何创建和使用数据使用策略

应用数据使用标签后，数据管理者可以使用 [DULE Policy Service API创建策略](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。

作为数据管理者，您可以使用Policy Service API管理和评估与对包含DULE标签的数据采取的营销操作相关的策略。 使用API，您可以创建和更新策略，确定策略的状态，并使用营销操作来评估特定操作是否违反了数据使用策略。

在策略服务API中，所有策略和营销操作都称为或 `core` 资 `custom` 源。 `core` 资源由Adobe定义和维护，而资 `custom` 源由个别客户创建和维护。 因此， `custom` 这些资源是独一无二的，只对创建这些资源的组织而言是可见的。

有关执行DULE Policy Service API提供的关键操作的详细信息，请参阅“ [Policy Service Developer”指南](../api/getting-started.md)。 有关使用DULE策略的分步说明，请参阅有关创建和评估DULE策 [略的教程](create.md)。