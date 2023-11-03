---
title: 创建和配置数据流
description: 了解如何将客户端 Web SDK 集成与其他 Adobe 产品和第三方目标连接起来。
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: f4c41e75eaa61878557868ffa9ce0c866eba3941
workflow-type: tm+mt
source-wordcount: '2842'
ht-degree: 71%

---


# 创建和配置数据流

本文档介绍了在 UI 中配置[数据流](./overview.md)的步骤。

## 访问[!UICONTROL 数据流]工作区

您可以通过在左侧导航中选择&#x200B;**[!UICONTROL 数据流]**&#x200B;来在数据收集 UI 或 Experience Platform UI 中创建和管理数据流。

![数据收集 UI 中的“数据流”选项卡](assets/configure/datastreams-tab.png)

**[!UICONTROL 数据流]**&#x200B;选项卡显示现有数据流的列表，包括其友好名称、ID 和上次修改日期。选择数据流的名称以[查看其详细信息并配置服务](#view-details)。

选择特定数据流的“更多”图标 (**...**) 以显示更多选项。选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以更新数据流的[基本配置](#configure)，或选择&#x200B;**[!UICONTROL 删除]**&#x200B;以删除数据流。

![用于编辑或删除现有数据流的选项](assets/configure/edit-datastream.png)

## 创建新的数据流 {#create}

要创建数据流，请首先选择&#x200B;**[!UICONTROL 新数据流]**。

![选择新数据流](assets/configure/new-datastream-button.png)

数据流创建工作流随即出现，从配置步骤开始。从该位置，您必须提供数据流的名称和可选描述。

如果您要配置此数据流以在 Experience Platform 中使用并使用 Platform Web SDK，则还必须选择一个[基于事件的体验数据模型 (XDM) 架构](../xdm/classes/experienceevent.md)以表示您计划摄取的数据。

![数据流的基本配置](assets/configure/configure.png)

### 配置地理位置和网络查找 {#geolocation-network-lookup}

地理位置和网络查找设置可帮助您定义要收集的地理和网络级别数据的粒度级别。

展开 **[!UICONTROL 地理位置和网络查找]** 部分来配置下述设置。

![平台UI屏幕截图，其中显示了数据流配置屏幕，并突出显示地理位置和网络查找设置。](assets/configure/geolookup.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL 地理位置查找] | 根据访客的IP地址为所选选项启用地理位置查找。 可用选项包括： <ul><li>**国家/地区**：填充 `xdm.placeContext.geo.countryCode`</li><li>**邮政编码**：填充 `xdm.placeContext.geo.postalCode`</li><li>**省/市/自治区**：填充 `xdm.placeContext.geo.stateProvince`</li><li>**DMA**：填充 `xdm.placeContext.geo.dmaID`</li><li>**城市**：填充 `xdm.placeContext.geo.city`</li><li>**纬度**：填充 `xdm.placeContext.geo._schema.latitude`</li><li>**经度**：填充 `xdm.placeContext.geo._schema.longitude`</li></ul>选择&#x200B;**[!UICONTROL 城市]**、**[!UICONTROL 纬度]**&#x200B;或&#x200B;**[!UICONTROL 经度]**&#x200B;将提供最多两位小数的坐标，而不管选择的其他选项如何。这被视为城市级别粒度。<br> <br>未选择任何选项将禁用地理位置查找。 地理位置发生在之前 [!UICONTROL IP模糊处理]，这表示它不受影响 [!UICONTROL IP模糊处理] 设置。 |
| [!UICONTROL 网络查找] | 根据访客的IP地址启用所选选项的网络查找。 可用选项包括： <ul><li>**运营商**：填充 `xdm.environment.carrier`</li><li>**域**：填充 `xdm.environment.domain`</li><li>**ISP**：填充 `xdm.environment.ISP`</li></ul> |

如果启用以上任何字段进行数据收集，请确保正确设置 [`context`](../edge/data-collection/automatic-information.md) 数组属性，条件 [配置Web SDK](../edge/fundamentals/configuring-the-sdk.md).

地理位置查找字段使用 `context` 数组字符串 `"placeContext"`，而网络查找字段使用 `context` 数组字符串 `"environment"`.

此外，请确保架构中存在每个所需的XDM字段。 如果不能，您可以添加Adobe提供的变量 `Environment Details` 字段组添加到您的架构。

### 配置设备查找 {#geolocation-device-lookup}

此 **[!UICONTROL 设备查找]** 设置允许您选择要收集的特定于设备的信息。

展开 **[!UICONTROL 设备查找]** 部分来配置下述设置。

![平台UI屏幕截图，其中显示了数据流配置屏幕，并突出显示设备查找设置。](assets/configure/device-lookup.png)

>[!IMPORTANT]
>
>下表所述的设置是互斥的。 您不能同时选择用户代理信息和设备查找数据。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 保留用户代理和客户端提示标头]** | 选择此选项可仅收集用户代理字符串中存储的信息。 默认情况下，此设置处于选中状态。 填充 `xdm.environment.browserDetails.userAgent` |
| **[!UICONTROL 使用设备查找收集以下信息]** | 如果要收集以下一个或多个特定于设备的信息，请选择此选项： <ul><li>**[!UICONTROL 设备]** 信息：<ul><li>**设备制造商**：填充 `xdm.device.manufacturer`</li><li>**设备型号**：填充 `xdm.device.modelNumber`</li><li>**营销名称**：填充 `xdm.device.model`</li></ul></li><li>**[!UICONTROL 硬件]** 信息： <ul><li>**硬件类型**：填充 `xdm.device.type`</li><li>**显示高度**：填充 `xdm.device.screenHeight`</li><li>**显示宽度**：填充 `xdm.device.screenWidth`</li><li>**显示颜色深度**：填充 `xdm.device.colorDepth`</li></ul></li><li>**[!UICONTROL 浏览器]** 信息： <ul><li>**浏览器供应商**：填充 `xdm.environment.browserDetails.vendor`</li><li>**浏览器名称**：填充 `xdm.environment.browserDetails.name`</li><li>**浏览器版本**：填充 `xdm.environment.browserDetails.version`</li></ul></li><li>**[!UICONTROL 操作系统]** 信息： <ul><li>**操作系统供应商**：填充 `xdm.environment.operatingSystemVendor`</li><li>**操作系统名称**：填充 `xdm.environment.operatingSystem`</li><li>**操作系统版本**：填充 `xdm.environment.operatingSystemVersion`</li></ul></li></ul>无法收集设备查找信息以及用户代理和客户端提示。 选择收集设备信息会禁用用户代理和客户端提示的收集，反之亦然。 |
| **[!UICONTROL 不收集任何设备信息]** | 如果不想收集任何设备查找信息，请选择此选项。 未收集任何设备、硬件、浏览器、操作系统、用户代理或客户端提示数据。 |

