---
keywords: target个性化；目标；experience platform target目标；adobe target目标；
title: Adobe Target连接
description: Adobe Target是一款应用程序，可在网站、移动应用程序等的所有入站客户互动中提供由AI支持的实时个性化和实验功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: f8863b79d0524ad3221d594756c027956e836070
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 9%

---

# Adobe Target连接 {#adobe-target-connection}

## 目标更改日志 {#changelog}

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2024 年 4 月 | 功能和文档更新 | 当连接到Target目标并使用数据流时，您现在&#x200B;*不需要*&#x200B;为边缘分段启用数据流。 这意味着Target目标将与批处理受众和流式受众配合使用，但您可以完成的用例有所不同。 查看[连接参数](#parameters)部分中的表以了解详细信息。 |
| 2024 年 1 月 | 功能和文档更新 | 您现在可以为默认的生产沙盒和其他非默认沙盒将受众和配置文件属性共享到Adobe Target连接。 |
| 2023 年 6 月 | 功能和文档更新 | 自2023年6月起，在配置新的Adobe Target目标连接时，您可以选择要将受众共享到的Adobe Target工作区。 请参阅[连接参数](#parameters)部分，了解详细信息。另外，请参阅有关在 Adobe Target 中[配置工作区](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html#)的教程，了解更多有关工作区的信息。 |
| 2023 年 5 月 | 功能和文档更新 | 自2023年5月起，**[!UICONTROL Adobe Target]**&#x200B;连接支持基于[属性的个性化](../../ui/activate-edge-personalization-destinations.md#map-attributes)，通常向所有客户提供。 |

{style="table-layout:auto"}

## 概述 {#overview}

Adobe Target是一款应用程序，可在网站、移动应用程序等的所有入站客户互动中提供由AI支持的实时个性化和实验功能。

Adobe Target是Adobe Experience Platform目标目录中的个性化连接。

## 视频概述 {#video-overview}

有关如何在Experience Platform中配置Adobe Target连接的简短概述，请观看以下视频。

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## 基于实施类型的受支持用例 {#supported-use-cases}

下表根据您的实施类型显示了Adobe Target目标支持的用例，无论是否启用了Web SDK，以及是否启用了[边缘分段](/help/segmentation/home.md#edge)。

| Adobe Target实施&#x200B;*不带* Web SDK | Adobe Target实施&#x200B;*与* Web SDK | 已关闭Adobe Target实施&#x200B;*的* Web SDK *和*&#x200B;边缘分段 |
|---|---|---|
| <ul><li>数据流不是必需的。 Adobe Target可以通过[at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html)、[服务器端](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation)或[hybrid](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation)实现方法进行部署。</li><li>不支持[Edge分段](../../../segmentation/methods/edge-segmentation.md)。</li><li>[不支持同一页面和下一页面个性化](../../ui/activate-edge-personalization-destinations.md)。</li><li>您可以将&#x200B;*默认生产沙盒*&#x200B;和非默认沙盒的受众和配置文件属性共享到Adobe Target连接。</li><li>要在不使用数据流的情况下配置下一会话个性化，请使用[at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html)。</li></ul> | <ul><li>需要将Adobe Target和Experience Platform配置为服务的数据流。</li><li>Edge分段按预期工作。</li><li>[支持同一页面和下一页面个性化](../../ui/activate-edge-personalization-destinations.md#use-cases)。</li><li>支持从其他沙盒共享受众和配置文件属性。</li></ul> | <ul><li>需要将Adobe Target和Experience Platform配置为服务的数据流。</li><li>在[配置数据流](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)时，请勿选中&#x200B;**Edge分段**&#x200B;复选框。</li><li>支持[下一会话个性化](../../ui/activate-edge-personalization-destinations.md#next-session)。</li><li>支持从其他沙盒共享受众和配置文件属性。</li></ul> |


## 先决条件 {#prerequisites}

### 数据流 {#datastream}

在配置与[的Adobe Target连接时使用数据流](#parameters)时，必须实施[Adobe Experience Platform数据收集](/help/collection/home.md)。

在不使用数据流的情况下配置Adobe Target连接不需要实施Web SDK。

>[!IMPORTANT]
>
>在创建[!DNL Adobe Target]连接之前，请阅读有关如何[为同一页面和下一页面个性化](../../ui/activate-edge-personalization-destinations.md)配置个性化目标的指南。 本指南将指导您跨多个Experience Platform组件完成相同页面和下一页面个性化用例所需的配置步骤。 要实现同页和下一页个性化用例，在配置Adobe Target连接时必须使用数据流。

### Adobe Target中的先决条件 {#prerequisites-in-adobe-target}

在Adobe Target中，确保您的用户具有：

* 访问[默认工作区](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace)；
* **审批者** [角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions)。

有关授予[Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80)和[Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions)权限的详细信息。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

>[!IMPORTANT]
>
>为同一页面和下一页面个性化用例&#x200B;*激活*&#x200B;边缘受众时，受众&#x200B;*必须*&#x200B;使用[active-on-edge合并策略](../../../segmentation/ui/segment-builder.md#merge-policies)。 [!DNL active-on-edge]合并策略可确保在[边缘上持续评估受众](../../../segmentation/methods/edge-segmentation.md)，并可用于实时和下一页个性化用例。  已阅读[所有可用的用例](#parameter)（基于实现类型）。
>如果将使用其他合并策略的边缘受众映射到Adobe Target目标，则对于实时和下一页用例，不会评估这些受众。
>按照[创建合并策略](../../../profile/merge-policies/ui-guide.md#create-a-merge-policy)中的说明进行操作，并确保启用&#x200B;**[!UICONTROL Active-On-Edge Merge Policy]**&#x200B;切换开关。


| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | X | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!DNL Profile request]** | 您正在请求在Adobe Target目标中映射的所有受众作为单个配置文件。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="关于数据流"
>abstract="此选项确定受众将包含在哪个数据收集数据流中。下拉菜单仅显示已启用目标配置的数据流。要使用边缘分段，您必须选择一个数据流。选择“无”将禁用所有使用边缘分段的用例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="了解有关选择数据流的更多信息"

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

Adobe Experience Platform会自动连接到贵公司的Adobe Target实例。 无需身份验证。

### 连接参数 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="关于 Adobe Target Workspaces"
>abstract="选择将受众共享到的 Adobe Target 工作区。可为每个 Adobe Target 连接选择一个工作区。激活后，受众将会被路由到选定的工作区，同时遵循适用的 Experience Platform 数据使用标签。"
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html#" text="详细了解 Adobe Target 工作区"

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **名称**：填写此目标的首选名称。
* **描述**：输入目标的描述。 例如，您可以提及要将此目标用于哪个营销活动。 此字段为可选字段。
* **数据流**：这将决定要将受众包含在哪个数据收集数据流中。 下拉菜单仅显示启用了Target和Adobe Experience Platform服务的数据流。 有关如何为Adobe Experience Platform和Adobe Target配置数据流的详细信息，请参阅[配置数据流](../../../datastreams/configure.md#aep)。

  >[!IMPORTANT]
  >
  >**跨组织**&#x200B;的数据流唯一性：对于IMS组织中的Adobe Target目标连接，数据流ID和沙盒名称的组合必须唯一。这意味着：
  >
  >* 数据流ID +沙盒名称的相同组合不能用于整个组织中的多个Adobe Target目标连接
  >* 您可以对不同目标连接使用相同的数据流ID，前提是这些连接位于不同的沙盒上
  >* 此规则适用于所有数据流选择，包括选择&#x200B;**[!UICONTROL None]**&#x200B;时

   * **[!UICONTROL None]**：如果需要配置Adobe Target个性化，但无法实施Adobe Experience Platform Web SDK，请选择此选项。 使用此选项时，从Experience Platform导出到Target的受众仅支持下一会话个性化，并且禁用边缘分段。 请参考[支持的用例](#supported-use-cases)部分中的表来比较每种实现类型的可用用例。

  | Adobe Target实施&#x200B;*不带* Web SDK | Adobe Target实施&#x200B;*与* Web SDK | 已关闭Adobe Target实施&#x200B;*的* Web SDK *和*&#x200B;边缘分段 |
  |---|---|---|
  | <ul><li>数据流不是必需的。 Adobe Target可以通过[at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html)、[服务器端](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation)或[hybrid](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation)实现方法进行部署。</li><li>不支持[Edge分段](../../../segmentation/methods/edge-segmentation.md)。</li><li>[不支持同一页面和下一页面个性化](../../ui/activate-edge-personalization-destinations.md)。</li><li>您可以将&#x200B;*默认生产沙盒*&#x200B;和非默认沙盒的受众和配置文件属性共享到Adobe Target连接。</li><li>要在不使用数据流的情况下配置下一会话个性化，请使用[at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html)。</li></ul> | <ul><li>需要将Adobe Target和Experience Platform配置为服务的数据流。</li><li>Edge分段按预期工作。</li><li>[支持同一页面和下一页面个性化](../../ui/activate-edge-personalization-destinations.md#use-cases)。</li><li>支持从其他沙盒共享受众和配置文件属性。</li></ul> | <ul><li>需要将Adobe Target和Experience Platform配置为服务的数据流。</li><li>在[配置数据流](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)时，请勿选中&#x200B;**Edge分段**&#x200B;复选框。</li><li>支持[下一会话个性化](../../ui/activate-edge-personalization-destinations.md#next-session)。</li><li>支持从其他沙盒共享受众和配置文件属性。</li></ul> |

* **Workspace**：选择要共享受众的Adobe Target [工作区](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html#)。 可为每个 Adobe Target 连接选择一个工作区。激活后，在遵循适用的[Experience Platform数据使用标签](../../../data-governance/labels/overview.md)时，受众将被路由到所选工作区。

>[!NOTE]
>
>为具有属性[的](../../ui/activate-edge-personalization-destinations.md)同一页面和下一页面个性化使用自定义Target工作区时，只将[选定的受众](../../ui/activate-edge-personalization-destinations.md#select-audiences)发送到选定的Target工作区。 [映射的属性](../../ui/activate-edge-personalization-destinations.md#mapping)将发送到默认的Target工作区。
><br>
>此行为将在以后的更新中更改。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请阅读[将受众激活到边缘个性化目标](../../ui/activate-edge-personalization-destinations.md)。

## 从Target目标删除受众 {#remove}

如果现有Adobe Target连接中的某个受众已在Adobe Target [活动](https://experienceleague.adobe.com/en/docs/target/using/activities/activities)中使用，则需要执行一些额外的步骤来删除该受众。 尝试从Adobe Target连接中删除受众时，如果Adobe Target活动使用受众，则会导致错误。

![Experience Platform UI图像显示因尝试删除Target活动使用的受众而导致的错误。](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

要在活动中使用该受众时从Target目标中删除受众，您必须首先从使用该受众的Target活动中删除该受众，或完全删除该活动。 然后，您可以从Target连接中删除受众。

如果活动中未使用该受众，请转到&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Browse]** > **[!UICONTROL Select destination dataflow]** > **[!UICONTROL Activation data]**，选择要删除的受众，然后选择&#x200B;**[!UICONTROL Remove audiences]**。

## 导出的数据 {#exported-data}

Adobe Target *从Adobe Experience Platform Edge Network中读取*&#x200B;配置文件数据，因此不会导出任何数据。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans)。
