---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 策略服务API指南
description: 策略服务API允许开发人员管理Experience Platform中的数据使用标签和策略。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 0c09db51d97bc0cf321c5d2fd57c42d194b25d5f
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 3%

---

# [!DNL Policy Service] API指南

Adobe Experience Platform数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和策略。 它在以下方面发挥着关键作用 [!DNL Experience Platform] 在各个级别，包括编目、数据谱系、数据使用标签、数据使用策略，以及控制营销活动的数据使用。

此 [!DNL Policy Service] API提供了多个端点，允许您以编程方式管理数据使用标签和策略，并评估营销操作是否存在策略违规。 这些端点概述如下。 有关详细信息，请参阅各个端点指南，并参阅 [快速入门指南](./getting-started.md) 有关所需标头的重要信息，请阅读示例API调用等。

要查看所有可用的端点和CRUD操作，请访问 [[!DNL Policy Service] API swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## 标记

将数据使用标签应用于架构，以根据应用于该数据的使用策略对数据集和字段进行分类。 您可以随时应用标签，灵活地选择管理数据的方式。 最佳实践鼓励在将数据摄取到其中后立即为其设置标签 [!DNL Experience Platform]，或当数据可用于以下项目时 [!DNL Platform]. 您可以使用创建、查看、编辑和删除标签 `/labels` 端点。 要了解如何使用此端点，请访问 [标签端点指南](./labels.md).

## 营销活动

在数据管理框架的上下文中，营销操作（也称为营销用例）是 [!DNL Experience Platform] 数据消费者可能会采取一些措施，贵组织希望限制对这些措施的数据使用。 有关使用营销活动的详细信息，请参阅 [营销操作端点指南](./marketing-actions.md).

## 支持

数据治理策略是描述允许或限制您对以下范围内的数据执行的营销操作类型的规则 [!DNL Experience Platform].

>[!NOTE]
>
>不应将数据管理策略与访问控制策略混淆，访问控制策略决定了组织中特定Platform用户可以访问的特定数据属性。 请参阅指南，网址为 [基于属性的访问控制](../../access-control/abac/overview.md) 以了解更多信息。

数据治理策略由以下内容定义：

1. 特定的营销活动
1. 操作被限制为无法执行的数据使用标签

要了解如何在API中管理策略，请参阅 [策略端点指南](./policies.md)

## 评估

将数据使用标签应用于Platform架构，并为针对这些标签的营销操作定义数据使用策略后，通过数据管理功能，可强制实施这些策略并阻止构成策略违规的数据操作。

此 [!DNL Policy Service] API提供了一些端点，可让您根据数据集或数据使用标签的任意组合测试营销操作，以检查是否发生了任何违反策略的情况。 根据API响应，您随后可以在体验应用程序中设置协议，以相应地强制实施数据使用策略合规性。 请参阅 [评估端点指南](./evaluation.md) 以了解更多信息。

## 后续步骤

要开始使用 [!DNL Policy Service] API，阅读 [快速入门指南](./getting-started.md) 然后选择其中一个端点指南以了解如何使用特定端点。 要使用 [!DNL Experience Platform] UI，请参阅 [标签用户指南](../labels/user-guide.md) 和 [策略用户指南](../policies/user-guide.md)、ID名称和ID名称等。
