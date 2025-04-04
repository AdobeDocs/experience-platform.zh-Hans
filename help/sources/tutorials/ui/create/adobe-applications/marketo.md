---
title: 在UI中创建Marketo Engage Source连接和数据流
description: 本教程提供了在UI中创建Marketo Engage源连接和数据流以将B2B数据引入Adobe Experience Platform的步骤。
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 2%

---

# 在UI中创建[!DNL Marketo Engage]源连接和数据流

>[!IMPORTANT]
>
>在创建[!DNL Marketo Engage]源连接和数据流之前，必须首先确保已在[!DNL Marketo]中映射[您的Adobe组织ID](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html)。 此外，您还必须确保在创建源连接和数据流之前已完成[自动填充 [!DNL Marketo] B2B命名空间和架构](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md)。

本教程提供了在UI中创建[!DNL Marketo Engage]（以下简称“[!DNL Marketo]”）源连接器以将B2B数据引入Adobe Experience Platform的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [B2B命名空间和架构自动生成实用程序](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md)： B2B命名空间和架构自动生成实用程序允许您使用[!DNL Postman]自动生成B2B命名空间和架构的值。 必须先完成B2B命名空间和架构，然后才能创建[!DNL Marketo]源连接和数据流。
* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [体验数据模型(XDM)](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [在UI中创建和编辑架构](../../../../../xdm/ui/resources/schemas.md)：了解如何在UI中创建和编辑架构。
* [身份命名空间](../../../../../identity-service/features/namespaces.md)：身份命名空间是[!DNL Identity Service]的组件，充当与身份相关的上下文的指示器。 完全限定的身份包括ID值和命名空间。
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

要在Experience Platform上访问您的[!DNL Marketo]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---- | ---- |
| `munchkinId` | Munchkin ID是特定[!DNL Marketo]实例的唯一标识符。 |
| `clientId` | [!DNL Marketo]实例的唯一客户端ID。 |
| `clientSecret` | [!DNL Marketo]实例的唯一客户端密钥。 |

有关获取这些值的详细信息，请参阅[[!DNL Marketo] 身份验证指南](../../../../connectors/adobe-applications/marketo/marketo-auth.md)。

收集所需的凭据后，您可以按照下一部分中的步骤操作。

## 连接您的[!DNL Marketo]帐户

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;*Adobe应用程序*&#x200B;类别下，选择&#x200B;**[!UICONTROL Marketo Engage]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 一旦存在经过身份验证的帐户，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![已选择Marketo Engage源的源目录。](../../../../images/tutorials/create/marketo/catalog.png)

此时会显示&#x200B;**[!UICONTROL Connect Marketo Engage帐户]**&#x200B;页面。 在此页面上，您可以使用新帐户或访问现有帐户。

>[!BEGINTABS]

>[!TAB 创建新帐户]

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，并提供名称、可选描述和您的凭据。

完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![用于验证新Marketo帐户的新帐户接口。](../../../../images/tutorials/create/marketo/new.png)

>[!TAB 使用现有帐户]

若要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后从现有帐户目录中选择要使用的帐户。

选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有的帐户界面，您可以在其中选择现有的Marketo帐户。](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## 选择数据集

创建[!DNL Marketo]帐户后，下一步将为您提供一个用于浏览[!DNL Marketo]数据集的界面。

界面的左半部分是一个目录浏览器，显示10 [!DNL Marketo]个数据集。 完全正常的[!DNL Marketo]源连接需要摄取9个不同的数据集。 如果您还使用[!DNL Marketo]基于帐户的营销(ABM)功能，则还必须创建第10个数据流以摄取[!UICONTROL 命名帐户]数据集。

>[!NOTE]
>
>为了简单起见，以下教程使用[!UICONTROL 机会]作为示例，但下面列出的步骤适用于10个[!DNL Marketo]数据集中的任意一个。

选择要摄取的数据集。 这将更新界面以显示数据集的预览。 完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![预览界面](../../../../images/tutorials/create/marketo/preview.png)

## 提供数据集和数据流详细信息 {#provide-dataset-and-dataflow-details}

接下来，您必须提供有关数据集和数据流的信息。

### 数据集详细信息 {#dataset-details}

数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。成功引入Experience Platform的数据将作为数据集存储在数据湖中。 在此步骤中，您可以创建新数据集或使用现有数据集。

>[!BEGINTABS]

>[!TAB 使用新数据集]

要使用新数据集，请选择&#x200B;**[!UICONTROL 新数据集]**，然后为您的数据集提供名称和可选描述。 您还必须选择数据集所遵循的体验数据模型(XDM)架构。

![新的数据集选择界面。](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB 使用现有数据集]

如果您已经有一个现有数据集，请选择&#x200B;**[!UICONTROL 现有数据集]**，然后使用&#x200B;**[!UICONTROL 高级搜索]**&#x200B;选项查看组织中所有数据集的窗口，包括其各自的详细信息，例如，是否启用它们以摄取到Real-time Customer Profile。

![现有数据集选择界面。](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### 数据流配置 {#dataflow-configurations}

>[!IMPORTANT]
>
>[!DNL Marketo]源使用批处理摄取来摄取所有历史记录，并使用流式摄取进行实时更新。 这允许源在摄取任何错误记录时继续流式传输。 启用&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换开关，然后将[!UICONTROL 错误阈值%]设置为最大值，以防止数据流失败。

如果您的数据集启用了实时客户个人资料，那么在此步骤中，您可以切换&#x200B;**[!UICONTROL 个人资料数据集]**&#x200B;以启用您的数据以进行个人资料摄取。 您还可以使用此步骤启用&#x200B;**[!UICONTROL 错误诊断]**&#x200B;和&#x200B;**[!UICONTROL 部分摄取]**。

* **[!UICONTROL 错误诊断]**：选择&#x200B;**[!UICONTROL 错误诊断]**&#x200B;以指示源生成错误诊断，以便以后在监视数据集活动和数据流状态时可以引用这些诊断。
* **[!UICONTROL 部分摄取]**： [部分批次摄取](../../../../../ingestion/batch-ingestion/partial.md)能够摄取包含错误的数据，最多可达到特定可配置阈值。 此功能允许您成功地将所有准确的数据提取到Experience Platform中，同时将所有不正确的数据与有关其无效原因的信息单独进行批处理。

在此步骤中，您可以启用&#x200B;**[!UICONTROL 示例数据流]**&#x200B;以限制数据摄取，并避免摄取所有历史数据（包括人员身份）所产生的额外成本。

>[!BEGINSHADEBOX]

**使用示例数据流的快速指南**

示例数据流是您可以为[!DNL Marketo]数据流设置的配置，用于限制摄取率，然后尝试使用Experience Platform功能而无需摄取大量数据。

* 启用示例数据流，通过在回填作业期间摄取最多10万条记录（从最大的记录ID）或最多10天的活动，来限制历史数据。
* 为所有B2B实体使用示例数据流配置时，您必须考虑可能缺少某些相关记录，因为未摄取源数据的整个历史记录。

>[!ENDSHADEBOX]

![数据流详细信息页面的数据流配置部分。](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

此外，如果您正在从公司数据集中摄取数据，则可以启用&#x200B;**[!UICONTROL 排除无人认领的帐户]**&#x200B;以从摄取中排除无人认领的帐户。

当个人填写表单时，[!DNL Marketo]会根据不包含其他数据的公司名称创建虚拟帐户记录。 对于新数据流，默认情况下会启用排除无人认领帐户的切换功能。 对于现有数据流，您可以启用或禁用该功能，所做的更改将应用于新摄取的数据，而不应用于现有数据。

![排除无人认领的帐户](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## 将[!DNL Marketo]数据集源字段映射到目标XDM字段

此时将显示[!UICONTROL 映射]步骤，该步骤为您提供了一个接口，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

每个[!DNL Marketo]数据集都有其自身的特定映射规则要遵循。 有关如何将[!DNL Marketo]数据集映射到XDM的更多信息，请参阅以下内容：

* [活动](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [项目](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [计划成员资格](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [公司](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [静态列表](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [静态列表成员资格](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [指定帐户](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [机会](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [机会联系人角色](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [人员](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射界面的完整步骤，请参阅[数据准备UI指南](../../../../../data-prep/ui/mapping.md)。

![Marketo数据的映射接口。](../../../../images/tutorials/create/marketo/mapping.png)

映射集准备就绪后，选择&#x200B;**[!UICONTROL 下一步]**，等待片刻再创建新数据流。

## 查看您的数据流

将显示&#x200B;**[!UICONTROL 审核]**&#x200B;步骤，允许您在创建新数据流之前对其进行审核。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源类型、所选源实体的相关路径以及该源实体中的列数。
* **[!UICONTROL 分配数据集和映射字段]**：显示要将源数据摄取到哪个数据集，包括数据集所遵循的架构。

查看数据流后，选择&#x200B;**[!UICONTROL 保存并摄取]**，然后等待一些时间来创建数据流。

![可在引入之前确认数据流详细信息的审核页面。](../../../../images/tutorials/create/marketo/review.png)

## 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的详细信息，请参阅有关UI中[监视数据流的教程](../../../../../dataflows/ui/monitor-sources.md)。

## 删除您的属性

无法以追溯方式隐藏或删除数据集中的自定义属性。 如果要从现有数据集中隐藏或移除自定义属性，则必须创建一个没有此自定义属性的新数据集和新的XDM架构，并为您创建的新数据集配置新数据流。 您还必须禁用或删除原始数据流，该数据流包含具有要隐藏或删除的自定义属性的数据集。

## 删除您的数据流

您可以删除不再必需的数据流或使用[!UICONTROL 数据流]工作区中提供的&#x200B;**[!UICONTROL 删除]**&#x200B;功能错误地创建的数据流。 有关如何删除数据流的详细信息，请参阅有关[在UI中删除数据流](../../delete.md)的教程。

## 后续步骤

通过学习本教程，您已成功创建了一个数据流以将B2B数据从[!DNL Marketo Engage]源摄取到Experience Platform。

## 附录 {#appendix}

以下部分提供了在使用[!DNL Marketo]源时可能遵循的其他准则。

### UI中的错误消息 {#error-messages}

当Experience Platform检测到您的设置存在问题时，UI中会显示以下错误消息：

#### [!DNL Munchkin ID]未映射到相应的组织

如果您的[!DNL Munchkin ID]未映射到您正在使用的Experience Platform组织，则身份验证将被拒绝。 使用[[!DNL Marketo] 接口](https://app-sjint.marketo.com/#MM0A1)配置[!DNL Munchkin ID]与组织之间的映射。

![显示未将Marketo实例正确映射到Adobe组织的错误消息。](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### 缺少主要身份

如果缺少主标识，数据流将无法保存和摄取。 在尝试配置数据流之前，请确保XDM架构](../../../../../xdm/tutorials/create-schema-ui.md)中存在[主标识。

![一条错误消息，显示XDM架构中缺少主标识。](../../../../images/tutorials/create/marketo/no-primary-identity.png)

