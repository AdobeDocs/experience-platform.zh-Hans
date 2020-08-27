---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 策略服务API开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: 71678b10c9e137016ea404305b272508b9c8cabe
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---


# [!DNL Policy Service] API开发人员指南

Adobe Experience Platform [!DNL Data Governance] 允许您管理客户数据并确保遵守适用于数据使用的法规、限制和政策。 它在各个级别(包括编目、 [!DNL Experience Platform] 数据谱系、数据使用标签、数据使用策略)中起关键作用，并控制数据在营销活动中的使用。

API提 [!DNL Policy Service] 供了多个端点，允许您以编程方式管理数据使用标签和策略，以及评估违反策略的营销操作。 这些端点概述如下。 请访问各个端点指南获取详细信息，并参 [阅入门指南](./getting-started.md) ，获取有关所需标头、读取示例API调用等的重要信息。

要视图所有可用端点和CRUD操作，请访 [[!DNL Policy Service] 问API swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。

## 标签

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 可随时应用标签，在数据管理方式上提供灵活性。 最佳实践是，在数据被引入或 [!DNL Experience Platform]数据可供使用时，立即添加标签 [!DNL Platform]。 您可以使用端点创建、视图、编辑和删除标 `/labels` 签。 要了解如何使用此端点，请访问标签 [端点指南](./labels.md)。

## 营销操作

在框架的上下文中，营销操作(也称为 [!DNL Data Governance] 营销用例)是数据消费者可以采取的 [!DNL Experience Platform] 操作，您的组织希望对其限制数据使用。 有关使用营销操作的详细信息，请参阅营销 [操作端点指南](./marketing-actions.md)。

## 策略

数据使用策略是描述允许或限制您对中的数据执行的营销操作种类的规则 [!DNL Experience Platform]。 策略由以下各项定义：

1. 特定营销活动
1. 限制不执行操作的数据使用标签

要了解如何在API中管理策略，请参阅策略端 [点指南](./policies.md)

## 评估

一旦数据使用标签已应用到数据集 [!DNL Platform] ，并且为针对这些标签的营销操作定义了数据使用策略，“数据管理”功能就允许您实施这些策略并防止构成策略违规的数据操作。

API提 [!DNL Policy Service] 供了端点，允许您针对数据集或数据使用标签的任意组合测试营销操作，以检查是否发生任何策略违规。 根据API响应，您随后可以在体验应用程序中设置协议以适当强制执行数据使用策略合规性。 See the [evaluation endpoints guide](./evaluation.md) for more information.

## 后续步骤

要开始使用API进行调 [!DNL Policy Service] 用，请阅读 [入门指南](./getting-started.md) ，然后选择一个端点指南，以了解如何使用特定端点。 要使用UI处理标签和策 [!DNL Experience Platform] 略，请分别参 [阅标签用](../labels/user-guide.md) 户指 [南和策略用户指南](../policies/user-guide.md)。