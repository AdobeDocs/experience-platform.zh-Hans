---
keywords: Experience Platform；主页；IAB;IAB 2.0；同意；同意
solution: Experience Platform
title: 为捕获IAB TCF 2.0同意数据创建数据集
topic-legacy: privacy events
description: 本文档提供了设置两个收集IAB TCF 2.0同意数据所需的数据集的步骤。
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: 656d772335c2f5ae58b471b31bfbd6dfa82490cd
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 0%

---

# 创建用于捕获IAB TCF 2.0同意数据的数据集

为了使Adobe Experience Platform能够根据IAB [!DNL Transparency & Consent Framework](TCF)2.0处理客户同意数据，必须将该数据发送到架构包含TCF 2.0同意字段的数据集。

具体而言，捕获TCF 2.0同意数据需要两个数据集：

* 基于[!DNL XDM Individual Profile]类的数据集，可在[!DNL Real-time Customer Profile]中使用。
* 基于[!DNL XDM ExperienceEvent]类的数据集。

>[!IMPORTANT]
>
>平台仅强制在“单个配置文件”数据集中收集TCF字符串。 虽然在此工作流中创建数据流时仍需要ExperienceEvent数据集，但您只需将数据摄取到用户档案数据集即可。 如果您希望跟踪一段时间内的同意更改事件，仍可以使用ExperienceEvent数据集，但在强制执行区段激活时，不会使用这些值。

本文档提供了设置这两个数据集的步骤。 有关配置TCF 2.0平台数据操作的完整工作流程的概述，请参阅[IAB TCF 2.0合规性概述](./overview.md)。

## 先决条件

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [体验数据模型(XDM)](../../../../xdm/home.md):用于组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [架构组合的基础知识](../../../../xdm/schema/composition.md):了解XDM模式的基本构建块。
* [Adobe Experience Platform Identity服务](../../../../identity-service/home.md):允许您跨设备和系统从不同数据源中桥接客户身份。
   * [身份命名空间](../../../../identity-service/namespaces.md):客户身份数据必须在由Identity Service识别的特定身份命名空间下提供。
* [实时客户资料](../../../../profile/home.md):利用 [!DNL Identity Service] 此功能，您可以根据数据集实时创建详细的客户用户档案。[!DNL Real-time Customer Profile] 从数据湖中提取数据，并将客户配置文件保留在其自己的单独数据存储中。

## TCF 2.0字段组 {#field-groups}

[!UICONTROL IAB TCF 2.0同意详细信息]架构字段组提供TCF 2.0支持所需的客户同意字段。 此字段组有两个版本：一个与[!DNL XDM Individual Profile]类兼容，另一个与[!DNL XDM ExperienceEvent]类兼容。

以下各节介绍了每个字段组的结构，包括它们在摄取期间预期的数据。

### 用户档案字段组 {#profile-field-group}

对于基于[!DNL XDM Individual Profile]的架构，[!UICONTROL IAB TCF 2.0同意详细信息]字段组提供了单个映射类型字段`identityPrivacyInfo`，该字段将客户身份映射到其TCF同意首选项。 此字段组必须包含在为实时客户资料启用的基于记录的架构中，才能自动执行。

请参阅此字段组的[参考指南](../../../../xdm/field-groups/profile/iab.md) ，了解有关其结构和用例的更多信息。

### 事件字段组 {#event-field-group}

如果要跟踪随时间推移发生的同意更改事件，可以将[!UICONTROL IAB TCF 2.0同意详细信息]字段组添加到您的[!UICONTROL XDM ExperienceEvent]架构中。

