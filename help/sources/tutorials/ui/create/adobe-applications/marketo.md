---
keywords: Experience Platform；主页；热门主题；Marketo源连接器；Marketo连接器；Marketo源；Marketo
solution: Experience Platform
title: 在UI中创建Marketo Engage源连接器
topic-legacy: overview
type: Tutorial
description: 本教程提供了在UI中创建Marketo Engage源连接器以将B2B数据导入Adobe Experience Platform的步骤。
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
translation-type: tm+mt
source-git-commit: 5322adb4b3a244de92300e7ce9d942ad4b968454
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 0%

---

# （测试版）在UI中创建[!DNL Marketo Engage]源连接器

>[!IMPORTANT]
>
>[!DNL Marketo Engage]源当前处于测试状态。 功能和文档是主题更改。 此外，在测试项目使用连接器时，您必须确保使用的是非生产沙箱。 有关沙箱的详细信息，请参阅[沙箱文档](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=en#understanding-sandboxes)。

本教程提供了在UI中创建[!DNL Marketo Engage]（以下称“[!DNL Marketo]”）源连接器以将消费者数据导入Adobe Experience Platform的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [体验数据模型(XDM)](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [在UI中创建和编辑模式](../../../../../xdm/ui/resources/schemas.md):了解如何在UI中创建和编辑模式。
* [身份命名空间](../../../../../identity-service/namespaces.md):身份命名空间是身份 [!DNL Identity Service] 相关上下文的一个组成部分。完全限定标识包括ID值和命名空间。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

### 收集所需凭据

要在平台上访问您的[!DNL Marketo]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `munchkinId` | Munchkin ID是特定[!DNL Marketo]实例的唯一标识符。 |
| `clientId` | [!DNL Marketo]实例的唯一客户端ID。 |
| `clientSecret` | [!DNL Marketo]实例的唯一客户端机密。 |

有关获取这些值的详细信息，请参阅[[!DNL Marketo] 身份验证指南](../../../../connectors/adobe-applications/marketo/marketo-auth.md)。

收集所需凭据后，您可以执行下一节中的步骤。

## 连接您的[!DNL Marketo]帐户

在平台UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示了可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索栏找到要处理的特定源。

在[!UICONTROL Adobe applications]类别下，选择&#x200B;**[!UICONTROL Marketo Engage]**。 然后，选择&#x200B;**[!UICONTROL Add data]**&#x200B;以创建新的[!DNL Marketo]数据流。

![目录](../../../../images/tutorials/create/marketo/catalog.png)

将显示&#x200B;**[!UICONTROL Connect to Marketo Engage]**&#x200B;页。 在此页面上，您可以使用新帐户或访问现有帐户。

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL New account]**。 在显示的输入表单上，提供帐户名、可选说明和您的[!DNL Marketo]身份验证凭据。 完成后，选择&#x200B;**[!UICONTROL Connect to source]**，然后为新连接建立留出一些时间。

![new-account](../../../../images/tutorials/create/marketo/new.png)

### 现有帐户

要使用现有帐户创建数据流，请选择&#x200B;**[!UICONTROL Existing account]**，然后选择要使用的[!DNL Marketo]帐户。 选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/marketo/existing.png)

## 选择数据集

创建[!DNL Marketo]帐户后，下一步将提供一个界面，供您浏览[!DNL Marketo]数据集。

界面的左半部分是目录浏览器，显示10个[!DNL Marketo]数据集。 全功能[!DNL Marketo]源连接需要获取9个不同的数据集。 如果您还使用[!DNL Marketo]基于帐户的营销(ABM)功能，则还必须创建第10个数据流以收集[!UICONTROL Named Accounts]数据集。

>[!NOTE]
>
>为了简便起见，以下教程以[!UICONTROL Named Accounts]为例，但下面概述的步骤适用于10个[!DNL Marketo]数据集中的任何一个。

先选择要收录的数据集，然后选择&#x200B;**[!UICONTROL Next]**。

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## 将[!DNL Marketo]模式映射到平台

出现[!UICONTROL Mapping]步骤，提供一个接口将[!DNL Marketo]模式映射到平台。

为要摄取的入站数据选择数据集。 您可以使用现有数据集或创建新数据集。

### 使用现有数据集

要将数据收录到现有数据集中，请选择&#x200B;**[!UICONTROL Existing dataset]**，然后选择数据集图标。

![existing-dataset](../../../../images/tutorials/create/marketo/existing-dataset.png)

出现&#x200B;**[!UICONTROL Select dataset]**&#x200B;对话框。 找到具有您要使用的相应模式的数据集，选择它，然后选择&#x200B;**[!UICONTROL Confirm]**。

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### 使用新数据集

要将数据收录到新数据集中，请选择&#x200B;**[!UICONTROL New dataset]**，并在提供的字段中输入数据集的名称和说明。

您可以通过在&#x200B;**[!UICONTROL Select schema]**&#x200B;搜索栏中输入模式名称来搜索该应用程序。 您还可以选择下拉图标来查看现有模式的列表。 或者，您也可以选择&#x200B;**[!UICONTROL Advanced search]**&#x200B;访问现有模式的页面，包括其各自的详细信息。

切换&#x200B;**[!UICONTROL Profile dataset]**&#x200B;按钮，为[!DNL Profile]启用目标数据集，从而使您能够创建实体属性和行为的整体视图。 所有[!DNL Profile]启用数据集中的数据将包含在[!DNL Profile]中，并在保存数据流时应用更改。

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

选择模式后，向下滚动以视图映射对话框，将[!DNL Marketo]数据集字段映射到相应的目标XDM字段。

### 将[!DNL Marketo]数据集源字段映射到目标XDM字段

每个[!DNL Marketo]数据集都有其自己的特定映射规则要遵循。 有关如何将[!DNL Marketo]数据集映射到XDM的更多信息，请参阅以下内容：

* [活动](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [程序](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [项目会员资格](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [公司](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [静态列表](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [静态列表成员关系](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [指定帐户](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [机会](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [机会联系角色](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [人](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

选择&#x200B;**[!UICONTROL Preview data]**&#x200B;可查看基于所选数据集的映射结果。

![映射](../../../../images/tutorials/create/marketo/mapping.png)

[!UICONTROL Preview]快显窗口为您提供一个界面，用于浏览所选数据集中最多100行样本数据的映射结果。

![预览](../../../../images/tutorials/create/marketo/mapping-preview.png)

将源字段映射到相应的目标字段后，请选择&#x200B;**[!UICONTROL Close]**。

## 提供数据流详细信息

将显示[!UICONTROL Dataflow detail]步骤，允许您提供有关新数据流的名称和简短说明。

![数据流详细信息](../../../../images/tutorials/create/marketo/dataflow-detail.png)

启用&#x200B;**[!UICONTROL Error diagnostics]**&#x200B;切换，可为新收录的批生成详细的错误消息，您可以使用API下载这些消息。 有关详细信息，请参阅教程[检索数据摄取错误诊断](../../../../../ingestion/quality/error-diagnostics.md)。

![错误](../../../../images/tutorials/create/marketo/errors.png)

[!DNL Marketo]连接器使用批处理摄取来摄取所有历史记录，并使用流摄取来进行实时更新。 这允许连接器在接收任何错误记录时继续流化。 启用&#x200B;**[!UICONTROL Partial ingestion]**&#x200B;切换，然后将[!UICONTROL Error threshold %]设置为最大值以防止数据流失败。

**[!UICONTROL Partial ingestion]** 提供了收录包含错误且达到特定阈值的数据的功能。有关详细信息，请参阅[部分批摄取概述](../../../../../ingestion/batch-ingestion/partial.md)。

提供数据流详细信息并将错误阈值设置为max后，请选择&#x200B;**[!UICONTROL Next]**。

![部分摄取](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## 查看数据流

将显示&#x200B;**[!UICONTROL Review]**&#x200B;步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL Connection]**:显示源类型、所选源实体的相关路径以及该源实体中的列数。
* **[!UICONTROL Assign dataset & map fields]**:显示接收源数据的模式集，包括数据集附带的数据集。

查看数据流后，请选择&#x200B;**[!UICONTROL Finish]**&#x200B;并允许一段时间创建数据流。

![审查](../../../../images/tutorials/create/marketo/review.png)

## 监控数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的详细信息，请参阅有关[在UI](../../../../../dataflows/ui/monitor-sources.md)中监视数据流的教程。

## 删除属性

不能逆向隐藏或删除数据集中的自定义属性。 如果要隐藏或删除现有数据集中的自定义属性，则必须创建一个没有此自定义属性的新数据集，一个新的XDM模式，并为您创建的新数据集配置一个新数据流。 您还必须禁用或删除包含具有要隐藏或删除的自定义属性的数据集的原始数据流。

## 删除数据流

您可以删除不再需要的或使用[!UICONTROL Dataflows]工作区中可用的&#x200B;**[!UICONTROL Delete]**&#x200B;函数创建错误的数据流。 有关如何删除数据流的详细信息，请参阅有关在UI](../../delete.md)中删除数据流的教程。[

## 后续步骤

通过本教程，您已成功创建了一个数据流以导入[!DNL Marketo]数据。 现在，下游平台服务（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用传入数据。 有关更多详细信息，请参阅以下文档:

* [[!DNL Real-time Customer Profile] 概述](../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../data-science-workspace/home.md)
