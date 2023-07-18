---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件；联合架构；联合配置文件
title: Real-Time Customer Profile用户界面指南
description: Real-time Customer Profile可以为每位客户创建整体视图，结合来自多个渠道（包括在线、离线、CRM和第三方数据）的数据。 本文档用作在Adobe Experience Platform用户界面中与Real-time Customer Profile交互的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '2008'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] UI指南

[!DNL Real-Time Customer Profile] 为每个客户创建整体视图，结合来自多个渠道（包括在线、离线、CRM和第三方数据）的数据。 本文档可用作与交互的指南 [!DNL Real-Time Customer Profile] Adobe Experience Platform用户界面(UI)中的数据。

## 快速入门

本UI指南要求您了解各种 [!DNL Experience Platform] 与管理有关的服务 [!DNL Real-Time Customer Profiles]. 在阅读本指南或使用UI之前，请查看以下服务的文档：

* [[!DNL Real-Time Customer Profile] 概述](../home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [[!DNL Identity Service]](../../identity-service/home.md)：启用 [!DNL Real-Time Customer Profile] 在引入身份时，通过桥接来自不同数据源的身份 [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。

## [!UICONTROL 概述]

在Experience PlatformUI中，选择 **[!UICONTROL 配置文件]** 在左侧导航中打开 **[!UICONTROL 概述]** 选项卡显示配置文件仪表板。

>[!NOTE]
>
>如果您的组织是初次使用Platform，但尚未创建活动配置文件数据集或合并策略，则 [!UICONTROL 配置文件] 仪表板不可见。 相反， [!UICONTROL 概述] 选项卡显示链接和文档，以帮助您开始使用Real-Time Customer Profile。

### 配置文件仪表板 {#profile-dashboard}

配置文件仪表板概述了与贵组织的配置文件数据相关的关键量度。

要了解更多信息，请访问 [个人资料仪表板指南](../../dashboards/guides/profiles.md).

![此时将显示“配置文件”仪表板。](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL 浏览] 选项卡量度

选择 **[!UICONTROL 浏览]** 选项卡以显示与贵组织的配置文件数据相关的多个量度。 您还可以使用此选项卡来浏览使用合并策略或标识的配置文件存储区，如本指南下一节中所述。

在右侧 **[!UICONTROL 浏览]** 选项卡是 [配置文件计数](#profile-count) 以及列表 [按命名空间列出的配置文件](#profiles-by-namespace).

>[!NOTE]
>
>这些配置文件量度可能与 [配置文件仪表板](#profile-dashboard) 因为它们是使用贵组织的默认合并策略进行评估的。 有关使用合并策略的更多信息，包括如何定义默认合并策略，请参阅 [合并策略概述](../merge-policies/overview.md).

除了这些量度之外，此部分还提供上次更新的日期和时间，显示上次评估量度的时间。

![此时会显示并突出显示配置文件量度。](../images/user-guide/browse-metrics.png)

### 配置文件计数 {#profile-count}

配置文件计数显示贵组织在默认合并Experience Platform中将配置文件片段合并在一起，以便为每个单独客户形成一个配置文件后，在该策略下拥有的配置文件总数。 换言之，您的组织可能具有多个与跨不同渠道与您的品牌进行交互的单个客户相关的配置文件片段，但这些片段将合并在一起（根据默认合并策略），并将返回计数“1”个配置文件，因为它们都与同一个人相关。

配置文件计数还包括具有属性（记录数据）的用户档案，以及仅包含时间序列（事件）数据(如Adobe Analytics配置文件)的用户档案。 用户档案计数会定期刷新，以提供Platform内最新的用户档案总数。

#### 更新用户档案计数量度

当将记录摄取到 [!DNL Profile] 存储区计数增加或减少超过5%，将触发作业以更新计数。 对于流数据工作流，会每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果存在，则会自动触发作业以更新用户档案计数。 对于批量摄取，在成功将批次摄取到配置文件存储区后15分钟内，如果满足5%的增加或减少阈值，则会运行作业以更新配置文件计数。

### [!UICONTROL 按命名空间列出的配置文件] {#profiles-by-namespace}

此 **[!UICONTROL 按命名空间列出的配置文件]** 量度显示配置文件存储区中所有合并的配置文件中的命名空间的总计数和划分。 按命名空间划分的配置文件总数（即为每个命名空间显示的值相加）将始终高于配置文件计数量度，因为一个配置文件可能具有多个关联的命名空间。 例如，如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个人客户关联。

#### 更新 [!UICONTROL 按命名空间列出的配置文件] 量度

与 [配置文件计数](#profile-count) 量度，当将记录摄取到 [!DNL Profile] 存储增加或减少计数超过5%，将触发作业以更新命名空间量度。 对于流数据工作流，会每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果存在，则会自动触发作业以更新用户档案计数。 对于批量摄取，请在成功将批次摄取到 [!DNL Profile] 存储，如果满足5%增加或减少阈值，则运行作业以更新量度。

## 使用 [!UICONTROL 浏览] 选项卡以查看配置文件

在 **[!UICONTROL 浏览]** 选项卡，您可以使用合并策略查看示例配置文件，或使用身份命名空间和值查找特定配置文件。

![此时将显示属于该组织的配置文件。](../images/user-guide/none-selected.png)

### 浏览方式 [!UICONTROL 合并策略]

此 **[!UICONTROL 浏览]** 选项卡。默认情况下，该选项卡设置为组织的默认合并策略。 要选择其他合并策略，请选择 `X` ，然后使用选择器打开 **[!UICONTROL 选择合并策略]** 对话框。

>[!NOTE]
>
>如果未选择合并策略，请使用 **[!UICONTROL 合并策略]** 字段以打开选择对话框。

![合并策略选择器会突出显示。](../images/user-guide/browse-by-merge-policy.png)

要从 **[!UICONTROL 选择合并策略]** 对话框中，选择策略名称旁边的单选按钮，然后使用 **[!UICONTROL 选择]** 以返回 [!UICONTROL 浏览] 选项卡。 然后，您可以选择 **[!UICONTROL 视图]** 刷新示例配置文件并查看应用了新合并策略的配置文件采样。

![将显示一个对话框，您可以在其中选择要作为筛选依据的合并策略。](../images/user-guide/select-merge-policy.png)

显示的配置文件表示在应用所选合并策略后，您组织的配置文件存储区中最多有20个配置文件的示例。 将新数据添加到贵组织的配置文件存储区后，将刷新所选合并策略的示例配置文件。

要查看其中一个示例配置文件的详细信息，请选择 **[!UICONTROL 配置文件ID]**. 有关更多信息，请参阅本指南后面关于 [查看配置文件详细信息](#profile-detail).

![将显示与合并策略匹配的示例配置文件。](../images/user-guide/sample-profiles.png)

要详细了解合并策略及其在Platform中的角色，请参阅 [合并策略概述](../merge-policies/overview.md).

### 浏览方式 [!UICONTROL 身份] {#browse-identity}

在 **[!UICONTROL 浏览]** 选项卡，您可以使用身份命名空间，以便按身份值查找特定配置文件。 按身份浏览要求您提供合并策略、身份命名空间和身份值。

![合并策略选择器会突出显示。](../images/user-guide/browse-by-merge-policy.png)

如有必要，请使用 **[!UICONTROL 合并策略]** 选择器以打开 **[!UICONTROL 选择合并策略]** 对话框，然后选择要使用的合并策略。

![将显示一个对话框，您可以在其中选择要作为筛选依据的合并策略。](../images/user-guide/select-merge-policy.png)

然后使用 **[!UICONTROL 身份命名空间]** 选择器以打开 **[!UICONTROL 选择身份命名空间]** 对话框，并选择要搜索的命名空间。 如果贵组织具有多个命名空间，则可以使用对话框中的搜索栏开始键入命名空间的名称。

您可以选择命名空间以查看其他详细信息，也可以选择单选按钮来选择命名空间。 然后，您可以使用 **[!UICONTROL 选择]** 以继续。

![将显示一个对话框，您可以在其中选择要作为筛选依据的身份命名空间。](../images/user-guide/select-identity-namespace.png)

选择 [!UICONTROL 身份命名空间] 并返回 [!UICONTROL 浏览] 选项卡，您可以输入 **[!UICONTROL 标识值]** 与所选的命名空间相关。

>[!NOTE]
>
>此值特定于单个客户配置文件，并且必须是所提供命名空间的有效条目。 例如，选择身份命名空间“Email”将需要有效电子邮件地址形式的身份值。

![要作为筛选依据的身份值会突出显示。](../images/user-guide/filter-identity-value.png)

输入值后，选择 **[!UICONTROL 视图]** 并返回一个与值匹配的配置文件。 选择 **[!UICONTROL 配置文件ID]** 查看配置文件详细信息。

![与标识值匹配的配置文件会突出显示。](../images/user-guide/filtered-identity-value.png)

## 查看配置文件详细信息 {#profile-detail}

选择 **[!UICONTROL 配置文件ID]**，则 **[!UICONTROL 详细信息]** 选项卡打开。 配置文件信息显示在 **[!UICONTROL 详细信息]** 选项卡已从多个配置文件片段合并在一起，以形成单个客户的视图。 这包括客户详细信息，如基本属性、链接身份和渠道偏好设置。

显示的默认字段也可以在组织级别更改以显示首选用户档案属性。 要了解有关自定义这些字段的更多信息（包括添加和删除属性以及调整仪表板面板大小的分步说明），请阅读 [配置文件详细信息自定义指南](profile-customization.md).

![Details （详细信息）选项卡会突出显示。 将显示配置文件详细信息。](../images/user-guide/profile-detail.png)

您可以通过选择另一个可用选项卡，查看与单个客户配置文件相关的附加信息。 这些选项卡包括属性、事件和受众成员资格选项卡，该选项卡显示配置文件当前符合条件的受众。

### “属性”选项卡

此 **[!UICONTROL 属性]** 选项卡提供一个列表视图，其中汇总了应用指定的合并策略后与单个配置文件相关的所有属性。

这些属性也可以通过选择 **[!UICONTROL 查看JSON]**. 对于希望更好地了解如何将配置文件属性摄取到Platform的任何用户，此功能非常有用。

![“属性”选项卡会突出显示。 此时会显示配置文件属性。](../images/user-guide/attributes.png)

### “事件”选项卡

此 **[!UICONTROL 事件]** 选项卡包含来自与客户关联的100个最新ExperienceEvents的数据。 此数据可能包括电子邮件打开次数、购物车活动和页面查看次数。 选择 **[!UICONTROL 查看全部]** 对于任何单个事件，都会在事件过程中提供额外的字段和值捕获。

通过选择以，事件也可以查看为JSON对象 **[!UICONTROL 查看JSON]**. 这有助于了解如何在Platform中捕获事件。

![Events选项卡高亮显示。 此时会显示配置文件事件。](../images/user-guide/events.png)

### “受众成员资格”选项卡

此 **[!UICONTROL 受众会员资格]** 选项卡显示一个列表，其中包含单个客户配置文件当前所属受众的名称和描述。 当配置文件符合受众资格或过期时，此列表会自动更新。 用户档案当前符合条件的受众总数将显示在选项卡的右侧。

有关Experience Platform分段的更多信息，请参阅 [AdobeExperience Platform分段服务文档](../../segmentation/home.md).

![受众成员资格选项卡会突出显示。 此时会显示用户档案的受众成员资格详细信息。](../images/user-guide/segment-membership.png)

## 合并策略

从主 **[!UICONTROL 配置文件]** 菜单中，选择 **[!UICONTROL 合并策略]** 选项卡，以查看属于贵组织的合并策略的列表。 每个列出的策略都会显示其名称（无论其是否是默认合并策略）及其应用的架构类。

有关合并策略的详细信息，请参阅 [合并策略概述](../merge-policies/overview.md).

![“合并策略”选项卡会突出显示。 将显示属于组织的合并策略。](../images/user-guide/merge-policies.png)

## 合并模式 {#union-schema}

从主 **[!UICONTROL 配置文件]** 菜单中，选择 **[!UICONTROL 合并架构]** 选项卡，以查看所摄取数据的可用合并架构。 合并模式是所有模式的合并 [!DNL Experience Data Model] (XDM)类下的字段，已启用其架构以便用于 [!DNL Real-Time Customer Profile].

有关合并模式的更多信息，请访问 [合并架构UI指南](union-schema.md).

![“合并架构”选项卡会突出显示。 将显示属于组织的合并架构。](../images/user-guide/union-schema.png)

## 计算属性 {#computed-attributes}

从主 **[!UICONTROL 配置文件]** 菜单中，选择 **[!UICONTROL 计算属性]** 选项卡，以查看属于您的组织的计算属性列表。

有关计算属性的详细信息，请阅读 [计算属性概述](../computed-attributes/overview.md). 有关如何在Platform UI中使用计算属性的更多信息，请阅读 [计算属性UI指南](../computed-attributes/ui.md).

图像

## 后续步骤

阅读本指南后，您将了解如何使用Experience PlatformUI查看和管理组织的配置文件数据。 有关如何使用Experience PlatformAPI处理配置文件数据的信息，请参阅 [Real-Time Customer Profile API指南](../api/overview.md).
