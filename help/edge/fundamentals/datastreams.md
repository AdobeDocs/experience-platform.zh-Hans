---
title: 为Experience PlatformWeb SDK配置数据流
description: '了解如何配置数据流。 '
keywords: 配置；数据流；数据流ID；边缘；数据流ID；环境设置；edgeConfigId；身份；启用ID同步的容器ID；沙盒；流入口；事件数据集；目标；客户端代码；资产令牌；目标环境ID;Cookie目标；URL目标；Analytics设置阻止报表包ID;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 0141f0a83ca7b444015d98d8ce11199b400f77a5
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 1%

---

# 配置数据流

数据流表示实施Adobe Experience Platform Web和移动SDK时的服务器端配置。 而 [配置命令](configuring-the-sdk.md) 中的控件控制必须在客户端上处理的事项(例如 `edgeDomain`)，数据流将处理SDK的所有其他配置。 请求发送至Adobe Experience Platform边缘网络时， `edgeConfigId` 用于引用数据流。 这样，您就无需在网站上进行代码更改即可更新服务器端配置。

本文档介绍了在数据收集UI中配置数据流的步骤。

>[!NOTE]
>
>您的组织必须配置此功能才能在UI中访问它。 如果您没有访问权限，请联系您的客户成功经理(CSM)以开始允许列表。

## 访问 [!UICONTROL 数据流] 工作区

您可以通过选择 **[!UICONTROL 数据流]** 中。

![数据收集UI中的“数据流”选项卡](../images/datastreams/datastreams-tab.png)

>[!NOTE]
>
>而您可以 [!UICONTROL 数据流] 选项卡无论您是否使用Platform的标签管理功能，都必须拥有开发人员权限来自行管理数据流。 请参阅 [用户权限](../../tags/ui/administration/user-permissions.md) 有关更多详细信息，请参阅标记文档中的文章。

