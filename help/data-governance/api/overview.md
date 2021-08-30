---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 策略服务API指南
topic-legacy: developer guide
description: 策略服务API允许开发人员管理Experience Platform中的数据使用标签和策略。 请阅读本指南，了解如何使用API执行关键操作。
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# [!DNL Policy Service] API指南

Adobe Experience Platform [!DNL Data Governance]允许您管理客户数据，并确保符合适用于数据使用的法规、限制和策略。 它在[!DNL Experience Platform]的各个级别中发挥着关键作用，包括编目、数据谱系、数据使用标签、数据使用策略以及控制营销操作数据的使用。

[!DNL Policy Service] API提供了多个端点，允许您以编程方式管理数据使用标签和策略，以及评估违反策略的营销操作。 下面概述了这些端点。 有关详细信息，请访问各个端点指南，并参阅[快速入门指南](./getting-started.md) ，以了解有关所需标头、读取示例API调用等的重要信息。

要查看所有可用的端点和CRUD操作，请访问[[!DNL Policy Service] API swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/)。

## 标签

数据使用情况标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 标签可随时应用，从而在您选择如何管理数据方面提供了灵活性。 最佳实践是：在将数据摄取到[!DNL Experience Platform]中后，或当数据可用于[!DNL Platform]时，立即为数据设置标签。 您可以使用`/labels`端点创建、查看、编辑和删除标签。 要了解如何使用此端点，请访问[标签端点指南](./labels.md)。

## 营销操作

在[!DNL Data Governance]框架的上下文中，营销操作（也称为营销用例）是[!DNL Experience Platform]数据消费者可以采取的操作，贵组织希望对其限制数据使用。 有关使用营销操作的详细信息，请参阅[营销操作端点指南](./marketing-actions.md)。

## 支持

数据使用策略是描述允许或限制您对[!DNL Experience Platform]内的数据执行的营销操作类型的规则。 策略由以下项定义：

1. 特定营销操作
1. 限制对其执行操作的数据使用标签

要了解如何在API中管理策略，请参阅[策略端点指南](./policies.md)

## 评估

在将数据使用标签应用于[!DNL Platform]数据集并为针对这些标签的营销操作定义了数据使用策略后，“数据管理”功能允许您强制执行这些策略并防止构成违反策略的数据操作。

[!DNL Policy Service] API提供了端点，允许您针对数据集或数据使用标签的任意组合测试营销操作，以检查是否发生任何策略违规。 然后，您可以根据API响应，在体验应用程序中设置协议，以适当强制执行数据使用策略合规性。 有关更多信息，请参阅[评估端点指南](./evaluation.md) 。

## 后续步骤

要开始使用[!DNL Policy Service] API进行调用，请阅读[入门指南](./getting-started.md)，然后选择其中一个端点指南，以了解如何使用特定端点。 要使用[!DNL Experience Platform] UI处理标签和策略，请分别参阅[标签用户指南](../labels/user-guide.md)和[策略用户指南](../policies/user-guide.md)。
