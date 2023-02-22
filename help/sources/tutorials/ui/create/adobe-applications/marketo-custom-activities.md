---
title: 在UI中为自定义活动数据创建Marketo Engage源连接和数据流
description: 本教程提供了在UI中创建Marketo Engage源连接和数据流以将自定义活动数据导入Adobe Experience Platform的步骤。
source-git-commit: d049a29d4c39fa41917e8da1dde530966f4cbaf4
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# 创建 [!DNL Marketo Engage] UI中自定义活动数据的源连接和数据流

>[!NOTE]
>
>本教程提供了有关如何设置和调用 **自定义活动** 数据 [!DNL Marketo] Experience Platform。 有关如何 **标准活动** 数据，读取 [[!DNL Marketo] UI指南](./marketo.md).

除 [标准活动](../../../../connectors/adobe-applications/mapping/marketo.md#activities)，您还可以使用 [!DNL Marketo] 来源将自定义活动数据导入Adobe Experience Platform。 本文档提供了有关如何使用为自定义活动数据创建源连接和数据流的步骤 [!DNL Marketo] 源。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [B2B命名空间和模式自动生成实用程序](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md):B2B命名空间和模式自动生成实用程序允许您使用 [!DNL Postman] 为B2B命名空间和模式自动生成值。 在创建 [!DNL Marketo] 源连接和数据流。
* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [体验数据模型(XDM)](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [在UI中创建和编辑架构](../../../../../xdm/ui/resources/schemas.md):了解如何在UI中创建和编辑模式。
* [身份命名空间](../../../../../identity-service/namespaces.md):身份命名空间是 [!DNL Identity Service] 作为身份相关背景的指标。 完全限定的标识包括ID值和命名空间。
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 检索自定义活动详细信息

将自定义活动数据从 [!DNL Marketo] 要Experience Platform，请检索API名称和自定义活动的显示名称。

使用 [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) 界面。 在左侧导航中，位于 [!DNL Database Management]，选择 **Marketo自定义活动**.

界面会更新为自定义活动的显示，包括有关其各自显示名称和API名称的信息。 您还可以使用右边栏从您的帐户中选择和查看其他自定义活动。

![Adobe Marketo Engage UI中的“自定义活动”界面。](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

选择 **字段** 从顶部标题查看与自定义活动关联的字段。 在本页中，您可以查看自定义活动中字段的名称、API名称、描述和数据类型。 有关单个字段的详细信息将在稍后创建架构时在步骤中使用。

![MarketoMarketo EngageUI中的“自定义活动字段详细信息”页面。](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## 在B2B活动架构中为自定义活动设置字段组

在 *[!UICONTROL 模式]* Experience PlatformUI的功能板，选择 **[!UICONTROL 浏览]** 然后选择 **[!UICONTROL B2B活动]** 从架构列表。

>[!TIP]
>
>使用搜索栏可加快您在架构列表中的导航速度。

![选择了B2B活动架构的Experience PlatformUI中的架构工作区。](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### 为自定义活动创建新字段组

接下来，向 [!DNL B2B Activity] 架构。 此字段组应与您要摄取的自定义活动相对应，且应使用您之前检索到的自定义活动的显示名称。

要添加新字段组，请选择 **[!UICONTROL +添加]** 旁边 *[!UICONTROL 字段组]* 面板 *[!UICONTROL 组合物]*.

![架构结构。](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

的 *[!UICONTROL 添加字段组]* 窗口。 选择 **[!UICONTROL 创建新字段组]** 然后，为之前步骤中检索到的自定义活动提供相同的显示名称，并为新字段组提供可选描述。 完成后，选择 **[!UICONTROL 添加字段组]**.

![用于标记和创建新字段组的窗口。](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

创建后，您的新自定义活动字段组将显示在 [!UICONTROL 字段组] 目录。

![字段组面板下添加了新字段组的架构结构。](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### 向架构结构中添加新字段

接下来，向架构中添加新字段。 此新字段必须设置为 `type: object` 和将包含自定义活动的各个字段。

要添加新字段，请选择加号(`+`)。 的条目 *[!UICONTROL 无标题字段 |类型]* 中。 接下来，使用 *[!UICONTROL 字段属性]* 的上界。 将字段名称设置为自定义活动的API名称，并将显示名称设置为自定义活动的显示名称。 然后，将类型设置为 `object` 并将字段组分配给您在上一步中创建的自定义活动字段组。 完成后，选择 **[!UICONTROL 应用]**.

![具有加号(`+`)符号，以便可以添加新字段。](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

新字段将显示在您的架构中。

![架构中添加了新字段。](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### 向对象字段添加子字段 {#add-sub-fields-to-the-object-field}

准备架构的最后一个步骤是在上一步骤中创建的字段中添加单个字段。

![添加到架构中字段的子字段组。](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## 创建数据流

架构设置完成后，您现在可以继续为自定义活动数据创建数据流。

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL Adobe应用程序] 类别，选择 **[!UICONTROL Marketo Engage]**. 然后，选择 **[!UICONTROL 添加数据]** 创建新 [!DNL Marketo] 数据流。

![Experience PlatformUI上的源目录，并选择Marketo Engage源。](../../../../images/tutorials/create/marketo/catalog.png)

### 选择数据

选择 **[!UICONTROL 活动]** 从 [!DNL Marketo] 然后选择 **[!UICONTROL 下一个]**.

![在源工作流中选择数据步骤，并选择活动数据集。](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### 数据流详细信息

下一个， [为数据流提供信息](./marketo.md#provide-dataflow-details)，包括数据集和数据流的名称和描述、将要使用的架构以及配置 [!DNL Profile] 摄取、错误诊断和部分摄取。

![数据流详细步骤。](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### 映射

标准活动字段的映射已自动填充，但自定义活动字段必须手动映射到其相应的目标字段。

要开始映射自定义活动字段，请选择 **[!UICONTROL 新字段类型]** 然后选择 **[!UICONTROL 添加新字段]**.

![使用下拉菜单添加新字段的映射步骤。](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

在源数据结构中导航，并找到要摄取的自定义活动字段。 完成后，选择 **[!UICONTROL 选择]**.

>[!TIP]
>
>为避免混淆和处理重复的字段名称，自定义活动字段的前缀为API名称。

![源数据结构。](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

要添加目标字段，请选择架构图标 ![架构图标](../../../../images/tutorials/create/marketo-custom-activities/schema-icon.png) 然后，从目标架构中选择自定义活动字段。

![目标架构结构。](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

重复这些步骤以添加其余的自定义活动映射字段。 完成后，选择 **[!UICONTROL 下一个]**.

![源数据和目标数据的所有映射。](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### 请查看

的 *[!UICONTROL 审阅]* 步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源类型、所选源实体的相关路径以及该源实体中的列数。
* **[!UICONTROL 分配数据集和映射字段]**:显示源数据被摄取到的数据集，包括该数据集附加的架构。

审核数据流后，选择 **[!UICONTROL 保存并摄取]** 并为创建数据流留出一些时间。

![最后一个审核步骤，用于汇总有关连接、数据集和映射字段的信息。](../../../../images/tutorials/create/marketo-custom-activities/review.png)

>[!NOTE]
>
>完成摄取后，摄取的数据集将包含所有活动，包括 [!DNL Marketo] 实例。 要在Platform上选择自定义活动记录，您必须使用 [查询服务](../../../../../query-service/home.md) 并提供合适的谓词。

## 后续步骤

通过阅读本教程，您已为 [!DNL Marketo] 自定义活动数据，并创建了一个数据流以将该数据导入平台。 有关 [!DNL Marketo] 源，读取 [[!DNL Marketo] 源概述](../../../../connectors/adobe-applications/marketo/marketo.md).