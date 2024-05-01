---
keywords: target个性化；目标；experience platform target目标；adobe target目标；
title: Adobe Target连接
description: Adobe Target是一款应用程序，可在网站、移动应用程序等的所有入站客户互动中提供由AI支持的实时个性化和实验功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: c113d9615a276af67714f38b8325e69737b23964
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 13%

---

# Adobe Target连接 {#adobe-target-connection}

## 目标更改日志 {#changelog}

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2024 年 4 月 | 功能和文档更新 | 使用数据流ID连接到Target目标时，您现在可以 *不需要* 必须为边缘分段启用数据流。 这意味着Target目标将与批处理受众和流式受众配合使用，但您可以完成的用例有所不同。 在中查看表 [连接参数](#parameters) 部分以了解更多信息。 |
| 2024 年 1 月 | 功能和文档更新 | 您现在可以为默认的生产沙盒和其他非默认沙盒将受众和配置文件属性共享到Adobe Target连接。 |
| 2023 年 6 月 | 功能和文档更新 | 自2023年6月起，在配置新的Adobe Target目标连接时，您可以选择要将受众共享到的Adobe Target工作区。 请参阅[连接参数](#parameters)部分，了解详细信息。另外，请参阅有关在 Adobe Target 中[配置工作区](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=zh-Hans)的教程，了解更多有关工作区的信息。 |
| 2023 年 5 月 | 功能和文档更新 | 截至2023年5月， **[!UICONTROL Adobe Target]** 连接支持 [基于属性的个性化](../../ui/activate-edge-personalization-destinations.md#map-attributes) 面向所有客户。 |

{style="table-layout:auto"}

## 概述 {#overview}

Adobe Target是一款应用程序，可在网站、移动应用程序等的所有入站客户互动中提供由AI支持的实时个性化和实验功能。

Adobe Target是Adobe Experience Platform目标目录中的个性化连接。

## 视频概述 {#video-overview}

有关如何在Experience Platform中配置Adobe Target连接的简短概述，请观看以下视频。

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## 先决条件 {#prerequisites}

### 数据流ID {#datastream-id}

配置Adobe Target连接以连接到 [使用数据流ID](#parameters)，您必须拥有 [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) 已实施。

在不使用数据流ID的情况下配置Adobe Target连接不需要实施Web SDK。

>[!IMPORTANT]
>
>创建之前 [!DNL Adobe Target] connection，请阅读操作指南 [为同一页面和下一页面个性化配置个性化目标](../../ui/activate-edge-personalization-destinations.md). 本指南将指导您跨多个Experience Platform组件完成同页和下一页个性化用例所需的配置步骤。 要实现同页和下一页个性化用例，在配置Adobe Target连接时必须使用数据流ID。

### Adobe Target中的先决条件 {#prerequisites-in-adobe-target}

在Adobe Target中，确保您的用户具有：

* 访问 [默认工作区](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace)；
* 此 **审批者** [角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

阅读有关授予权限的详细信息 [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) 和 [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions).

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | X | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!DNL Profile request]** | 您正在请求在Adobe Target目标中映射的所有受众作为单个配置文件。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="关于数据流 ID"
>abstract="此选项确定受众将包含在哪个数据收集数据流中。下拉菜单仅显示已启用目标配置的数据流。要使用边缘分段，您必须选择数据流 ID。选择“无”将禁用所有使用边缘分段的用例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=zh-Hans#parameters" text="了解有关选择数据流的更多信息"

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

Adobe Experience Platform会自动连接到贵公司的Adobe Target实例。 无需身份验证。

### 连接参数 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="关于 Adobe Target 工作区"
>abstract="选择将受众共享到的 Adobe Target 工作区。可为每个 Adobe Target 连接选择一个工作区。激活后，受众将会被路由到选定的工作区，同时遵循适用的 Experience Platform 数据使用标签。"
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=zh-Hans" text="详细了解 Adobe Target 工作区"

同时 [设置](../../ui/connect-destination.md) 此目标必须提供以下信息：

* **名称**：填写此目标的首选名称。
* **描述**：输入目标的描述。 例如，您可以提及要将此目标用于哪个营销活动。 此字段为可选字段。
* **数据流ID**：这确定要包含受众的数据收集数据流。 下拉菜单仅显示启用了Target和Adobe Experience Platform服务的数据流。 请参阅 [配置数据流](../../../datastreams/configure.md#aep) 有关如何为Adobe Experience Platform和Adobe Target配置数据流的详细信息。

  >[!IMPORTANT]
  >
  >每个Adobe Target目标连接的数据流ID都是唯一的。 如果需要将相同的受众映射到多个数据流，您必须 [创建新的目标连接](../../ui/connect-destination.md) ，然后查看 [audience activation流程](#activate).

   * **[!UICONTROL 无]**：如果您需要配置Adobe Target个性化，但无法实施，请选择此选项 [Experience PlatformWeb SDK](/help/web-sdk/home.md). 使用此选项时，从Experience Platform导出到Target的受众仅支持下一会话个性化，并且禁用边缘分段。 请参阅下表，比较每种实施类型的可用用例。

  | Adobe Target实施 *不含* Web SDK | Adobe Target实施 *替换为* Web SDK | Adobe Target实施 *替换为* Web SDK *和* 关闭边缘分段 |
  |---|---|---|
  | <ul><li>数据流不是必需的。 Adobe Target可以通过以下方式部署： [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html)， [服务器端](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation)，或 [混合](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation) 实施方法。</li><li>[边缘分段](../../../segmentation/ui/edge-segmentation.md) 不受支持。</li><li>[同一页面和下一页面个性化](../../ui/activate-edge-personalization-destinations.md) 不受支持。</li><li>您可以将受众和配置文件属性共享到Adobe Target连接的 *默认的生产沙盒* 和非默认沙盒。</li><li>要在不使用数据流ID的情况下配置下一会话个性化，请使用 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>需要将Adobe Target和Experience Platform配置为服务的数据流。</li><li>边缘分段按预期工作。</li><li>[同一页面和下一页面个性化](../../ui/activate-edge-personalization-destinations.md#use-cases) 受支持。</li><li>支持从其他沙盒共享受众和配置文件属性。</li></ul> | <ul><li>需要将Adobe Target和Experience Platform配置为服务的数据流。</li><li>时间 [配置数据流](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)，请勿选择 **边缘分段** 复选框。</li><li>[下一会话个性化](../../ui/activate-edge-personalization-destinations.md#next-session) 受支持。</li><li>支持从其他沙盒共享受众和配置文件属性。</li></ul> |

* **工作区**：选择Adobe Target [工作区](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=zh-Hans) 将共享到的受众。 可为每个 Adobe Target 连接选择一个工作区。激活后，在遵循适用的同时，受众将被路由到选定的工作区 [Experience Platform数据使用标签](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>在使用的自定义Target工作区时 [使用属性进行同一页面和下一页面个性化](../../ui/activate-edge-personalization-destinations.md)，仅 [选定受众](../../ui/activate-edge-personalization-destinations.md#select-audiences) 都会发送到选定的Target工作区。 此 [映射的属性](../../ui/activate-edge-personalization-destinations.md#mapping) 都会发送到默认的Target工作区。
><br>
>此行为将在以后的更新中更改。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [激活受众以边缘个性化目标](../../ui/activate-edge-personalization-destinations.md) 有关将受众激活到此目标的说明。

## 导出的数据 {#exported-data}

Adobe Target *阅读* 配置文件数据来自Adobe Experience PlatformEdge Network，因此不会导出任何数据。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).
