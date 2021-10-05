---
keywords: Experience Platform；主页；热门主题；Marketo源连接器；Marketo连接器；Marketo源；Marketo
solution: Experience Platform
title: 在UI中创建Marketo Engage源连接器
topic-legacy: overview
type: Tutorial
description: 本教程提供了在UI中创建Marketo Engage源连接器以将B2B数据导入Adobe Experience Platform的步骤。
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 0661d124ffe520697a1fc8e2cae7b0b61ef4edfc
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 0%

---

# （测试版）在UI中创建[!DNL Marketo Engage]源连接器

>[!IMPORTANT]
>
>Adobe Experience Platform中的[!DNL Marketo Engage]源当前为测试版。 文档和功能可能会发生更改。

本教程提供了在UI中创建[!DNL Marketo Engage]（以下称“[!DNL Marketo]”）源连接器以将B2B数据导入Adobe Experience Platform的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [体验数据模型(XDM)](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [在UI中创建和编辑架构](../../../../../xdm/ui/resources/schemas.md):了解如何在UI中创建和编辑模式。
* [身份命名空间](../../../../../identity-service/namespaces.md):身份命名空间是的组 [!DNL Identity Service] 件，用作与身份相关的上下文的指示器。完全限定的标识包括ID值和命名空间。
* [[!DNL Real-time Customer Profile]](/help/profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

要在Platform上访问您的[!DNL Marketo]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `munchkinId` | Munchkin ID是特定[!DNL Marketo]实例的唯一标识符。 |
| `clientId` | [!DNL Marketo]实例的唯一客户端ID。 |
| `clientSecret` | [!DNL Marketo]实例的唯一客户端密钥。 |

有关获取这些值的更多信息，请参阅[[!DNL Marketo] 身份验证指南](../../../../connectors/adobe-applications/marketo/marketo-auth.md)。

收集所需的凭据后，即可执行下一节中的步骤。

## 连接[!DNL Marketo]帐户

在平台UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在[!UICONTROL Adobe应用程序]类别下，选择&#x200B;**[!UICONTROL Marketo Engage]**。 然后，选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的[!DNL Marketo]数据流。

![目录](../../../../images/tutorials/create/marketo/catalog.png)

出现&#x200B;**[!UICONTROL 连接到Marketo Engage]**&#x200B;页面。 在此页面上，您可以使用新帐户或访问现有帐户。

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新建帐户]**。 在显示的输入窗体中，提供帐户名称、可选描述和您的[!DNL Marketo]身份验证凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后允许一些时间建立新连接。

![新帐户](../../../../images/tutorials/create/marketo/new.png)

### 现有帐户

要使用现有帐户创建数据流，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后选择要使用的[!DNL Marketo]帐户。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/marketo/existing.png)

## 选择数据集

创建[!DNL Marketo]帐户后，下一步会提供一个界面，供您浏览[!DNL Marketo]数据集。

界面的左半部分是目录浏览器，显示10个[!DNL Marketo]数据集。 要实现[!DNL Marketo]源连接的完全正常运行，需要摄取九个不同的数据集。 如果您还使用[!DNL Marketo]基于帐户的营销(ABM)功能，则还必须创建第10个数据流以摄取[!UICONTROL 命名帐户]数据集。

>[!NOTE]
>
>为简便起见，以下教程以[!UICONTROL 命名帐户]为例，但下面概述的步骤适用于10个[!DNL Marketo]数据集中的任意一个。

选择要先摄取的数据集，然后选择&#x200B;**[!UICONTROL Next]**。

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## 将[!DNL Marketo]架构映射到平台

将显示[!UICONTROL 映射]步骤，提供一个接口将[!DNL Marketo]架构映射到平台。

为要摄取到的入站数据选择数据集。 您可以使用现有数据集或创建新数据集。

### 使用现有数据集

要将数据摄取到现有数据集，请选择&#x200B;**[!UICONTROL 现有数据集]**，然后选择数据集图标。

![现有数据集](../../../../images/tutorials/create/marketo/existing-dataset.png)

出现&#x200B;**[!UICONTROL 选择数据集]**&#x200B;对话框。 找到包含您要使用的相应架构的数据集，将其选中，然后选择&#x200B;**[!UICONTROL Confirm]**。

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### 使用新数据集

要将数据摄取到新数据集，请选择&#x200B;**[!UICONTROL New dataset]** ，然后在提供的字段中输入数据集的名称和说明。

