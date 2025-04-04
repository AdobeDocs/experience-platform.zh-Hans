---
title: 在UI中为自定义活动数据创建Marketo Engage Source连接和数据流
description: 本教程提供了在UI中创建Marketo Engage源连接和数据流以将自定义活动数据引入Adobe Experience Platform的步骤。
exl-id: 05a7b500-11d2-4d58-be43-a2c4c0ceeb87
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 0%

---

# 在用户界面中为自定义活动数据创建[!DNL Marketo Engage]源连接和数据流

>[!NOTE]
>
>本教程提供了有关如何设置并将&#x200B;**自定义活动**&#x200B;数据从[!DNL Marketo]带到Experience Platform的具体步骤。 有关如何引入&#x200B;**标准活动**&#x200B;数据的步骤，请阅读[[!DNL Marketo] UI指南](./marketo.md)。

除了[标准活动](../../../../connectors/adobe-applications/mapping/marketo.md#activities)之外，您还可以使用[!DNL Marketo]源将自定义活动数据引入Adobe Experience Platform。 本文档提供了有关如何使用UI中的[!DNL Marketo]源为自定义活动数据创建源连接和数据流的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [B2B命名空间和架构自动生成实用程序](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md)： B2B命名空间和架构自动生成实用程序允许您使用[!DNL Postman]自动生成B2B命名空间和架构的值。 必须先完成B2B命名空间和架构，然后才能创建[!DNL Marketo]源连接和数据流。
* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [体验数据模型(XDM)](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [在UI中创建和编辑架构](../../../../../xdm/ui/resources/schemas.md)：了解如何在UI中创建和编辑架构。
* [身份命名空间](../../../../../identity-service/features/namespaces.md)：身份命名空间是[!DNL Identity Service]的组件，充当与身份相关的上下文的指示器。 完全限定的身份包括ID值和命名空间。
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 检索您的自定义活动详细信息

将自定义活动数据从[!DNL Marketo]引入Experience Platform的第一步是检索API名称和自定义活动的显示名称。

使用[[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1)界面登录到您的帐户。 在左侧导航中的[!DNL Database Management]下，选择&#x200B;**Marketo自定义活动**。

界面将更新为自定义活动的显示，包括有关其各自显示名称和API名称的信息。 您还可以使用右边栏从帐户中选择和查看其他自定义活动。

![Adobe Marketo Engage UI中的自定义活动界面。](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

从顶部标题中选择&#x200B;**字段**&#x200B;以查看与自定义活动关联的字段。 在此页面中，您可以查看自定义活动中字段的名称、API名称、描述和数据类型。 有关各个字段的详细信息，将在稍后创建架构时使用的步骤中使用。

![Marketo Engage UI中的“Marketo自定义活动字段详细信息”页面。](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## 在B2B活动架构中为自定义活动设置字段组

在Experience Platform UI的&#x200B;*[!UICONTROL 架构]*&#x200B;仪表板中，选择&#x200B;**[!UICONTROL 浏览]**，然后从架构列表中选择&#x200B;**[!UICONTROL B2B活动]**。

>[!TIP]
>
>使用搜索栏可加快在架构列表中的导航。

![已选择B2B活动架构的Experience Platform UI中的架构工作区。](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### 为自定义活动创建新字段组

接下来，向[!DNL B2B Activity]架构中添加新的字段组。 此字段组应该与您要摄取的自定义活动相对应，并且应该使用您之前检索到的自定义活动的显示名称。

要添加新字段组，请选择&#x200B;*[!UICONTROL 合成]*&#x200B;下的&#x200B;*[!UICONTROL 字段组]*&#x200B;面板旁边的&#x200B;**[!UICONTROL +添加]**。

![架构结构。](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

出现&#x200B;*[!UICONTROL 添加字段组]*&#x200B;窗口。 选择&#x200B;**[!UICONTROL 创建新字段组]**，然后为您在前一步中检索的自定义活动提供相同的显示名称，并为新字段组提供可选描述。 完成后，选择&#x200B;**[!UICONTROL 添加字段组]**。

![用于标记和创建新字段组的窗口。](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

创建后，自定义活动的新字段组将显示在[!UICONTROL 字段组]目录中。

![在字段组面板下添加了新字段组的架构结构。](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### 向架构结构添加新字段

接下来，向架构中添加新字段。 此新字段必须设置为`type: object`，并将包含自定义活动的各个字段。

要添加新字段，请选择架构名称旁边的加号(`+`)。 *[!UICONTROL 无标题字段的条目 | 类型]*&#x200B;出现。 接下来，使用&#x200B;*[!UICONTROL 字段属性]*&#x200B;面板配置字段的属性。 将字段名称设置为您的自定义活动的API名称，并将显示名称设置为您的自定义活动的显示名称。 然后，将类型设置为`object`并将该字段组分配给您在上一步中创建的自定义活动字段组。 完成后，选择&#x200B;**[!UICONTROL 应用]**。

![选定加号(`+`)的架构结构，以便添加新字段。](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

新字段即会显示在您的架构中。

![新字段已添加到架构。](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### 向对象字段添加子字段 {#add-sub-fields-to-the-object-field}

准备架构的最后一步是在您在上一步中创建的字段中添加各个字段。

![添加到架构内字段的一组子字段。](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## 创建数据流

在架构设置完成后，您现在可以为自定义活动数据创建数据流。

在Experience Platform UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在[!UICONTROL Adobe应用程序]类别下，选择&#x200B;**[!UICONTROL Marketo Engage]**。 然后，选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的[!DNL Marketo]数据流。

![已选择Marketo Engage源的Experience Platform UI上的源目录。](../../../../images/tutorials/create/marketo/catalog.png)

### 选择数据

从[!DNL Marketo]数据集的列表中选择&#x200B;**[!UICONTROL 活动]**，然后选择&#x200B;**[!UICONTROL 下一步]**。

![选定了活动数据集的源工作流中的选择数据步骤。](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### 数据流详细信息

接下来，[提供您的数据流](./marketo.md#provide-dataflow-details)的信息，包括您的数据集和数据流的名称和描述、您将使用的架构以及用于[!DNL Profile]摄取、错误诊断和部分摄取的配置。

![数据流详细信息步骤。](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### 映射

系统会自动填充标准活动字段的映射，但自定义活动字段必须手动映射到其对应的目标字段。

要开始映射自定义活动字段，请选择&#x200B;**[!UICONTROL 新字段类型]**，然后选择&#x200B;**[!UICONTROL 添加新字段]**。

![带有下拉菜单的映射步骤以添加新字段。](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

浏览源数据结构并找到要摄取的自定义活动字段。 完成后，选择&#x200B;**[!UICONTROL 选择]**。

>[!TIP]
>
>为避免混淆并处理重复的字段名称，自定义活动字段将带有API名称前缀。

![源数据结构。](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

要添加目标字段，请选择架构图标![架构图标](/help/images/icons/schema.png)，然后从目标架构中选择自定义活动字段。

![目标架构结构。](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

重复这些步骤以添加其余的自定义活动映射字段。 完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![源数据和目标数据的所有映射。](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### 审查

将显示&#x200B;*[!UICONTROL 审核]*&#x200B;步骤，允许您在创建新数据流之前对其进行审核。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源类型、所选源实体的相关路径以及该源实体中的列数。
* **[!UICONTROL 分配数据集和映射字段]**：显示要将源数据摄取到哪个数据集，包括数据集所遵循的架构。

查看数据流后，选择&#x200B;**[!UICONTROL 保存并摄取]**，然后等待一些时间来创建数据流。

![总结有关连接、数据集和映射字段的信息的最终审阅步骤。](../../../../images/tutorials/create/marketo-custom-activities/review.png)

### 将自定义活动添加到现有活动数据流 {#add-to-existing-dataflows}

要将自定义活动数据添加到现有数据流，请使用要摄取的自定义活动数据修改现有活动数据流的映射。 这允许您将自定义活动摄取到相同的现有活动数据集中。 有关如何更新现有数据流的映射的更多信息，请阅读有关UI中[更新数据流的指南](../../update-dataflows.md)。

### 使用[!DNL Query Service]筛选自定义活动的活动 {#query-service-filter}

数据流完成后，您可以使用[查询服务](../../../../../query-service/home.md)来筛选自定义活动数据的活动。

将自定义活动摄取到Experience Platform后，自定义活动的API名称会自动变为其`eventType`。 使用`eventType={API_NAME}`筛选自定义活动数据。

```sql
SELECT * FROM with_custom_activities_ds_today WHERE eventType='aepCustomActivityDemo1' 
```

使用`IN`子句筛选多个自定义活动：

```sql
SELECT * FROM $datasetName WHERE eventType='{API_NAME}'
SELECT * FROM $datasetName WHERE eventType IN ('aepCustomActivityDemo1', 'aepCustomActivityDemo2')
```

下图显示了[查询编辑器](../../../../../query-service/ui/user-guide.md)中过滤自定义活动数据的示例SQL语句。

![Experience Platform UI显示自定义活动的查询示例。](../../../../images/tutorials/create/marketo-custom-activities/queries.png)

## 后续步骤

通过学习本教程，您已为[!DNL Marketo]自定义活动数据设置Experience Platform架构并创建数据流以将该数据引入到Experience Platform。 有关[!DNL Marketo]源的一般信息，请阅读[[!DNL Marketo] 源概述](../../../../connectors/adobe-applications/marketo/marketo.md)。