如果启用以上任何字段进行数据收集，请确保正确设置 [`context`](../edge/data-collection/automatic-information.md) 数组属性，条件 [配置Web SDK](../edge/fundamentals/configuring-the-sdk.md).

设备和硬件信息使用 `context` 数组字符串 `"device"`，而浏览器和操作系统信息则使用 `context` 数组字符串 `"environment"`.

此外，请确保架构中存在每个所需的XDM字段。 如果不能，您可以添加Adobe提供的变量 `Environment Details` 字段组添加到您的架构。

### 配置高级选项 {#@advanced-options}

选择 **[!UICONTROL 高级选项]** 显示用于配置数据流的附加控件，如IP模糊处理、第一方ID Cookie等。

![高级配置选项](assets/configure/advanced-settings.png)

>[!IMPORTANT]
>
> 您有责任确保已获得适用法律和法规要求的所有必要的权限、同意、许可和授权，以收集、处理和传输个人数据，包括精确的地理位置信息。
> 
> 您选择的 IP 地址模糊处理方式不影响将从 IP 地址派生并发送到您配置的 Adobe 解决方案的地理位置信息的级别。必须单独限制或禁用地理位置查找。

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL IP 模糊处理] | 指示要应用于数据流的 IP 模糊处理的类型。任何基于客户 IP 的处理都将受 IP 模糊处理设置的影响。这包括从数据流接收数据的所有 Experience Cloud 服务。 <p>可用选项：</p> <ul><li>**[!UICONTROL 无]**：禁用 IP 模糊处理。完整的用户 IP 地址将通过数据流发送。</li><li>**[!UICONTROL 部分]**：对于 IPv4 地址，对用户 IP 地址的最后一个八位字节进行模糊处理。对于 IPv6 地址，对地址的最后 80 位进行模糊处理。 <p>示例：</p> <ul><li>IPv4：`1.2.3.4` -> `1.2.3.0`</li><li>IPv6：`2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL 完全]**：对整个 IP 地址进行模糊处理。 <p>示例：</p> <ul><li>IPv4：`1.2.3.4` -> `0.0.0.0`</li><li>IPv6：`2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> IP 模糊处理对其他 Adobe 产品的影响： <ul><li>**Adobe Target**：数据流级别 [!UICONTROL IP模糊处理] 在以下日期之前应用： [!UICONTROL IP模糊处理] 在Adobe Target中执行，针对请求中存在的所有IP地址。 例如，如果数据流级别 [!UICONTROL IP模糊处理] 选项设置为 **[!UICONTROL 完整]** 并且Adobe Target IP模糊处理选项设置为 **[!UICONTROL 最后一个八位字节模糊处理]**，Adobe Target会收到一个完全模糊处理的IP。 如果数据流级别 [!UICONTROL IP模糊处理] 选项设置为 **[!UICONTROL 部分]** 并且Adobe Target IP模糊处理选项设置为 **[!UICONTROL 完整]**， Adobe Target会收到一个部分模糊处理的IP，然后对其应用完全模糊处理。 Adobe Target IP模糊处理是独立于数据流进行管理的。 请参阅介绍 [IP 模糊处理](https://developer.adobe.com/target/before-implement/privacy/privacy/)和[地理定位](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html)的 Adobe Target 文档以了解更多详细信息。</li><li>**Audience Manager**：数据流级别 [!UICONTROL IP模糊处理] 设置先于 [!UICONTROL IP模糊处理] 在Audience Manager中执行，针对请求中存在的所有IP地址。 Audience Manager 完成的任何地理位置查找都将受数据流级别的 [!UICONTROL IP 模糊处理]选项的影响。Audience Manager 中基于完全模糊处理的 IP 的地理位置查找将生成未知区域，并且基于生成的地理位置数据的任何区段将无法实现。请参阅介绍 [IP 模糊处理](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html)的 Audience Manager 文档以了解更多详细信息。</li><li>**Adobe Analytics**：如果数据流级别的IP模糊处理设置设置为 **[!UICONTROL 完整]**， Adobe Analytics将IP地址视为空白。 这会影响任何依赖于IP地址的Analytics处理，例如地理位置查找和IP过滤。 要让Analytics接收未模糊处理或部分模糊处理的IP地址，请将IP模糊处理设置设置为 **[!UICONTROL 部分]** 或 **[!UICONTROL 无]**. 在Analytics中，可以进一步对部分模糊处理和未模糊处理的IP地址进行模糊处理。 请参阅 Adobe Analytics[文档](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html)以了解有关如何在 Analytics 中启用 IP 模糊处理的详细信息。如果IP地址被完全模糊处理，并且页面点击既没有 [!DNL ECID] 也不是 [!DNL VisitorID]，则Analytics将丢弃点击，而不是生成 [回退ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-ids.html?lang=zh-Hans)，这部分基于IP地址。</li></ul> |
| [!UICONTROL 第一方 ID Cookie] | 启用后，此设置将告知 Edge Network 在查找[第一方设备 ID](../edge/identity/first-party-device-ids.md) 时引用指定的 Cookie，而不是在“标识映射”中查找该值。<br><br>启用此设置时，您必须提供应存储 ID 的 Cookie 的名称。 |
| [!UICONTROL 第三方 ID 同步] | ID 同步可分组到容器中，以允许不同的 ID 同步在不同时间运行。启用后，此设置可让您指定为该数据流运行哪个 ID 同步容器。 |
| [!UICONTROL 第三方 ID 同步容器 ID] | 要用于第三方 ID 同步的容器的数字 ID。 |
| [!UICONTROL 容器 ID 覆盖] | 在此部分中，您可以定义其他第三方 ID 同步容器 ID，它们可用于覆盖默认 ID。 |
| [!UICONTROL 访问类型] | 为数据流定义 Edge Network 接受的身份验证类型。 <ul><li>**[!UICONTROL 混合身份验证]**：选择此选项时，Edge Network 接受经过身份验证和未经身份验证的请求。当您计划使用 Web SDK 或 [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) 与[服务器 API](../server-api/overview.md)，请选择此选项。 </li><li>**[!UICONTROL 仅经过身份验证]**：选择此选项时，Edge Network 仅接受经过身份验证的请求。当您计划仅使用服务器 API 并希望防止 Edge Network 处理任何未经身份验证的请求时，请选择此选项。</li></ul> |
| [!UICONTROL Media Analytics] | 选择此选项以启用通过Media SDK或Media Edge API为Edge Network集成处理Experience Platform流数据。 从了解Media Analytics [文档](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html). |

从该位置，如果您要为 Experience Platform 配置数据流，请按照[为数据收集准备数据](./data-prep.md)教程操作，在返回本指南之前将您的数据映射到 Platform 事件架构。否则，请选择&#x200B;**[!UICONTROL 保存]**&#x200B;并继续下一部分。

## 查看数据流详细信息 {#view-details}

在配置新的数据流或选择要查看的现有数据流后，将显示该数据流的详细信息页面。在该页面中，可以找到有关数据流的更多信息，包括其 ID。

![创建的数据流的详细信息页面](assets/configure/view-details.png)

从数据流详细信息屏幕中，可以[添加服务](#add-services)以启用您有权访问的 Adobe Experience Cloud 产品中的功能。您还可以编辑数据流的[基本配置](#create)、更新其[映射规则](./data-prep.md)、[复制数据流](#copy)或将其完全删除。

## 将服务添加到数据流 {#add-services}

在数据流的详细信息页面上，选择&#x200B;**[!UICONTROL 添加服务]**&#x200B;以开始为该数据流添加可用服务。

![选择“添加服务”以继续](assets/configure/add-service.png)

在下一个屏幕上，使用下拉菜单选择要为此数据流配置的服务。仅您有权访问的服务将显示在此列表中。

![从列表中选择服务](assets/configure/service-selection.png)

选择所需的服务，填写显示的配置选项，然后选择&#x200B;**[!UICONTROL 保存]**&#x200B;以将服务添加到数据流。所有添加的服务都会显示在数据流的详细信息视图中。

![添加到数据流的服务](assets/configure/services-added.png)

以下子部分描述了每项服务的配置选项。

>[!NOTE]
>
>每个服务配置均包含一个&#x200B;**[!UICONTROL 已启用]**&#x200B;开关，它在选择服务时自动激活。要禁用此数据流的选定服务，请再次选择&#x200B;**[!UICONTROL 已启用]**&#x200B;开关。

### Adobe Analytics 设置 {#analytics}

此服务控制数据是否以及如何发送到 Adobe Analytics。可以在有关[将数据发送到 Analytics](../edge/data-collection/adobe-analytics/analytics-overview.md) 的指南中找到其他详细信息。

![Adobe Analytics 设置块](assets/configure/analytics-config.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL 报表包 ID] | **（必需）**&#x200B;要将数据发送到的 Analytics 报表包的 ID。可以在 Adobe Analytics UI 中的[!UICONTROL 管理员] > [!UICONTROL 报表包]下找到此 ID。如果指定了多个报表包，则数据将复制到每个报表包。 |
| [!UICONTROL 报表包覆盖] | 在此部分中，您可以添加其他报表包 ID，它们可用于覆盖默认报表包 ID。 |

### Adobe Audience Manager 设置 {#audience-manager}

此服务控制数据是否以及如何发送到 Adobe Audience Manager。只需启用此部分即可将数据发送到 Audience Manager。其他设置是可选的，但建议使用。

![Adobe Audience Manager 设置块](assets/configure/audience-manager-config.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL 已启用 Cookie 目标] | 允许 SDK 通过 [Cookie 目标](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)从 [!DNL Audience Manager] 共享区段信息。 |
| [!UICONTROL 已启用 URL 目标] | 允许 SDK 通过 [URL 目标](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)从 [!DNL Audience Manager] 共享区段信息。 |

### Adobe Experience Platform 设置 {#aep}

>[!IMPORTANT]
>
>为 Platform 启用数据流时，请记下您当前正在使用的 Platform 沙盒，如 UI 的顶部功能区中所示。
>
>![选定的沙盒](assets/configure/platform-sandbox.png)
>
>沙盒是 Adobe Experience Platform 中的虚拟分区，可让您将您的数据和实施与组织中的其他数据和实施隔离开来。一旦创建数据流，其沙盒便无法更改。有关沙盒在 Experience Platform 中发挥的作用的更多详细信息，请参阅[沙盒文档](../sandboxes/home.md)。

此服务控制数据是否以及如何发送到 Adobe Experience Platform。

![Adobe Experience Platform 设置块](assets/configure/platform-config.png)

| 设置 | 描述 |
|---| --- |
| [!UICONTROL 事件数据集] | **（必需）**&#x200B;选择客户事件数据将流式传输到的 Platform 数据集。此架构必须使用 [XDM ExperienceEvent 类](../xdm/classes/experienceevent.md)。要添加其他数据集，请选择&#x200B;**[!UICONTROL 添加事件数据集]**。 |
| [!UICONTROL 配置文件数据集] | 选择客户属性数据将发送到的 Platform 数据集。此架构必须使用 [XDM 单个配置文件类](../xdm/classes/individual-profile.md)。 |
| [!UICONTROL Offer Decisioning] | 选中此复选框可为 Platform Web SDK 实施启用 Offer Decisioning。请参阅有关[通过 Platform Web SDK 使用 Offer Decisioning](../edge/personalization/offer-decisioning/offer-decisioning-overview.md) 的指南以了解更多实施详细信息。<br><br>有关 Offer Decisioning 功能的更多信息，请参阅 [Adobe Journey Optimizer 文档](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=zh-Hans)。 |
| [!UICONTROL 边缘分段] | 选中此复选框可为该数据流启用[边缘分段](../segmentation/ui/edge-segmentation.md)。当 SDK 通过支持边缘分段的数据流发送数据时，相关配置文件的任何更新的分段成员资格将在响应中发送回。<br><br>对于[下一页个性化用例](../destinations/ui/activate-edge-personalization-destinations.md)，此选项可与[!UICONTROL 个性化目标]结合使用。 |
| [!UICONTROL 个性化目标] | 如果在选中[!UICONTROL 边缘分段]复选框后启用此选项，将允许数据流连接到个性化目标，例如[自定义个性化](../destinations/catalog/personalization/custom-personalization.md)。<br><br>有关[配置个性化目标](../destinations/ui/activate-edge-personalization-destinations.md)的具体步骤，请参阅目标文档。 |
| [!UICONTROL Adobe Journey Optimizer] | 选中此复选框可为该数据流启用 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)。<br><br> 启用此选项将允许数据流从 [!DNL Adobe Journey Optimizer] 中基于 Web 和应用程序的入站营销活动返回个性化内容。此选项要求[!UICONTROL 边缘分段]处于活动状态。如果[!UICONTROL 边缘分段]未选中，此选项将灰显。 |

### Adobe Target 设置 {#target}

此服务控制数据是否以及如何发送到 Adobe Target。

![Adobe Target 设置块](assets/configure/target-config.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL 属性令牌] | [!DNL Target] 允许客户通过使用属性来控制权限。有关属性的更多信息，请参阅 [!DNL Target] 文档中有关[配置企业权限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html)的指南。<br><br>可以在 Adobe Target UI 中的[!UICONTROL 设置] > [!UICONTROL 属性]下找到属性令牌。 |
| [!UICONTROL Target 环境 ID] | [Adobe Target 中的环境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html)可帮助您在开发过程的所有阶段管理实施。此设置指定您将用于此数据流的环境。<br><br>最佳实践是为每个 `dev`、`stage` 和 `prod` 数据流环境进行不同设置，以简化操作。但是，如果您已定义 Adobe Target 环境，则可以使用这些环境。 |
| [!UICONTROL Target 第三方 ID 命名空间] | 要用于此数据流的 `mbox3rdPartyId` 的标识命名空间。有关更多信息，请参阅有关[使用 Web SDK 实施 `mbox3rdPartyId`](../edge/personalization/adobe-target/using-mbox-3rdpartyid.md) 的指南。 |
| [!UICONTROL 属性令牌覆盖] | 在此部分中，您可以定义可用于覆盖默认属性令牌的其他属性令牌。 |

### [!UICONTROL 事件转发]设置

此服务控制数据是否以及如何发送到[事件转发](../tags/ui/event-forwarding/overview.md)。

![配置 UI 的“事件转发”部分](assets/configure/event-forwarding-config.png)

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL Launch 属性] | **（必需）**&#x200B;要将数据发送到的事件转发属性。 |
| [!UICONTROL Launch 环境] | **（必需）**&#x200B;要将数据发送到的所选属性中的环境。 |