的 [!UICONTROL 数据流] 选项卡显示现有数据流的列表，包括其友好名称、ID和上次修改日期。 选择要跟踪的数据流的名称 [查看其详细信息并配置服务](#view-details).

选择“更多”图标(**...**)以显示更多选项。 选择 **[!UICONTROL 编辑]** 更新 [基本配置](#configure) ，或选择 **[!UICONTROL 删除]** 删除数据流。

![用于编辑或删除和现有数据流的选项](../images/datastreams/edit-datastream.png)

## 创建新数据流 {#create}

要创建数据流，请首先选择 **[!UICONTROL 新数据流]**.

![选择新数据流](../images/datastreams/new-datastream-button.png)

### [!UICONTROL 配置] {#configure}

此时会显示数据流创建工作流，从配置步骤开始。 在此，必须为数据流提供名称和可选描述。

如果要配置此数据流以在Experience Platform中使用，并且使用的是Platform Web SDK，则还必须选择 [基于事件的体验数据模型(XDM)架构](../../xdm/classes/experienceevent.md) 来表示您计划摄取的数据。

![数据流的基本配置](../images/datastreams/configure.png)

本节的其余部分重点介绍将数据映射到选定平台事件架构的步骤。 如果您使用的是Mobile SDK或未为Platform配置数据流，请选择 **[!UICONTROL 保存]** 在继续下一节之前，请参阅 [向数据流添加服务](#add-services).

### 为数据收集准备数据 {#data-prep}

>[!IMPORTANT]
>
>Mobile SDK实施当前不支持为数据收集进行数据准备。

数据准备是一项Experience Platform服务，允许您映射、转换和验证来自体验数据模型(XDM)的数据。 在配置启用平台的数据流时，您可以在将源数据发送到平台边缘网络时，使用数据准备功能将源数据映射到XDM。

以下子部分介绍在数据收集UI中映射数据的基本步骤。 有关所有数据准备功能（包括计算字段的转换函数）的全面指导，请参阅以下文档：

* [数据准备概述](../../data-prep/home.md)
* [数据准备映射函数](../../data-prep/functions.md)
* [使用数据准备处理数据格式](../../data-prep/data-handling.md)

#### [!UICONTROL 选择数据]

选择 **[!UICONTROL 保存并添加映射]** 完成 [基本配置步骤](#configure)和 **[!UICONTROL 选择数据]** 中。 在此，您必须提供一个JSON对象示例，该对象表示您计划发送到平台的数据的结构。 您可以选择将对象上传为文件的选项，或将原始对象粘贴到提供的文本框中。

>[!NOTE]
>
>JSON对象必须具有单个根节点 `data` 以通过验证。

如果JSON有效，则会在右侧面板中显示预览架构。 选择 **[!UICONTROL 下一个]** 继续。

![预期传入数据的JSON示例](../images/datastreams/select-data.png)

#### [!UICONTROL 映射]

的 **[!UICONTROL 映射]** 步骤，允许您将源数据中的字段映射到平台中目标事件架构的字段。 要开始配置，请选择 **[!UICONTROL 添加新映射]** 创建新映射行。

![添加新映射](../images/datastreams/add-new-mapping.png)

选择源图标(![“源”图标](../images/datastreams/source-icon.png))，并在出现的对话框中，选择要在提供的画布中映射的源字段。 选择字段后，请使用 **[!UICONTROL 选择]** 按钮继续。

![选择要在源架构中映射的字段](../images/datastreams/source-mapping.png)

接下来，选择架构图标(![“架构”图标](../images/datastreams/schema-icon.png))以打开目标事件架构的类似对话框。 选择要在确认之前将数据映射到的字段 **[!UICONTROL 选择]**.

![选择要在目标架构中映射的字段](../images/datastreams/target-mapping.png)

此时将重新显示映射页面，并显示已完成的字段映射。 的 **[!UICONTROL 映射进度]** 部分更新以反映已成功映射的字段总数。

![已成功映射反映进度的字段](../images/datastreams/field-mapped.png)

继续按照上述步骤将其余字段映射到目标架构。 虽然您不必映射所有可用的源字段，但必须映射目标架构中设置为必需的任何字段，才能完成此步骤。 的 **[!UICONTROL 必填字段]** 计数器指示当前配置中尚未映射的必填字段数。

当必填字段计数达到零且您对映射满意后，请选择 **[!UICONTROL 保存]** 完成更改。

![映射完成](../images/datastreams/mapping-complete.png)

## 查看数据流详细信息 {#view-details}

配置新数据流或选择要查看的现有数据流后，将显示该数据流的详细信息页面。 在此，您可以找到有关数据流（包括其ID）的更多信息。

![已创建数据流的详细信息页面](../images/datastreams/view-details.png)

创建数据流后，会使用相同的设置自动创建三个关联的环境。 这三个环境包括 `dev`, `stage`和 `prod`，对应于 [标记的默认环境](../../tags/ui/publishing/environments.md). 在将标记库构建到 `dev` 环境中，库会自动使用 `dev` 环境。 您可以根据自己的需求，在单个环境中自由编辑设置。

在SDK实施中， `edgeConfigId` 是一个复合ID，用于指定该数据流中的数据流和特定环境。 例如，要指定 `stage` 具有ID的数据流的环境 `1c86778b-cdba-4684-9903-750e52912ad1`，则使用 `edgeConfigId` `1c86778b-cdba-4684-9903-750e52912ad1:stage`.

>[!IMPORTANT]
>
>如果复合ID中不存在环境，则生产环境(`prod`)。

从数据流详细信息屏幕中，您可以 [添加服务](#add-services) 从您有权访问的Adobe Experience Cloud产品中启用各项功能。

## 向数据流添加服务 {#add-services}

在数据流的详细信息页面上，选择 **[!UICONTROL 添加服务]** 以开始添加该数据流的可用服务。

![选择添加服务以继续](../images/datastreams/add-service.png)

在下一个屏幕中，使用下拉菜单选择要为此数据流配置的服务。 此列表中将仅显示您有权访问的服务。

![从列表中选择服务](../images/datastreams/service-selection.png)

选择所需的服务，填写显示的配置选项，然后选择 **[!UICONTROL 保存]** 将服务添加到数据流。 所有添加的服务都显示在数据流的详细信息视图中。

![向数据流添加的服务](../images/datastreams/services-added.png)

以下子部分介绍了每项服务的配置选项。

>[!NOTE]
>
>每个服务配置都包含一个 **[!UICONTROL 已启用]** 在选择服务时自动激活的切换开关。 要禁用此数据流的选定服务，请选择 **[!UICONTROL 已启用]** 再次切换。

### Adobe Analytics设置

此服务可控制数据是否以及如何发送到Adobe Analytics。 有关更多详细信息，请参阅 [向Analytics发送数据](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics设置块](../images/datastreams/analytics-config.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL 报表包 ID] | **（必需）** 要将数据发送到的Analytics报表包的ID。 此ID可在Adobe Analytics UI中的 [!UICONTROL 管理员] > [!UICONTROL 报表包]. 如果指定了多个报表包，则数据会复制到每个报表包。 |

### Adobe Audience Manager设置

此服务可控制数据是否以及如何发送到Adobe Audience Manager。 将数据发送到Audience Manager所需的只是启用此部分。 其他设置是可选的，但鼓励使用。

![Adobe受众管理设置块](../images/datastreams/audience-manager-config.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL Cookie目标已启用] | 允许SDK通过 [cookie目标](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) 从 [!DNL Audience Manager]. |
| [!UICONTROL 启用URL目标] | 允许SDK通过 [URL目标](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) 从 [!DNL Audience Manager]. |

### Adobe Experience Platform设置

>[!IMPORTANT]
>
>为Platform启用数据流时，请注意您当前使用的Platform沙盒，如数据收集UI顶部功能区中所示。
>
>![选定的沙盒](../images/datastreams/platform-sandbox.png)
>
>沙盒是Adobe Experience Platform中的虚拟分区，允许您将数据和实施与组织中的其他人员隔离开来。 创建数据流后，便无法更改其沙盒。 有关沙箱在Experience Platform中角色的更多详细信息，请参阅 [沙盒文档](../../sandboxes/home.md).

此服务可控制数据是否以及如何发送到Adobe Experience Platform。

![Adobe Experience Platform设置块](../images/datastreams/platform-config.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL 事件数据集] | **（必需）** 选择将客户事件数据流式传输到的Platform数据集。 此架构必须使用 [XDM ExperienceEvent类](../../xdm/classes/experienceevent.md). |
| [!UICONTROL 配置文件数据集] | 选择要将客户属性数据发送到的Platform数据集。 此架构必须使用 [XDM个人配置文件类](../../xdm/classes/individual-profile.md). |
| [!UICONTROL 优惠决策] | 选中此复选框可启用Platform Web SDK实施的Offer decisioning。 请参阅 [将Offer decisioning与Platform Web SDK结合使用](../personalization/offer-decisioning/offer-decisioning-overview.md) 以了解更多实施详细信息。 有关Offer decisioning功能的更多信息，请参阅 [Adobe Journey Optimizer文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=zh-Hans). |
| [!UICONTROL 边缘分割] | 选中此复选框可启用 [边缘分割](../../segmentation/ui/edge-segmentation.md) 数据流。 当SDK通过启用边缘分段的数据流发送数据时，相关用户档案的任何更新区段成员关系将在响应中发送回。<br><br>此选项可与 [!UICONTROL 个性化目标] 表示 [下一页个性化用例](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL 个性化目标] | 与 [!UICONTROL 边缘分割] 复选框，此选项允许数据流连接到个性化引擎，如Adobe Target。 有关的具体步骤，请参阅目标文档 [配置个性化目标](../../destinations/ui/configure-personalization-destinations.md). |

### Adobe Target设置

此服务可控制数据是否以及如何发送到Adobe Target。

![Adobe Target设置块](../images/datastreams/target-config.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL 资产令牌] | [!DNL Target] 允许客户通过使用资产来控制权限。 有关属性的更多信息，请参阅 [配置企业权限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) 在 [!DNL Target] 文档。<br><br>资产令牌可在Adobe Target UI中的 [!UICONTROL 设置] > [!UICONTROL 属性]. |
| [!UICONTROL Target环境ID] | [Adobe Target中的环境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) 帮助您在所有开发阶段管理实施。 此设置指定要与此数据流一起使用的环境。<br><br>最佳做法是对您的 `dev`, `stage`和 `prod` 数据流环境，使事情保持简单。 但是，如果您已经定义了Adobe Target环境，则可以使用这些环境。 |
| [!UICONTROL Target第三方ID命名空间] | 的标识命名空间 `mbox3rdPartyId` 要用于此数据流。 请参阅 [实施 `mbox3rdPartyId` 和Web SDK](../personalization/adobe-target/using-mbox-3rdpartyid.md) 以了解更多信息。 |

### [!UICONTROL 事件转发] 设置

此服务控制数据是否以及如何发送到 [事件转发](../../tags/ui/event-forwarding/overview.md).

![配置UI的“事件转发”部分](../images/datastreams/event-forwarding-config.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL Launch资产] | **（必需）** 要将数据发送到的事件转发属性。 |
| [!UICONTROL Launch环境] | **（必需）** 要将数据发送到的选定资产中的环境。 |

>[!NOTE]
>
>您可以选择 **[!UICONTROL 手动输入ID]** 以键入属性和环境名称，而不使用下拉菜单。

### [!UICONTROL 第三方ID同步] 设置

第三方ID部分是唯一始终打开的部分。 它有两个可用的设置：&quot;[!UICONTROL 已启用第三方ID同步]&quot;和&quot;[!UICONTROL 第三方ID同步容器ID]&quot;

![配置UI的“第三方ID同步”部分](../images/datastreams/third-party-id-sync-config.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL 第三方ID同步容器ID] | ID同步可以分组到容器中，以允许在不同时间运行不同的ID同步。 此操作可控制为此数据流运行哪个ID同步容器。 |

## 后续步骤

本指南介绍了如何在数据收集UI中配置数据流。 有关如何在设置数据流后安装和配置Web SDK的更多信息，请参阅 [数据收集E2E指南](../../collection/e2e.md#install).
