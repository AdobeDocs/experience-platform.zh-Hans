---
title: Real-time Customer Data Platform B2B版本的分段用例
description: 各种可用的Adobe Real-time Customer Data Platform B2B版本用例的概述。
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: b436aeb8a8628d9b481041be518c1113fb54c342
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B版本的分段用例

本文档提供了Adobe Real-time Customer Data Platform B2B版本中的区段定义示例，以及针对常见B2B用例如何组合不同类型的属性。 要了解目标如何适合您的B2B工作流，请参阅 [端到端教程](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>这些分段用例所需的属性仅适用于Real-time Customer Data Platform B2B版本客户。 如果您没有使用Real-time Customer Data Platform B2B版本，请参阅 [分段概述](./segmentation-overview.md) 而是。

## 先决条件 {#prerequisites}

必须先完成以下步骤，然后才能对B2B类使用分段属性：

1. 创建使用B2B类的架构。 B2B版本类包括Account、Campaign、Opportunity、Marketing List等。 有关以下项的信息 [如何设置与B2B类一起使用的架构](../schemas/b2b.md) 请参阅架构文档。
1. 在体验数据模型(XDM) B2B架构之间创建关系。 基于B2B版本属性的区段需要类之间的关系，以充分利用扩展的B2B分段功能。 请参阅相关文档 [如何定义两个B2B架构之间的关系](../../xdm/tutorials/relationship-b2b.md) 了解更多信息。
1. 使用基于B2B架构的数据集来引入数据。 请参阅源文档，了解 [有关如何摄取数据的信息](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. 阅读 [区段生成器用户指南](../../segmentation/ui/segment-builder.md) 以获取有关如何构建区段的更详细指南。

在满足这些要求后，您就能够为常见的B2B用例组合这些属性。

## 快速入门 {#getting-started}

一旦B2B类的合并架构建立了关系并已用于摄取数据，则其属性在区段生成器的左边栏中可用。

B2B类及其属性会附加 `B2B` 区段工作区中的标签，以区分它们与Real-time Customer Data Platform中可用的标准区段。

为了有效地为B2B用例创建区段，请务必熟悉架构并了解数据模型的外观。 了解数据从一个数据对象移动到另一个数据对象的路径也很有用。

下图说明了Real-Time CDP B2B版本中可用的B2B类之间的关系。

![B2B类ERD](../assets/segmentation/b2b-classes.png)

由于数据模型可能很复杂，因此您可以使用Platform UI查看数据模型的更详细的可视化表示形式，以帮助查找用例的相关属性。 要开始配置，请转到Platform UI，然后在左侧导航中选择架构。

从可用列表中选择相应的架构，然后从中选择相应的关系 [!UICONTROL 合成] 侧边栏。 在以下示例中，选择“人员”关系可揭示当前架构中的哪个属性引用了相关的“人员”架构（如果它是关系中的源架构），或被“人员”架构引用（如果它是关系中的引用架构）。

![在架构工作区中使用人员关系的源密钥示例](../assets/segmentation/source-key-schema-relationship-example.png)

此关系通过使用反映在区段生成器中 `Key` 文件夹，如下图所示。

![在分段工作区中使用区段生成器的源键示例](../assets/segmentation/source-key-segmentation-example.png)

请参阅 [Real-time Customer Data Platform B2B版本文档中的架构](../schemas/b2b.md) 有关可用B2B类的详细信息。

以下用例提供了有关使用哪些类在不同架构之间建立关系以实现这些结果的信息。 这些示例可用于帮助您创建自己的区段。

## 不同分段用例的示例 {#use-cases}

以下用例可用于B2B版本的分段。 每个示例都提供了区段功能的说明以及用于创建它们的类的说明。 提供的图像突出显示 [!UICONTROL 属性] 反映架构结构的侧边栏。 此 [!UICONTROL 区段属性] 右侧部分包含区段属性的书面细分。

### 示例1：查找B2B机会的“决策者” {#find-decision-maker}

查找所有作为任何机会的“决策者”的人员。 此区段需要 [!UICONTROL XDM个人资料] 类和 [!UICONTROL XDM业务机会人员关系] 类。

![显示示例1设置的UI](../assets/segmentation/example-1.png)

### 示例2：查找分配给超过特定美元金额的业务机会的B2B配置文件 {#find-opportunities-amount}

查找直接分配到任何商机金额超过给定金额（100万美元）的商机的所有人员。 此区段需要 [!UICONTROL XDM个人资料] 类， [!UICONTROL XDM业务机会人员关系] 类，和 [!UICONTROL XDM商业机会] 类。

![显示示例2设置的UI](../assets/segmentation/example-2.png)

### 实例3：按地点查找分配给业务机会的B2B配置文件 {#find-opportunities-location}

查找直接分配到客户位于给定位置（加拿大）的任何业务机会的所有人员。 此区段需要 [!UICONTROL XDM个人资料] 类， [!UICONTROL XDM业务机会人员关系] 类， [!UICONTROL XDM商业机会] 类，和 [!UICONTROL XDM商业帐户] 类。

![显示示例3设置的UI](../assets/segmentation/example-3.png)

### 示例4：按行业和浏览行为查找机会的“决策者” {#find-industry-browsing-behavior}

查找客户处于“金融”行业的任何机会的“决策者”并在过去三天中访问过定价页面的所有人员。 此区段需要 [!UICONTROL XDM个人资料] 类， [!UICONTROL XDM业务机会人员关系] 类， [!UICONTROL XDM商业机会] 类，和 [!UICONTROL XDM商业帐户] 类，和 [!UICONTROL XDM ExperienceEvent] 类。

![显示示例4设置的UI](../assets/segmentation/example-4.png)

### 示例5：按部门名称和业务机会金额查找业务机会的B2B配置文件 {#find-department-opportunity-amount}

查找所有在人力资源(HR)部门工作并具有至少一个与给定金额（100万美元）或以上金额相当的未完成机会的帐户的人员。 此区段需要 [!UICONTROL XDM个人资料] 类， [!UICONTROL XDM商业帐户] 类，和 [!UICONTROL XDM商业机会] 类。

![显示示例5设置的UI](../assets/segmentation/example-5.png)

### 示例6：按职称和年度帐户收入查找B2B用户档案 {#find-by-job-title-and-revenue}

查找所有其职衔是副总裁并且拥有任何账户具有给定金额（1亿美元）或以上年收入的人员，并且在上个月至少访问过3次定价页面。 此区段需要 [!UICONTROL XDM个人资料] 类， [!UICONTROL XDM商业帐户] 类，和 [!UICONTROL XDM ExperienceEvent] 类。

![显示示例6设置的UI](../assets/segmentation/example-6.png)

### 示例7：按机会状态和浏览行为查找“决策者” {#find-by-opportunity-status-and-browsing-behavior}

查找所有作为任何已结束的失去的机会的“决策者”的人员，并在上周访问过定价页面。 此区段需要 [!UICONTROL XDM个人资料] 类， [!UICONTROL XDM业务机会人员关系] 类， [!UICONTROL XDM商业机会] 类，和 [!UICONTROL XDM ExperienceEvent] 类。

![显示示例7设置的UI](../assets/segmentation/example-7.png)

### 示例8：使用相关帐户扩大分段范围 {#related-accounts}

查找在人力资源(HR)部门工作并与任何帐户相关的所有人员 *或任何帐户的相关帐户* 至少有一个与给定金额（100万美元）或以上相同的未完成机会。 此区段需要 [!UICONTROL XDM个人资料] 类， [!UICONTROL XDM商业帐户] 类，和 [!UICONTROL XDM商业机会] 类。

![显示相关帐户分段的UI](../assets/segmentation/example-8.png)

### 示例9：使用潜在客户得分和/或客户得分来限定用户档案 {#account-scoring}

查找商机得分超过80的所有用户档案。

![显示预测性商机和帐户评分分段的UI](../assets/segmentation/example-9.png)

### 示例10：查找与父组织收入超过特定美元金额的帐户关联的B2B配置文件 {#find-parent-org-amount}

查找与父组织收入超过给定金额($100,000,000)的帐户关联的所有人员。

![显示分段父组织的UI](../assets/segmentation/example-10.png)

### 示例11：按职务和具有有效关系的帐户名查找B2B配置文件 {#find-by-job-title-and-account-name}

查找客户“Acme”（帐户关系为“活动”）上所有身为“经理”的人员。

![显示分段父组织的UI](../assets/segmentation/example-11.png)

### 示例12：查找actualCost超过budgetedCost的营销活动所定向的B2B配置文件 {#find-actualcost-exceed-budgetcost}

查找actualCost超过budgetedCost的营销活动所针对的所有人员。

![显示分段父组织的UI](../assets/segmentation/example-12.png)

### 示例13：查找属于Marketo静态列表的B2B配置文件和isDeleted=false {#find-marketo-static-list}

查找所有属于Marketo静态列表“周年纪念用户”的人员，其中isDeleted=false。

![显示分段父组织的UI](../assets/segmentation/example-13.png)

## 后续步骤 {#next-steps}

阅读本概述后，您现在了解了使用Real-Time CDP B2B版本时可用的分段可能性。 欲知分段服务的详情，请阅读 [分段文档](../../segmentation/home.md).