>[!NOTE]
>
>您可以选择&#x200B;**[!UICONTROL 手动输入 ID]** 以键入属性和环境名称，而不是使用下拉菜单。

## 复制数据流 {#copy}

您可以创建现有数据流的副本并根据需要更改其详细信息。

>[!NOTE]
>
>数据流只能在同一个[沙盒](../sandboxes/home.md)中复制。换句话说，您无法将数据流从一个沙盒复制到另一个沙盒。

从[!UICONTROL 数据流]工作区的主页中，为相关数据流选择省略号 (**....**)，然后选择&#x200B;**[!UICONTROL 复制]**。

![显示将从数据流列表视图中选择的[!UICONTROL 复制]选项的图像](assets/configure/copy-datastream-list.png)

或者，您可以从给定数据流的详细信息视图中选择&#x200B;**[!UICONTROL 复制数据流]**。

![显示将从数据流详细信息视图中选择的[!UICONTROL 复制]选项的图像](assets/configure/copy-datastream-details.png)

将出现一个确认对话框，提示您为要创建的新数据流提供唯一名称，以及有关将复制的配置选项的详细信息。准备就绪后，选择&#x200B;**[!UICONTROL 复制]**。

![用于复制数据流的确认对话框的图像](assets/configure/copy-datastream-confirm.png)

[!UICONTROL 数据流]工作区的主页将重新出现，并列出了新数据流。

## 后续步骤

本指南介绍如何在数据收集 UI 中管理数据流。有关如何在设置数据流后安装和配置 Web SDK 的更多信息，请参阅[数据收集 E2E 指南](../collection/e2e.md#install)。
