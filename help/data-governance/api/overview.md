---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 策略服务API指南
topic: developer guide
description: 策略服务API允许开发人员在Experience Platform中管理数据使用标签和策略。 请按照本指南学习如何使用API执行关键操作。
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# [!DNL Policy Service] API指南

Adobe Experience Platform[!DNL Data Governance]允许您管理客户数据并确保符合适用于数据使用的法规、限制和政策。 它在[!DNL Experience Platform]的各个级别中起着关键作用，包括编目、数据谱系、数据使用标签、数据使用策略以及控制数据在营销活动中的使用。

[!DNL Policy Service] API提供多个端点，允许您以编程方式管理数据使用标签和策略，并评估违反策略的营销操作。 这些端点概述如下。 请访问各个端点指南获取详细信息，并参阅[快速入门指南](./getting-started.md)以获取有关所需标头、读取示例API调用等的重要信息。

要视图所有可用端点和CRUD操作，请访问[[!DNL Policy Service] API swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。

## 标签

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 可随时应用标签，在数据管理方式上提供灵活性。 最佳实践是，在将数据引入[!DNL Experience Platform]时或在数据可用于[!DNL Platform]时，立即给数据添加标签。 您可以使用`/labels`端点创建、视图、编辑和删除标签。 要了解如何使用此端点，请访问[labels endpoint guide](./labels.md)。

## 营销操作

在[!DNL Data Governance]框架的上下文中，营销操作（也称为营销用例）是[!DNL Experience Platform]数据消费者可以采取的操作，您的组织希望对其限制数据使用。 有关使用营销操作的详细信息，请参阅[营销操作端点指南](./marketing-actions.md)。

## 策略

数据使用策略是描述您允许对[!DNL Experience Platform]内的数据执行或限制的营销操作类型的规则。 策略由以下各项定义：

1. 特定营销活动
1. 限制不执行操作的数据使用标签

要了解如何管理API中的策略，请参阅[策略端点指南](./policies.md)

## 评估

一旦数据使用标签已应用到[!DNL Platform]数据集，且为针对这些标签的营销操作定义了数据使用策略，“数据管理”功能就允许您执行这些策略并防止构成策略违规的数据操作。

[!DNL Policy Service] API提供的端点允许您针对数据集或数据使用标签的任意组合测试营销操作，以检查是否发生任何违反策略的情况。 根据API响应，您随后可以在体验应用程序中设置协议以适当强制执行数据使用策略合规性。 有关详细信息，请参阅[评估端点指南](./evaluation.md)。

## 后续步骤

要开始使用[!DNL Policy Service] API进行调用，请阅读[入门指南](./getting-started.md)，然后选择其中一个端点指南来了解如何使用特定端点。 要使用[!DNL Experience Platform] UI处理标签和策略，请分别参阅[标签用户指南](../labels/user-guide.md)和[策略用户指南](../policies/user-guide.md)。