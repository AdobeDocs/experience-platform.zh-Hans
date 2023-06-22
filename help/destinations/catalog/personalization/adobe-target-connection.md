---
keywords: target个性化；目标；experience platform target目标；adobe target目标；
title: Adobe Target连接
description: Adobe Target是一款应用程序，可在网站、移动应用程序等的所有入站客户交互中提供由AI支持的实时个性化和实验功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 3b2fedf4f7b17c4fb32afb5978bfac6f618f5bc3
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 7%

---

# Adobe Target连接 {#adobe-target-connection}

## 目标更改日志 {#changelog}

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 6 月 | 功能和文档更新 | 自2023年6月起，在配置新的Adobe Target目标连接时，您可以选择要将受众共享到的Adobe Target工作区。 请参阅 [连接参数](#parameters) 部分以了解更多信息。 此外，请参阅关于的教程 [配置工作区](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en) Adobe Target中的，以了解有关工作区的更多信息。 |
| 2023 年 5 月 | 功能和文档更新 | 截至2023年5月， **[!UICONTROL Adobe Target]** 连接支持 [基于属性的个性化](../../ui/activate-edge-personalization-destinations.md#map-attributes) 并向所有客户正式提供。 |

{style="table-layout:auto"}

## 概述 {#overview}

Adobe Target是一款应用程序，可在网站、移动应用程序等的所有入站客户交互中提供由AI支持的实时个性化和实验功能。

Adobe Target是Adobe Experience Platform目标目录中的个性化连接。

有关如何在Experience Platform中配置Adobe Target连接的简短概述，请观看以下视频。

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## 先决条件 {#prerequisites}

### 数据流ID {#datastream-id}

将Adobe Target连接配置到 [使用数据流Id](#parameters)，您必须拥有 [Adobe Experience Platform Web SDK](../../../edge/home.md) 已实施。

在不使用数据流ID的情况下配置Adobe Target连接不需要您实施Web SDK。

>[!IMPORTANT]
>
>创建之前 [!DNL Adobe Target] connection，请阅读操作指南 [为同一页面和下一页面个性化配置个性化目标](../../ui/activate-edge-personalization-destinations.md). 本指南将指导您跨多个Experience Platform组件完成同页和下一页个性化用例所需的配置步骤。 同页和下一页个性化要求您在配置Adobe Target连接时使用数据流ID。

### Adobe Target中的先决条件 {#prerequisites-in-adobe-target}

在Adobe Target中，确保您的用户具有：

* 访问 [默认工作区](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace)；
* 此 **审批者** [角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

阅读有关授予权限的详细信息 [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) 和 [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!DNL Profile request]** | 您正在请求在Adobe Target目标中映射的所有区段用于单个配置文件。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="关于数据流 ID"
>abstract="此选项确定区段将包含在哪个数据收集数据流中。下拉菜单仅显示已启用目标配置的数据流。要使用边缘分段，您必须选择数据流 ID。选择“无”将禁用所有使用边缘分段的用例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="了解有关选择数据流的更多信息"

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

Adobe Experience Platform会自动连接到贵公司的Adobe Target实例。 无需身份验证。

### 连接参数 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="关于Adobe Target工作区"
>abstract="选择要将受众共享到的Adobe Target工作区。 您可以为每个Adobe Target连接选择一个工作区。 激活后，受众将在遵循适用的Experience Platform数据使用标签的同时被路由到选定的工作区。"
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en" text="了解有关Adobe Target工作区的更多信息"

While [设置](../../ui/connect-destination.md) 必须提供以下信息，才能使用此目标：

* **名称**：填写此目标的首选名称。
* **描述**：输入目标的描述。 例如，您可以提及要将此目标用于哪个营销活动。 此字段是可选的。
* **数据流ID**：这确定要包含区段的数据收集数据流。 下拉菜单仅显示启用了Target和Adobe Experience Platform服务的数据流。 参见 [配置数据流](../../../edge/datastreams/configure.md#aep) 有关如何为Adobe Experience Platform和Adobe Target配置数据流的详细信息。
   * **[!UICONTROL 无]**：如果需要配置Adobe Target个性化，但无法实施，请选择此选项 [Experience PlatformWeb SDK](../../../edge/home.md). 使用此选项时，从Experience Platform导出到Target的区段仅支持下一会话个性化，并且禁用边缘分段。 有关更多信息，请参阅下表。
* **工作区**：选择Adobe Target [工作区](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en) 受众将共享到的受众。 您可以为每个Adobe Target连接选择一个工作区。 激活后，受众将路由到选定的工作区，同时遵循适用的规则 [Experience Platform数据使用标签](../../../data-governance/labels/overview.md).

| 未选择数据流 | 已选择数据流 |
|---|---|
| <ul><li>[边缘分段](../../../segmentation/ui/edge-segmentation.md) 不受支持。</li><li>[同一页面和下一页面个性化](../../ui/activate-edge-personalization-destinations.md) 不受支持。</li><li>您只能将区段共享到Adobe Target连接， *默认生产沙盒*.</li><li>要在不使用数据流ID的情况下配置下一会话个性化，请使用 [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>边缘分段按预期工作。</li><li>[同一页面和下一页面个性化](../../ui/activate-edge-personalization-destinations.md) 受支持。</li><li>其他沙盒支持区段共享。</li></ul> |

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将配置文件和区段激活到配置文件请求目标](../../ui/activate-edge-personalization-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

Adobe Target从Adobe Experience Platform Edge Network中读取配置文件数据，因此不会导出任何数据。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).
