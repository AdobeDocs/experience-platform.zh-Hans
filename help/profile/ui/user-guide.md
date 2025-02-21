---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件；联合架构；UNION PROFILE；联合配置文件
title: 实时客户个人资料UI指南
description: Real-time Customer Profile可以为每位客户创建整体视图，结合来自多个渠道（包括在线、离线、CRM和第三方数据）的数据。 本文档提供了在Adobe Experience Platform用户界面中与Real-time Customer Profile交互的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 4afb2c76f2022423e8f1fa29c91d02b43447ba90
workflow-type: tm+mt
source-wordcount: '2212'
ht-degree: 3%

---

# [!DNL Real-Time Customer Profile] UI 指南

[!DNL Real-Time Customer Profile]为每个客户创建整体视图，结合来自多个渠道的数据，包括在线、离线、CRM和第三方数据。 本文档用作在Adobe Experience Platform用户界面(UI)中与[!DNL Real-Time Customer Profile]数据交互的指南。

## 快速入门

此UI指南要求您了解与管理[!DNL Real-Time Customer Profiles]有关的各种[!DNL Experience Platform]服务。 在阅读本指南或使用UI之前，请查看以下服务的文档：

* [[!DNL Real-Time Customer Profile] 概述](../home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [[!DNL Identity Service]](../../identity-service/home.md)：在将[!DNL Real-Time Customer Profile]引入到[!DNL Platform]中时，通过桥接来自不同数据源的标识来启用它们。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Platform]用于组织客户体验数据的标准化框架。

## [!UICONTROL 概述]

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 配置文件]**&#x200B;以打开显示配置文件仪表板的&#x200B;**[!UICONTROL 概述]**&#x200B;选项卡。

>[!NOTE]
>
>如果您的组织是Platform的新用户，并且尚未创建活动配置文件数据集或合并策略，则[!UICONTROL 配置文件]仪表板不可见。 相反，[!UICONTROL 概述]选项卡显示链接和文档，以帮助您开始使用实时客户个人资料。

### 轮廓仪表板 {#profile-dashboard}

配置文件仪表板概述了与组织配置文件数据相关的关键量度。

若要了解详细信息，请访问[个人资料仪表板指南](../../dashboards/guides/profiles.md)。

![将显示配置文件仪表板。](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL 浏览]选项卡度量

选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡以显示与贵组织的配置文件数据相关的多个量度。 您还可以使用此选项卡使用合并策略或标识浏览配置文件存储区，如本指南下一节中所述。

**[!UICONTROL 浏览]**&#x200B;选项卡的右侧是[配置文件计数](#profile-count)以及按命名空间](#profiles-by-namespace)列出的[配置文件。