如果您不打算跟踪随时间推移的同意更改事件，则无需在事件架构中包含此字段组。 自动强制实施TCF同意值时，Experience Platform仅使用摄取到[配置文件字段组](#profile-field-group)的最新同意信息。 由事件捕获的同意值不会参与自动执行工作流。

有关此字段组的结构和用例的详细信息，请参阅此字段组的[参考指南](../../../../xdm/field-groups/event/iab.md)。

## 创建客户同意架构 {#create-schemas}

要创建可捕获同意数据的数据集，您必须首先创建XDM模式以基于这些数据集。

如上节所述，为了在下游平台工作流中强制执行同意，需要使用[!UICONTROL XDM个人配置文件]类的架构。 如果您希望跟踪随时间推移的同意更改，则还可以选择根据[!UICONTROL XDM ExperienceEvent]创建单独的架构。 两个架构都必须包含`identityMap`字段和相应的TCF 2.0字段组。

在平台UI的左侧导航中，选择&#x200B;**[!UICONTROL 架构]**&#x200B;以打开[!UICONTROL 架构]工作区。 在此，请按照以下部分中的步骤创建每个必需的架构。

>[!NOTE]
>
>如果您现有的XDM架构想要用来捕获同意数据，则可以编辑这些架构，而不是创建新的架构。 但是，如果已启用现有架构以在实时客户资料中使用，则其主要标识不能是禁止在基于兴趣的广告（如电子邮件地址）中使用的直接可识别字段。 如果您不确定哪些字段受到限制，请咨询您的法律顾问。
>
>此外，在编辑现有架构时，只能进行加性（非中断）更改。 有关更多信息，请参阅[架构演变原则](../../../../xdm/schema/composition.md#evolution)一节。

### 创建用户档案同意架构 {#profile-schema}

选择&#x200B;**[!UICONTROL 创建架构]**，然后从下拉菜单中选择&#x200B;**[!UICONTROL XDM Indivial Profile]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

出现&#x200B;**[!UICONTROL 添加字段组]**&#x200B;对话框，允许您立即开始向架构添加字段组。 从此处，从列表中选择&#x200B;**[!UICONTROL IAB TCF 2.0同意详细信息]**。 您可以选择使用搜索栏来缩小结果范围，以便更轻松地找到字段组。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

接下来，从列表中找到&#x200B;**[!UICONTROL IdentityMap]**&#x200B;字段组，并将其选中。 在右边栏中列出两个字段组后，选择&#x200B;**[!UICONTROL 添加字段组]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

画布将重新出现，显示`identityPrivacyInfo`和`identityMap`字段已添加到架构结构中。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

在向架构添加更多字段之前，请选择根字段以在右边栏中显示&#x200B;**[!UICONTROL 架构属性]**，您可以在此处提供架构的名称和描述。

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

在提供了名称和描述后，您可以选择向架构添加更多字段，方法是：在画布左侧的&#x200B;**[!UICONTROL 字段组]**&#x200B;部分下选择&#x200B;**[!UICONTROL 添加]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

如果您正在编辑已启用以供在[!DNL Real-time Customer Profile]中使用的现有架构，请选择&#x200B;**[!UICONTROL Save]**&#x200B;以确认您所做的更改，然后再跳到[上的部分，该部分基于您的同意架构](#dataset)创建数据集。 如果要创建新架构，请继续执行下面子部分中列出的步骤。

#### 启用架构以在[!DNL Real-time Customer Profile]中使用

为了使Platform将其收到的同意数据与特定客户配置文件关联，必须启用同意架构以在[!DNL Real-time Customer Profile]中使用。

>[!NOTE]
>
>此部分中显示的示例架构使用其`identityMap`字段作为其主标识。 如果您希望将其他字段设置为主标识，请确保您使用的是间接标识符（如Cookie ID），而不是基于兴趣的广告中禁止使用的直接可识别字段（如电子邮件地址）。 如果您不确定哪些字段受到限制，请咨询您的法律顾问。
>
>有关如何为架构设置主标识字段的步骤可在[[!UICONTROL Schemas] UI指南](../../../../xdm/ui/fields/identity.md)中找到。

要启用[!DNL Profile]的架构，请在左边栏中选择该架构的名称，以打开&#x200B;**[!UICONTROL 架构属性]**&#x200B;部分。 从此处，选择&#x200B;**[!UICONTROL Profile]**&#x200B;切换按钮。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

出现一个弹出窗口，指示缺少主标识。 选中用于使用替代主标识的复选框，因为主标识将包含在`identityMap`字段中。

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

最后，选择&#x200B;**[!UICONTROL Save]**&#x200B;以确认更改。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### 创建事件同意架构 {#event-schema}

>[!NOTE]
>
>事件同意架构仅用于跟踪一段时间内的同意更改事件，并且不参与下游实施工作流。 如果您不希望跟踪随时间推移的同意更改，则可以跳到[创建同意数据集](#datasets)的下一部分。

在&#x200B;**[!UICONTROL 架构]**&#x200B;工作区中，选择&#x200B;**[!UICONTROL 创建架构]**，然后从下拉菜单中选择&#x200B;**[!UICONTROL XDM ExperienceEvent]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

出现&#x200B;**[!UICONTROL 添加字段组]**&#x200B;对话框。 从此处，从列表中选择&#x200B;**[!UICONTROL IAB TCF 2.0同意详细信息]**。 您可以选择使用搜索栏来缩小结果范围，以便更轻松地找到字段组。


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

接下来，从列表中找到&#x200B;**[!UICONTROL IdentityMap]**&#x200B;字段组，并将其选中。 在右边栏中列出两个字段组后，选择&#x200B;**[!UICONTROL 添加字段组]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

画布将重新出现，显示`consentStrings`和`identityMap`字段已添加到架构结构中。

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

在向架构添加更多字段之前，请选择根字段以在右边栏中显示&#x200B;**[!UICONTROL 架构属性]**，您可以在此处提供架构的名称和描述。

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

在提供了名称和描述后，您可以选择向架构添加更多字段，方法是：在画布左侧的&#x200B;**[!UICONTROL 字段组]**&#x200B;部分下选择&#x200B;**[!UICONTROL 添加]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

添加所需的字段组后，选择&#x200B;**[!UICONTROL Save]**&#x200B;即可完成。

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## 根据您的同意模式创建数据集 {#datasets}

对于上述每个必需的架构，您必须创建一个数据集，以最终摄取客户同意数据。 必须为[!DNL Real-time Customer Profile]启用基于记录架构的数据集，而基于时间系列架构&#x200B;**的数据集不应**&#x200B;启用[!DNL Profile]。

要开始，请在左侧导航中选择&#x200B;**[!UICONTROL 数据集]**，然后选择右上角的&#x200B;**[!UICONTROL 创建数据集]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

在下一页，选择&#x200B;**[!UICONTROL 从架构创建数据集]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

将显示&#x200B;**[!UICONTROL 从架构]**&#x200B;创建数据集工作流，从&#x200B;**[!UICONTROL 选择架构]**&#x200B;步骤开始。 在提供的列表中，找到您之前创建的同意架构之一。 您可以选择使用搜索栏来缩小结果范围并更轻松地查找架构。 选择所需架构旁边的单选按钮，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

此时将显示&#x200B;**[!UICONTROL 配置数据集]**&#x200B;步骤。 在选择&#x200B;**[!UICONTROL 完成]**&#x200B;之前，为数据集提供唯一且易于识别的名称和描述。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

此时会显示新创建数据集的详细信息页面。 如果数据集基于您的时间系列架构，则该过程会完成。 如果数据集基于您的记录架构，则此过程的最后一步是启用该数据集，以在[!DNL Real-time Customer Profile]中使用。

在右边栏中，选择&#x200B;**[!UICONTROL 配置文件]**&#x200B;切换开关，然后选择确认弹出窗口中的&#x200B;**[!UICONTROL 启用]**&#x200B;以启用[!DNL Profile]架构。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

如果您为数据集创建了架构，请再次按照上述步骤创建基于事件的数据集。

## 后续步骤

在本教程之后，您至少创建了一个数据集，现在可以用它来收集客户同意数据：

* 基于记录的数据集，在“实时客户资料”中启用。 **(必需)**
* 未为[!DNL Profile]启用的基于时间序列的数据集。 （可选）

现在，您可以返回到[IAB TCF 2.0概述](./overview.md#merge-policies)以继续配置Platform for TCF 2.0合规性的过程。