您可以在&#x200B;**[!UICONTROL 选择架构]**&#x200B;搜索栏中输入其名称，以搜索架构。 您还可以选择下拉图标以查看现有架构的列表。 或者，您也可以选择&#x200B;**[!UICONTROL 高级搜索]**&#x200B;以访问现有架构的页面，包括其各自的详细信息。

切换&#x200B;**[!UICONTROL 配置文件数据集]**&#x200B;按钮以为[!DNL Profile]启用目标数据集，从而允许您创建实体属性和行为的整体视图。 所有启用[!DNL Profile]的数据集中的数据都将包含在[!DNL Profile]中，并在保存数据流时应用更改。

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

选择架构后，向下滚动以查看映射对话框，以开始将[!DNL Marketo]数据集字段映射到相应的目标XDM字段。

### 将[!DNL Marketo]数据集源字段映射到XDM字段

每个[!DNL Marketo]数据集都有其自己的特定映射规则要遵循。 有关如何将[!DNL Marketo]数据集映射到XDM的更多信息，请参阅以下内容：

* [活动](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [程序](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [方案成员资格](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [公司](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [静态列表](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [静态列表成员关系](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [指定帐户](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [机会](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [机会联系角色](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [人员](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

选择&#x200B;**[!UICONTROL 预览数据]**&#x200B;以查看基于选定数据集的映射结果。

![映射](../../../../images/tutorials/create/marketo/mapping.png)

[!UICONTROL 预览]弹出窗口提供了一个界面，用于浏览来自选定数据集的最多100行示例数据的映射结果。

![预览](../../../../images/tutorials/create/marketo/mapping-preview.png)

将源字段映射到相应的目标字段后，请选择&#x200B;**[!UICONTROL 关闭]**。

## 提供数据流详细信息

出现[!UICONTROL 数据流详细信息]步骤，允许您提供有关新数据流的名称和简要说明。

![数据流详细信息](../../../../images/tutorials/create/marketo/dataflow-detail.png)

启用&#x200B;**[!UICONTROL 错误诊断]**&#x200B;切换开关，以允许为新摄取的批次生成详细的错误消息，您可以使用API下载这些消息。 有关更多信息，请参阅[检索数据摄取错误诊断](../../../../../ingestion/quality/error-diagnostics.md)的教程。

![错误](../../../../images/tutorials/create/marketo/errors.png)

[!DNL Marketo]连接器使用批量摄取来摄取所有历史记录，并使用流式摄取来进行实时更新。 这允许连接器在摄取任何错误记录时继续流式传输。 启用&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换开关，然后将[!UICONTROL 错误阈值%]设置为最大值，以防止数据流失败。

**[!UICONTROL 部分]** 摄取提供了摄取包含错误且达到特定阈值的数据的功能。有关更多信息，请参阅[部分批量摄取概述](../../../../../ingestion/batch-ingestion/partial.md)。

提供数据流详细信息并将错误阈值设置为max后，请选择&#x200B;**[!UICONTROL Next]**。

![部分摄取](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## 查看数据流

此时会出现&#x200B;**[!UICONTROL Review]**&#x200B;步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源类型、所选源实体的相关路径以及该源实体中的列数。
* **[!UICONTROL 分配数据集和映射字段]**:显示源数据被摄取到的数据集，包括该数据集附加的架构。

审核数据流后，选择&#x200B;**[!UICONTROL 完成]**&#x200B;并为创建数据流留出一些时间。

![审查](../../../../images/tutorials/create/marketo/review.png)

## 监控数据流

创建数据流后，您可以监控通过其摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监控数据流的更多信息，请参阅关于[在UI](../../../../../dataflows/ui/monitor-sources.md)中监控数据流的教程。

## 删除属性

数据集中的自定义属性不能以追溯方式隐藏或删除。 如果要隐藏或删除现有数据集中的自定义属性，则必须创建一个没有此自定义属性的新数据集、一个新的XDM架构，并为您创建的新数据集配置新的数据流。 您还必须禁用或删除原始数据流，该数据流包含具有您要隐藏或删除的自定义属性的数据集。

## 删除数据流

您可以删除不再需要或使用[!UICONTROL 数据流]工作区中提供的&#x200B;**[!UICONTROL Delete]**&#x200B;函数错误地创建的数据流。 有关如何删除数据流的更多信息，请参阅有关[在UI](../../delete.md)中删除数据流的教程。

## 后续步骤

在本教程中，您已成功创建了一个数据流以导入[!DNL Marketo]数据。 现在，下游Platform服务（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用传入数据。 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-time Customer Profile] 概述](/help/profile/home.md)
* [[!DNL Data Science Workspace] 概述](/help/data-science-workspace/home.md)