>[!NOTE]
>
>这些配置文件量度可能与[配置文件仪表板](#profile-dashboard)上显示的量度不同，因为它们是使用贵组织的默认合并策略评估的。 有关如何使用合并策略的更多信息，包括如何定义默认合并策略，请参阅[合并策略概述](../merge-policies/overview.md)。

除了这些量度之外，此部分还提供上次更新的日期和时间，以显示上次评估量度的时间。

![配置文件量度显示并突出显示。](../images/user-guide/browse-metrics.png)

### 轮廓计数 {#profile-count}

配置文件计数显示贵组织在将默认合并策略与配置文件片段合并在一起，以便为每个单独客户形成一个配置文件后，在Experience Platform中拥有的配置文件总数。 换言之，您的组织可能具有多个与跨不同渠道与您的品牌互动的单个客户相关的配置文件片段，但这些片段将合并在一起（根据默认合并策略），并将返回计数“1”个配置文件，因为它们都与同一个人相关。

配置文件计数还包括具有属性（记录数据）的用户档案，以及仅包含时间序列（事件）数据(如Adobe Analytics配置文件)的用户档案。 用户档案计数会定期刷新，以提供Platform内最新的用户档案总数。

#### 更新配置文件计数量度

当将记录摄取到[!DNL Profile]存储区后计数增加或减少超过5%时，将触发作业以更新计数。 对于流数据工作流，会每小时进行一次检查，以确定是否满足了5%的增加或减少阈值。 如果有，则会自动触发作业以更新用户档案计数。 对于批量摄取，在成功将批次摄取到配置文件存储后15分钟内，如果满足5%的增加或减少阈值，将运行作业以更新配置文件计数。

### [!UICONTROL 按命名空间列出的配置文件] {#profiles-by-namespace}

**[!UICONTROL 按命名空间列出的配置文件]**&#x200B;量度显示配置文件存储中所有合并配置文件的命名空间总数和划分情况。 按命名空间划分的配置文件总数（也就是为每个命名空间显示的值相加）将始终高于配置文件计数量度，因为一个配置文件可能具有多个关联的命名空间。 例如，如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个人客户关联。

#### 正在按命名空间]指标更新[!UICONTROL 配置文件

与[配置文件计数](#profile-count)量度类似，当将记录摄取到[!DNL Profile]存储区中的记录增加或减少计数超过5%时，将触发作业以更新命名空间量度。 对于流数据工作流，会每小时进行一次检查，以确定是否满足了5%的增加或减少阈值。 如果有，则会自动触发作业以更新用户档案计数。 对于批次摄取，在成功将批次摄取到[!DNL Profile]存储区后15分钟内，如果达到5%的增加或减少阈值，则会运行作业以更新量度。

## 使用[!UICONTROL 浏览]选项卡查看配置文件

在&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡上，您可以使用合并策略查看样本配置文件，或使用身份命名空间和值查找特定配置文件。

![将显示属于该组织的配置文件。](../images/user-guide/none-selected.png)

### 按[!UICONTROL 合并策略]浏览

默认情况下，**[!UICONTROL 浏览]**&#x200B;选项卡设置为您组织的默认合并策略。 要选择其他合并策略，请选择合并策略名称旁边的`X`，然后使用该选择器打开&#x200B;**[!UICONTROL 选择合并策略]**&#x200B;对话框。

>[!NOTE]
>
>如果未选择合并策略，请使用&#x200B;**[!UICONTROL 合并策略]**&#x200B;字段旁边的选择器按钮打开选择对话框。

![合并策略选择器已突出显示。](../images/user-guide/browse-by-merge-policy.png)

要从&#x200B;**[!UICONTROL 选择合并策略]**&#x200B;对话框中选择合并策略，请选择策略名称旁边的单选按钮，然后使用&#x200B;**[!UICONTROL 选择]**&#x200B;返回[!UICONTROL 浏览]选项卡。 然后，您可以选择&#x200B;**[!UICONTROL 视图]**&#x200B;以刷新示例配置文件并查看应用了新合并策略的配置文件采样。

![将显示一个对话框，您可以在其中选择要作为筛选依据的合并策略。](../images/user-guide/select-merge-policy.png)

显示的配置文件表示在应用所选合并策略后，从您组织的配置文件存储区中选择最多20个配置文件的示例。 将新数据添加到贵组织的配置文件存储区后，将刷新所选合并策略的示例配置文件。

要查看其中一个示例配置文件的详细信息，请选择&#x200B;**[!UICONTROL 配置文件ID]**。 有关详细信息，请参阅本指南稍后关于[查看配置文件详细信息](#profile-detail)的部分。

![显示与合并策略匹配的样本配置文件。](../images/user-guide/sample-profiles.png)

要了解有关合并策略及其在Platform中的角色的更多信息，请参阅[合并策略概述](../merge-policies/overview.md)。

### 按[!UICONTROL 标识]浏览 {#browse-identity}

在&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡上，您可以使用标识命名空间来按标识值查找特定配置文件。 按身份浏览需要您提供合并策略、身份命名空间和身份值。

![合并策略选择器已突出显示。](../images/user-guide/browse-by-merge-policy.png)

如有必要，请使用&#x200B;**[!UICONTROL 合并策略]**&#x200B;选择器打开&#x200B;**[!UICONTROL 选择合并策略]**&#x200B;对话框，然后选择要使用的合并策略。

![将显示一个对话框，您可以在其中选择要作为筛选依据的合并策略。](../images/user-guide/select-merge-policy.png)

然后使用&#x200B;**[!UICONTROL 身份命名空间]**&#x200B;选择器打开&#x200B;**[!UICONTROL 选择身份命名空间]**&#x200B;对话框并选择要搜索的命名空间。 如果贵组织具有多个命名空间，则可以使用对话框中的搜索栏开始键入命名空间的名称。

您可以选择命名空间来查看其他详细信息，也可以选择单选按钮来选择命名空间。 然后，您可以使用&#x200B;**[!UICONTROL 选择]**&#x200B;继续。

![将显示一个对话框，您可以在其中选择要作为筛选依据的身份命名空间。](../images/user-guide/select-identity-namespace.png)

选择[!UICONTROL 身份命名空间]并返回[!UICONTROL 浏览]选项卡后，您可以输入与所选命名空间相关的&#x200B;**[!UICONTROL 身份值]**。

>[!NOTE]
>
>此值特定于单个客户配置文件，并且必须是所提供命名空间的有效条目。 例如，选择身份命名空间“Email”将需要有效电子邮件地址形式的身份值。

![要过滤的标识值突出显示。](../images/user-guide/filter-identity-value.png)

输入值后，选择&#x200B;**[!UICONTROL 视图]**，并返回与该值匹配的单个配置文件。 选择&#x200B;**[!UICONTROL 配置文件ID]**&#x200B;以查看配置文件详细信息。

![与标识值匹配的配置文件突出显示。](../images/user-guide/filtered-identity-value.png)

## 查看轮廓详情 {#profile-detail}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_201001_404"
>title="未找到实体"
>abstract="这意味着平台找不到所请求的实体。要解决此错误，请尝试以下解决方案之一：<ul><li>确保您尝试访问的实体的 URL 中列出了正确的轮廓 ID。</li><li>确保您拥有适合您尝试访问的实体的相应的组织和沙盒组合。</li></ul>"

选择&#x200B;**[!UICONTROL 配置文件ID]**&#x200B;后，**[!UICONTROL 详细信息]**&#x200B;选项卡将打开。 显示在&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡上的配置文件信息已从多个配置文件片段合并在一起，形成单个客户的视图。 这包括客户详细信息，如基本属性、链接身份和渠道偏好设置。

显示的默认字段也可以在组织级别更改以显示首选用户档案属性。 要了解有关自定义这些字段的更多信息，包括添加和删除属性以及调整仪表板面板大小的分步说明，请阅读[配置文件详细信息自定义指南](profile-customization.md)。

![详细信息选项卡突出显示。 将显示配置文件详细信息。](../images/user-guide/profile-detail-row-name.png)

您还可以选择在查看属性名称作为其显示名称与字段路径名称之间进行切换。 若要在这两个显示之间切换，请选择&#x200B;**[!UICONTROL 显示显示名称]**&#x200B;切换开关。

![显示名称切换开关高亮显示，显示名称显示在属性下。](../images/user-guide/profile-detail.png)

要查看与单个客户配置文件相关的附加信息，请选择其它可用标签之一。 这些选项卡包括属性、事件和受众成员资格选项卡，用于显示配置文件当前符合条件的受众。

### “属性”选项卡

**[!UICONTROL 属性]**&#x200B;选项卡提供了一个列表视图，该视图汇总了应用指定的合并策略后与单个配置文件相关的所有属性。

通过选择&#x200B;**[!UICONTROL 查看JSON]**，也可以将这些属性视为JSON对象。 对于希望更好地了解如何将配置文件属性摄取到Platform中的任何用户，此功能非常有用。

![“属性”选项卡高亮显示。 显示配置文件属性。](../images/user-guide/attributes.png)

要查看Edge上可用的属性，请在数据位置选择器上选择&#x200B;**[!UICONTROL Edge]**。

![属性选项卡中的数据位置选择器突出显示。](../images/user-guide/attributes-select.png)

有关边缘配置文件的详细信息，请阅读[边缘配置文件文档](../edge-profiles.md)。

### “事件”选项卡

**[!UICONTROL 事件]**&#x200B;选项卡包含与客户关联的100个最新ExperienceEvents中的数据。 此数据可能包括电子邮件打开次数、购物车活动和页面查看次数。 为任何单个事件选择&#x200B;**[!UICONTROL 查看全部]**&#x200B;将提供附加字段和值作为事件的一部分捕获。

通过选择以&#x200B;**[!UICONTROL 查看JSON]**，还可以将事件视为JSON对象。 这有助于了解如何在Platform中捕获事件。

![事件选项卡突出显示。 显示配置文件事件。](../images/user-guide/events.png)

### “受众成员资格”选项卡

**[!UICONTROL 受众成员资格]**&#x200B;选项卡显示一个列表，其中包含单个客户配置文件当前所属受众的名称和描述。 当配置文件符合受众资格或过期时，此列表会自动更新。 配置文件当前符合条件的受众总数，将显示在选项卡的右侧。

有关Experience Platform中分段的更多信息，请参阅[Adobes Experience Platform分段服务文档](../../segmentation/home.md)。

![受众成员资格选项卡突出显示。 将显示个人资料的受众成员资格详细信息。](../images/user-guide/audience-membership.png)

要查看Edge上可用配置文件的受众成员资格，请在数据位置选择器中选择&#x200B;**[!UICONTROL Edge]**。 有关边缘分段的更多信息，请参阅[边缘分段指南](../../segmentation/methods/edge-segmentation.md)。

![受众成员资格选项卡中的数据位置选择器突出显示。](../images/user-guide/audience-membership-select.png)

## 合并策略

从主&#x200B;**[!UICONTROL 配置文件]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 合并策略]**&#x200B;选项卡以查看属于您组织的合并策略列表。 每个列出的策略都会显示其名称（无论其是否为默认合并策略）及其应用的架构类。

有关合并策略的详细信息，请参阅[合并策略概述](../merge-policies/overview.md)。

![突出显示了“合并策略”选项卡。 将显示属于组织的合并策略。](../images/user-guide/merge-policies.png)

## 合并架构 {#union-schema}

从主&#x200B;**[!UICONTROL 配置文件]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 合并架构]**&#x200B;选项卡，以查看所摄取数据的可用合并架构。 合并架构是同一类下所有[!DNL Experience Data Model] (XDM)字段的合并，这些字段的架构已在[!DNL Real-Time Customer Profile]中启用。

有关合并架构的详细信息，请访问[合并架构UI指南](union-schema.md)。

![合并架构选项卡突出显示。 将显示属于该组织的合并架构。](../images/user-guide/union-schema.png)

## 计算属性 {#computed-attributes}

从主&#x200B;**[!UICONTROL 配置文件]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 计算属性]**&#x200B;选项卡以查看属于您组织的计算属性列表。

![已突出显示“计算属性”选项卡。](../images/user-guide/computed-attributes.png)

有关计算属性的详细信息，请阅读[计算属性概述](../computed-attributes/overview.md)。 有关如何在Platform UI中使用计算属性的更多信息，请参阅[计算属性UI指南](../computed-attributes/ui.md)。

## 后续步骤

通过阅读本指南，您可以了解如何使用Experience Platform UI查看和管理组织的配置文件数据。 有关如何使用Experience Platform API处理配置文件数据的信息，请参阅[实时客户配置文件API指南](../api/overview.md)。
