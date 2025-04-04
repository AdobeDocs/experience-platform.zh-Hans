---
keywords: Experience Platform；首页；热门话题
solution: Experience Platform
title: 策略服务API指南
description: 通过策略服务API，开发人员可以在Experience Platform中管理数据使用标签和策略。 参阅本指南，了解如何使用 API 执行关键操作。
role: Developer
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 4%

---

# [!DNL Policy Service] API指南

Adobe Experience Platform数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和策略。 它在各个级别的[!DNL Experience Platform]中起着关键作用，包括编目、数据谱系、数据使用标签、数据使用策略和控制营销操作的数据使用。

[!DNL Policy Service] API提供了多个端点，允许您以编程方式管理数据使用标签和策略，并评估策略违规的营销操作。 这些端点概述如下。 有关详细信息，请访问各个端点指南，请参阅[快速入门指南](./getting-started.md)，了解有关所需标头、读取示例API调用等的重要信息。

要查看所有可用的端点和CRUD操作，请访问[[!DNL Policy Service] API swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/)。

## 标记

将数据使用标签应用于架构，以根据应用于该数据的使用策略对数据集和字段进行分类。 您可以随时应用标签，灵活地选择管理数据的方式。 最佳实践鼓励在将数据摄取到[!DNL Experience Platform]中后立即标记数据，或者当数据在[!DNL Experience Platform]中可用时立即标记数据。 您可以使用`/labels`端点创建、查看、编辑和删除标签。 要了解如何使用此端点，请访问[标签端点指南](./labels.md)。

## 营销操作

在数据管理框架上下文中，营销操作（也称为营销用例）是[!DNL Experience Platform]数据使用者可以采取的操作，贵组织希望限制对这些操作的数据使用。 有关使用营销操作的详细信息，请参阅[营销操作端点指南](./marketing-actions.md)。

## 支持

数据治理策略是描述允许或限制您对[!DNL Experience Platform]内的数据执行的营销操作类型的规则。

>[!NOTE]
>
>不要将数据治理策略与访问控制策略混淆，访问控制策略确定组织中的某些Experience Platform用户可以访问的特定数据属性。 有关详细信息，请参阅[基于属性的访问控制](../../access-control/abac/overview.md)指南。

数据治理策略由以下内容定义：

1. 特定的营销活动
1. 操作被限制为无法执行的数据使用标签

要了解如何管理API中的策略，请参阅[策略端点指南](./policies.md)

## 评估

将数据使用标签应用于Experience Platform架构，并为针对这些标签的营销操作定义数据使用策略后，通过数据管理功能，可强制实施这些策略并阻止构成策略违规的数据操作。

[!DNL Policy Service] API提供了一些端点，可让您针对数据集或数据使用标签的任意组合测试营销操作，以检查是否发生了任何违反策略的情况。 根据API响应，您随后可以在体验应用程序中设置协议，以相应地强制实施数据使用策略合规性。 有关详细信息，请参阅[评估端点指南](./evaluation.md)。

## 后续步骤

要开始使用[!DNL Policy Service] API进行调用，请阅读[入门指南](./getting-started.md)，然后选择其中一个端点指南以了解如何使用特定端点。 要使用[!DNL Experience Platform] UI处理标签和策略，请分别参阅[标签用户指南](../labels/user-guide.md)和[策略用户指南](../policies/user-guide.md)。
