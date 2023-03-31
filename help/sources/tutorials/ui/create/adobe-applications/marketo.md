---
title: 在UI中创建Marketo Engage源连接和数据流
description: 本教程提供了在UI中创建Marketo Engage源连接和数据流以将B2B数据引入Adobe Experience Platform的步骤。
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: b271d28677543f773fe1ba471fc08574e7c5542b
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# 创建 [!DNL Marketo Engage] UI中的源连接和数据流

>[!IMPORTANT]
>
>在创建 [!DNL Marketo Engage] 源连接和数据流之间，您必须首先确保 [已映射Adobe组织ID](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html?lang=en) in [!DNL Marketo]. 此外，您还必须确保您已完成 [自动填充 [!DNL Marketo] B2B命名空间和架构](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) 创建源连接和数据流之前。

本教程提供了创建 [!DNL Marketo Engage] (以下简称“[!DNL Marketo]“)UI中的源连接器，将B2B数据导入Adobe Experience Platform。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [B2B命名空间和模式自动生成实用程序](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md):B2B命名空间和模式自动生成实用程序允许您使用 [!DNL Postman] 为B2B命名空间和模式自动生成值。 在创建 [!DNL Marketo] 源连接和数据流。
* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [体验数据模型(XDM)](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [在UI中创建和编辑架构](../../../../../xdm/ui/resources/schemas.md):了解如何在UI中创建和编辑模式。
* [身份命名空间](../../../../../identity-service/namespaces.md):身份命名空间是 [!DNL Identity Service] 作为身份相关背景的指标。 完全限定的标识包括ID值和命名空间。
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

为了访问 [!DNL Marketo] 帐户时，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `munchkinId` | Munchkin ID是特定 [!DNL Marketo] 实例。 |
| `clientId` | 您的 [!DNL Marketo] 实例。 |
| `clientSecret` | 您的唯一客户端密钥 [!DNL Marketo] 实例。 |

有关获取这些值的更多信息，请参阅 [[!DNL Marketo] 身份验证指南](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

收集所需的凭据后，即可执行下一节中的步骤。

## 连接 [!DNL Marketo] 帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL Adobe应用程序] 类别，选择 **[!UICONTROL Marketo Engage]**. 然后，选择 **[!UICONTROL 添加数据]** 创建新 [!DNL Marketo] 数据流。

![目录](../../../../images/tutorials/create/marketo/catalog.png)

的 **[!UICONTROL 连接Marketo Engage帐户]** 页面。 在此页面上，您可以使用新帐户或访问现有帐户。

### 现有帐户

要使用现有帐户创建数据流，请选择 **[!UICONTROL 现有帐户]** ，然后选择 [!DNL Marketo] 帐户。 选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/marketo/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供帐户名称、可选描述和 [!DNL Marketo] 身份验证凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![新建](../../../../images/tutorials/create/marketo/new.png)

## 选择数据集

创建 [!DNL Marketo] 帐户，下一步会提供一个界面供您浏览 [!DNL Marketo] 数据集。

界面的左半部分是目录浏览器，显示 [!DNL Marketo] 数据集。 功能齐全 [!DNL Marketo] 源连接需要摄取九个不同的数据集。 如果您还在使用 [!DNL Marketo] 基于帐户的营销(ABM)功能，则还必须创建第10个数据流以引入 [!UICONTROL 指定帐户] 数据集。

>[!NOTE]
>
>为简短起见，以下教程使用 [!UICONTROL 机会] 例如，但下面列出的步骤适用于以下10个 [!DNL Marketo] 数据集。

选择要先摄取的数据集，然后选择 **[!UICONTROL 下一个]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## 提供数据流详细信息 {#provide-dataflow-details}

的 [!UICONTROL 数据流详细信息] 页面允许您选择是要使用现有数据集还是新数据集。 在此过程中，您还可以配置 [!UICONTROL 配置文件数据集], [!UICONTROL 错误诊断], [!UICONTROL 部分摄取]和 [!UICONTROL 警报].

![数据流详细信息](../../../../images/tutorials/create/marketo/dataflow-details.png)

>[!BEGINTABS]

>[!TAB 使用现有数据集]

要将数据摄取到现有数据集，请选择 **[!UICONTROL 现有数据集]**. 您可以使用 [!UICONTROL 高级搜索] 选项，或者通过在下拉菜单中滚动浏览现有数据集列表来配置。 选择数据集后，请为数据流提供名称和描述。

![现有数据集](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!TAB 使用新数据集]

要摄取到新数据集，请选择 **[!UICONTROL 新数据集]** 然后，提供输出数据集名称和可选描述。 接下来，使用 [!UICONTROL 高级搜索] 选项或通过滚动下拉菜单中的现有架构列表来迁移。 选择架构后，请为数据流提供名称和描述。

![新数据集](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!ENDTABS]

### 启用 [!DNL Profile] 和错误诊断

接下来，选择 **[!UICONTROL 配置文件数据集]** 切换为启用数据集 [!DNL Profile]. 这允许您创建实体属性和行为的整体视图。 所有数据 [!DNL Profile]-enabled数据集将包含在 [!DNL Profile] 和更改将在您保存数据流时应用。

[!UICONTROL 错误诊断] 为数据流中发生的任何错误记录启用详细的错误消息生成，而 [!UICONTROL 部分摄取] 允许您摄取包含错误的数据，最多可达您手动定义的特定阈值。 请参阅 [部分批量摄取概述](../../../../../ingestion/batch-ingestion/partial.md) 以了解更多信息。

>[!IMPORTANT]
>
>的 [!DNL Marketo] 源使用批量摄取来摄取所有历史记录，并使用流式摄取来进行实时更新。 这允许源在摄取任何错误记录时继续流式传输。 启用 **[!UICONTROL 部分摄取]** 切换，然后设置 [!UICONTROL 错误阈值%] 以防止数据流失败。

![配置文件和错误](../../../../images/tutorials/create/marketo/profile-and-errors.png)

### 启用警报

您可以启用警报以接收有关数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅源警报](../../alerts.md).

完成向数据流提供详细信息后，选择 **[!UICONTROL 下一个]**.

![警报](../../../../images/tutorials/create/marketo/alerts.png)

### 在摄取公司数据时跳过未声明的帐户

创建数据流以从公司数据集摄取数据时，您可以配置 [!UICONTROL 排除未声明的帐户] 从摄取中排除或包含未声明的帐户。

当个人填写表格时， [!DNL Marketo] 根据不包含其他数据的公司名称创建虚拟帐户记录。 对于新数据流，默认情况下会启用用于排除未声明帐户的切换开关。 对于现有数据流，您可以启用或禁用该功能，其更改将应用于新摄取的数据，而非现有数据。

![未声明的帐户](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## 映射 [!DNL Marketo] 用于定位XDM字段的数据集源字段

的 [!UICONTROL 映射] 此时会显示步骤，为您提供一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

每个 [!DNL Marketo] 数据集有其自己的特定映射规则可遵循。 有关如何映射的更多信息，请参阅以下内容 [!DNL Marketo] 数据集到XDM:

* [活动](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [项目](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [方案成员资格](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [公司](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [静态列表](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [静态列表成员关系](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [指定帐户](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [机会](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [机会联系角色](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [人员](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

根据您的需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以导出计算值或计算值。 有关使用映射界面的完整步骤，请参阅 [数据准备UI指南](../../../../../data-prep/ui/mapping.md).

![映射](../../../../images/tutorials/create/marketo/mapping.png)

映射集准备就绪后，选择 **[!UICONTROL 下一个]** 并且需要片刻时间才能创建新数据流。

## 查看数据流

的 **[!UICONTROL 审阅]** 步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源类型、所选源实体的相关路径以及该源实体中的列数。
* **[!UICONTROL 分配数据集和映射字段]**:显示源数据被摄取到的数据集，包括该数据集附加的架构。

审核数据流后，选择 **[!UICONTROL 保存并摄取]** 并为创建数据流留出一些时间。

![审查](../../../../images/tutorials/create/marketo/review.png)

## 监控数据流

创建数据流后，您可以监控通过其摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的更多信息，请参阅 [监控UI中的数据流](../../../../../dataflows/ui/monitor-sources.md).

## 删除属性

数据集中的自定义属性不能以追溯方式隐藏或删除。 如果要隐藏或删除现有数据集中的自定义属性，则必须创建一个没有此自定义属性的新数据集、一个新的XDM架构，并为您创建的新数据集配置新的数据流。 您还必须禁用或删除原始数据流，该数据流包含具有您要隐藏或删除的自定义属性的数据集。

## 删除数据流

您可以删除不再需要或使用错误创建的数据流 **[!UICONTROL 删除]** 函数 [!UICONTROL 数据流] 工作区。 有关如何删除数据流的更多信息，请参阅 [删除UI中的数据流](../../delete.md).

## 后续步骤

通过阅读本教程，您已成功创建了要引入的数据流 [!DNL Marketo] 数据。 传入数据现在可由下游Platform服务使用，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-Time Customer Profile] 概述](/help/profile/home.md)
* [[!DNL Data Science Workspace] 概述](/help/data-science-workspace/home.md)

## 附录 {#appendix}

以下部分提供了在使用 [!DNL Marketo] 来源。

### UI中的错误消息 {#error-messages}

当Platform检测到您的设置存在问题时，UI中会显示以下错误消息：

#### [!DNL Munchkin ID] 未映射到相应的组织

如果您的 [!DNL Munchkin ID] 未映射到您使用的平台组织。 配置 [!DNL Munchkin ID] 和贵组织使用 [[!DNL Marketo] 界面](https://app-sjint.marketo.com/#MM0A1).

![显示Marketo实例未正确映射到Adobe组织的错误消息。](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### 缺少主标识

如果缺少主标识，则数据流将无法保存和摄取。 确保 [XDM架构中存在主标识](../../../../../xdm/tutorials/create-schema-ui.md)，然后再尝试配置数据流。

![显示XDM架构中缺少主标识的错误消息。](../../../../images/tutorials/create/marketo/no-primary-identity.png)

