---
title: 在UI中为自定义Marketo Engage数据创建活动源连接和数据流
description: 本教程提供了在UI中创建Marketo Engage源连接和数据流的步骤，以便将自定义活动数据引入Adobe Experience Platform。
source-git-commit: e584fbdfa64516a0dad1e7b99eb347f18e59d6d5
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 0%

---

# 创建 [!DNL Marketo Engage] UI中自定义活动数据的源连接和数据流

>[!NOTE]
>
>本教程提供了有关如何设置和引入的具体步骤 **自定义活动** 数据来源 [!DNL Marketo] 以Experience Platform。 有关如何引入 **标准活动** 数据，读取 [[!DNL Marketo] UI指南](./marketo.md).

除此之外 [标准活动](../../../../connectors/adobe-applications/mapping/marketo.md#activities)，您还可以使用 [!DNL Marketo] 将自定义活动数据引入Adobe Experience Platform的源。 本文档提供了有关如何使用为自定义活动数据创建源连接和数据流的步骤。 [!DNL Marketo] UI中的源。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [B2B命名空间和模式自动生成实用程序](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md)：通过B2B命名空间和模式自动生成实用程序，您可以使用 [!DNL Postman] 自动生成B2B命名空间和架构的值。 必须先完成B2B命名空间和架构，然后才能创建 [!DNL Marketo] 源连接和数据流。
* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [体验数据模型(XDM)](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [在UI中创建和编辑架构](../../../../../xdm/ui/resources/schemas.md)：了解如何在UI中创建和编辑架构。
* [身份命名空间](../../../../../identity-service/namespaces.md)：身份命名空间是的组件 [!DNL Identity Service] 用作与身份相关的上下文的指示器。 完全限定的身份包括ID值和命名空间。
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 检索自定义活动详细信息

从引入自定义活动数据的第一步 [!DNL Marketo] Experience Platform是检索API名称和自定义活动的显示名称。

使用登录到您的帐户 [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) 界面。 在左侧导航中，在 [!DNL Database Management]，选择 **Marketo自定义活动**.

界面将更新为自定义活动的显示，包括关于其各自显示名称和API名称的信息。 您还可以使用右边栏从帐户中选择和查看其他自定义活动。

![Adobe Marketo Engage UI中的“自定义活动”界面。](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

选择 **字段** ，以查看与自定义活动关联的字段。 在此页面中，您可以查看自定义活动中字段的名称、API名称、描述和数据类型。 有关各个字段的详细信息，将在创建架构的后续步骤中使用。

![Marketo EngageUI中的“Marketo自定义活动字段详细信息”页面。](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## 在B2B活动架构中为自定义活动设置字段组

在 *[!UICONTROL 架构]* Experience PlatformUI的控制板，选择 **[!UICONTROL 浏览]** 然后选择 **[!UICONTROL B2B活动]** 架构列表中。

>[!TIP]
>
>使用搜索栏可加快在架构列表中的导航。

![选择了B2BExperience Platform架构的活动用户界面中的架构工作区。](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### 为自定义活动创建新字段组

接下来，将新的字段组添加到 [!DNL B2B Activity] 架构。 此字段组应与您要摄取的自定义活动对应，并应使用您之前检索的自定义活动的显示名称。

要添加新字段组，请选择 **[!UICONTROL +添加]** 在 *[!UICONTROL 字段组]* 下的面板 *[!UICONTROL 合成]*.

![架构结构。](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

此 *[!UICONTROL 添加字段组]* 窗口。 选择 **[!UICONTROL 创建新字段组]** ，然后为您在之前的步骤中检索到的自定义活动提供相同的显示名称，并为新字段组提供可选描述。 完成后，选择 **[!UICONTROL 添加字段组]**.

![用于标记和创建新字段组的窗口。](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

创建后，您的新自定义活动字段组将显示在 [!UICONTROL 字段组] 目录。

![在字段组面板下添加了新字段组的架构结构。](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### 向架构结构添加新字段

接下来，向架构中添加一个新字段。 此新字段必须设置为 `type: object` 和将包含自定义活动的各个字段。

要添加新字段，请选择加号(`+`)。 条目 *[!UICONTROL 无标题字段 |类型]* 显示。 接下来，使用配置字段的属性 *[!UICONTROL 字段属性]* 面板。 将字段名称设置为自定义活动的API名称，将显示名称设置为自定义活动的显示名称。 然后，将类型设置为 `object` 并将字段组分配给在上一步中创建的自定义活动字段组。 完成后，选择 **[!UICONTROL 应用]**.

![带加号(`+`)符号，以便添加新字段。](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

新字段会显示在您的架构中。

![架构中添加了新字段。](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### 将子字段添加到对象字段 {#add-sub-fields-to-the-object-field}

准备架构的最后一步是在您在上一步中创建的字段中添加各个字段。

![添加到架构中字段的一组子字段。](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## 创建数据流

架构设置完成后，您现在可以继续为自定义活动数据创建数据流。

在Platform UI中，选择 **[!UICONTROL 源]** 以访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在 [!UICONTROL Adobe应用程序] 类别，选择 **[!UICONTROL Marketo Engage]**. 然后，选择 **[!UICONTROL 添加数据]** 以新建 [!DNL Marketo] 数据流。

![已选择Marketo Engage源的Experience PlatformUI上的源目录。](../../../../images/tutorials/create/marketo/catalog.png)

### 选择数据

选择 **[!UICONTROL 活动]** 从列表 [!DNL Marketo] 数据集，然后选择 **[!UICONTROL 下一个]**.

![选择活动数据集后，源工作流中的选择数据步骤。](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### 数据流详细信息

下一步， [为数据流提供信息](./marketo.md#provide-dataflow-details)，包括数据集和数据流的名称和描述、将使用的架构以及配置 [!DNL Profile] 摄取、错误诊断和部分摄取。

![数据流详细信息步骤。](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### 映射

自动填充标准活动字段的映射，但自定义活动字段必须手动映射到其对应的目标字段。

要开始映射自定义活动字段，请选择 **[!UICONTROL 新字段类型]** 然后选择 **[!UICONTROL 添加新字段]**.

![使用下拉菜单添加新字段的映射步骤。](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

浏览源数据结构并找到要摄取的自定义活动字段。 完成后，选择 **[!UICONTROL 选择]**.

>[!TIP]
>
>为避免混淆并处理重复的字段名称，自定义活动字段将带有API名称前缀。

![源数据结构。](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

要添加目标字段，请选择架构图标 ![架构图标](../../../../images/tutorials/create/marketo-custom-activities/schema-icon.png) 然后从目标架构中选择自定义活动字段。

![目标架构结构。](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

重复这些步骤以添加其余的自定义活动映射字段。 完成后，选择 **[!UICONTROL 下一个]**.

![源数据和目标数据的所有映射。](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### 请查看

此 *[!UICONTROL 审核]* 步骤，允许您在创建新数据流之前对其进行查看。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源类型、所选源实体的相关路径以及源实体中的列数。
* **[!UICONTROL 分配数据集和映射字段]**：显示要将源数据摄取到哪个数据集，包括该数据集所遵循的架构。

查看数据流后，选择 **[!UICONTROL 保存并摄取]** 并留出一些时间来创建数据流。

![总结有关连接、数据集和映射字段的信息的最后审核步骤。](../../../../images/tutorials/create/marketo-custom-activities/review.png)

### 将自定义活动添加到现有活动数据流 {#add-to-existing-dataflows}

要将自定义活动数据添加到现有数据流，请使用要摄取的自定义活动数据修改现有活动数据流的映射。 这样，您可以将自定义活动摄取到相同的现有活动数据集中。 有关如何更新现有数据流的映射的更多信息，请阅读以下指南： [在UI中更新数据流](../../update-dataflows.md).

### 使用 [!DNL Query Service] 筛选自定义活动的活动 {#query-service-filter}

数据流完成后，您可以使用 [查询服务](../../../../../query-service/home.md) 以筛选自定义活动数据的活动。

将自定义活动摄取到Platform后，自定义活动的API名称会自动变为 `eventType`. 使用 `eventType={API_NAME}` 以筛选自定义活动数据。

```sql
SELECT * FROM with_custom_activities_ds_today WHERE eventType='aepCustomActivityDemo1' 
```

使用 `IN` 用于筛选多个自定义活动的子句：

```sql
SELECT * FROM $datasetName WHERE eventType='{API_NAME}'
SELECT * FROM $datasetName WHERE eventType IN ('aepCustomActivityDemo1', 'aepCustomActivityDemo2')
```

下图显示了 [查询编辑器](../../../../../query-service/ui/user-guide.md) 用于筛选自定义活动数据。

![显示自定义活动的查询示例的平台UI。](../../../../images/tutorials/create/marketo-custom-activities/queries.png)

## 后续步骤

通过阅读本教程，您已为设置一个平台架构 [!DNL Marketo] 自定义活动数据并创建了一个数据流以将该数据传送到Platform。 欲知关于 [!DNL Marketo] 源，请阅读 [[!DNL Marketo] 源概述](../../../../connectors/adobe-applications/marketo/marketo.md).