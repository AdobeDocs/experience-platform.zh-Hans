---
title: 目标激活工作流程中的身份处理
description: 了解如何在激活工作流中处理身份导出，具体取决于目标类型
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 3%

---

# 目标激活工作流程中的身份处理

本页介绍如何将身份导出到不同的目标类型的特性，并教您如何根据目标找到可以导出的身份。

>[!TIP]
>
> 有关身份、身份命名空间以及与身份相关的术语的定义的更多信息，请参阅 [identity service概述](/help/identity-service/home.md).

中的每个目标 [目录](/help/destinations/catalog/overview.md) 略有不同，因此没有在所有目标上设置一刀切的设置。 但是，有一些模式可指导目标的设置及其身份要求，如下节所述。

## 基于文件的目标 {#file-based}

对象 [基于文件的目标](/help/destinations/destination-types.md#file-based) (例如 [!DNL Amazon S3]、 SFTP、大多数电子邮件营销目标，如 [!DNL Adobe Campaign]， [!DNL Oracle Eloqua]， [!DNL Salesforce Marketing Cloud])，则其中大多数目标的身份设置是开放的，这意味着您无需在 [选择属性](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) 批量激活工作流的步骤。

如果您选择向文件导出添加标识，请注意，只能从 [身份命名空间](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) 可以在导出中选择。 选择要导出的标识时，会自动将其选为 [必需属性](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) 和 [重复数据删除键](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![选定为强制属性和重复数据删除键的标识。](/help/destinations/assets/how-destinations-work/selected-identity.png)

作为解决方法，如果这些标识已作为属性引入Experience Platform，则可以向导出添加更多标识。 请参阅下面的示例，其中除了身份命名空间之外，还选择了XDM属性电子邮件地址进行导出 `Phone_E.164`.

![为导出选择的电子邮件地址属性示例。](/help/destinations/assets/how-destinations-work/email-selected.png)

## 从身份映射导出身份与将身份导出为XDM属性 — 区别 {#identity-map-or-attribute}

根据您是从标识映射中选择导出标识还是选择已作为属性引入到Experience Platform中的标识，导出的记录数可能会有所不同。 [合并策略](/help/profile/merge-policies/overview.md) 另外，当您从身份映射中选择身份时，在导出记录的数目方面也会起到重要作用。

例如，假定从两个不同的数据集，您具有以下配置文件片段，这些片段将合并到单个客户配置文件中：

**配置文件片段一**

| 标识映射 | 名字 | 姓氏 | 电子邮件属性 |
|---------|----------|---------|--------|
| 电子邮件1，忠诚度ID1 | John | Doe | 电子邮件1 |


**配置文件片段二**

| 标识映射 | 名字 | 姓氏 | 电子邮件属性 |
|---------|----------|---------|--------|
| 电子邮件2，忠诚度ID1 | John | Doe | 电子邮件2 |

合并后的用户档案如下所示：

| 标识映射 | 名字 | 姓氏 | 电子邮件属性 |
|---------|----------|---------|--------|
| 电子邮件1、电子邮件2、忠诚度ID1 | John | Doe | 电子邮件2 |

导出行为会因您选择的 `IdentityMap: Email` 或 `xdm: personalEmail.address` 以导出。

如果客户激活 `IdentityMap: Email`，导出的文件中将有两个记录，一个用于email1，另一个用于email2。

但是，如果客户激活 `xdm: personalEmail.address`，记录中仅存在email2 ，因为email attribute字段仅包含email2。 这些情形可以解决不同的用例，在这些用例中，您可能希望激活到您为某个客户归档的所有电子邮件地址，或者仅激活到您为某个客户归档的最新电子邮件地址。

由此得出的结论是，您导出的记录数取决于您选择的合并策略以及在导出中选择的是身份还是属性。

## 基于API的流目标 {#streaming-destinations}

[基于API的流目标](/help/destinations/destination-types.md#streaming-destination) 构建方式 [Destination SDK](/help/destinations/destination-sdk/overview.md) (例如 [!DNL Facebook]， [!DNL Google Customer Match]， [!DNL Pinterest]， [!DNL Braze]、及其他)仅支持特定的ID用于导出。 有关可导出到每个目标的特定身份的详细信息，请阅读 *支持的身份* 部分(例如，请参阅 [支持的身份部分](/help/destinations/catalog/advertising/pinterest.md) 在 [!DNL Pinterest] 目标页面)。

但请注意，您可以灵活地从以下任一位置使用数据： [专用图](/help/profile/merge-policies/overview.md#id-stitching) 或属性中的身份进行标识。 这意味着您可以将XDM属性映射到目标所需的标识字段。 请参阅下面的示例， [!DNL Pinterest] XDM属性的目标 `personalEmail.address` 映射到所需的 [!DNL Pinterest] 身份 `pinterest_audience`.

>[!TIP]
>
>当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项使Experience Platform在激活时自动散列数据。 详细了解 **[!UICONTROL 应用转换]** 中的选项 [流目标激活教程](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![映射到Pinterest目标的身份字段的电子邮件地址属性示例。](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### 依赖第三方Cookie集成的广告目标 {#third-party-cookie-destinations}

依赖第三方Cookie的广告目标(例如： [!DNL Google Ads]， [!DNL Google Ad Manager]， [!DNL Google DV360]， [!DNL Bing]， [!DNL The Trade Desk])不需要客户在激活工作流中选择ID。 对于这些目标，在设置激活工作流时，Experience Platform会自动查找由构建的身份匹配表 [[!UICONTROL Experience CloudID服务]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans) 和会导出配置文件可用且受目标支持的所有身份。

这些目标要求通过 [!UICONTROL Experience CloudID服务] 或通过 [!UICONTROL Experience PlatformWeb SDK].

如果您使用 [!UICONTROL Experience PlatformWeb SDK] 和旧版 [!UICONTROL Experience CloudID服务] 未在页面上实施，则需要确保相关网站的数据流已启用，以允许同步第三方ID，如中所述 [配置数据流文档](/help/datastreams/configure.md#create).

在按照上面链接的文档中的说明配置数据流时，您需要确保 **[!UICONTROL 第三方ID同步]** 已启用滑块。 大多数客户会离开 `container_id` 字段为空（默认为0）。 仅当旧版Audience Manager实施使用特定的容器ID时，才需要更改此值（但请注意，这将是绝大多数客户）。

>[!NOTE]
>
>Audience Manager支持这些广告目标中的大多数(这些目标类型在Audience Manager中称为基于设备的目标)。 查看 [Audience Manager中所有受支持的基于设备的目标列表](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html))。 Experience Platform中只列出少数几个。 有关在Experience Platform和Audience Manager之间共享数据的信息，请阅读以下部分： [启用在Experience Platform与Audience Manager之间共享数据](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#enable-aep-to-aam-data). 目前，没有计划支持更多第三方Cookie目标。

## 企业目标 {#enterprise-destinations}

[企业目标](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis]， [!DNL Azure Event Hubs]、HTTP API)在数据导出中不需要特定ID，因为这些特定ID专为企业集成用例而设计。 但是，您可以根据需要将身份导出为XDM属性或从身份映射中导出。 查看 [将数据导出到HTTP目标的示例](/help/destinations/catalog/streaming/http-destination.md#exported-data)，包括两项 `personalEmail.address` XDM属性和身份 `ECID` 和 `email_lc_sha256` （经过哈希处理的电子邮件地址）。

## 个性化目标 {#personalization-destinations}

[个性化（或边缘）目标](/help/destinations/destination-types.md#edge-personalization-destinations) (例如：Adobe Target、 [!DNL Custom Personalization])在激活工作流中不需要任何身份选择，因为集成是用户档案查找。 客户端([!DNL Target]， [!DNL Web SDK]，或其他)查询 [[!UICONTROL Edge]](/help/collection/home.md#edge) 并提取所需的用户档案信息以进行现场个性化。

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## 后续步骤 {#next-steps}

在阅读本文档后，您现在知道如何找出各个目标支持或所需的身份。 您现在还了解了身份选择如何用于每种目标类型。

接下来，您可以阅读以下内容 [导出设置](/help/destinations/how-destinations-work/destinations-configurations.md) 对于目标，这在所有目标类型中都是通用的，开发人员可以在单个目标级别上配置这些目标类型，并且用户可以在激活工作流中编辑哪些设置。

您还可以查看以下位置的所有可用目标： [目录](/help/destinations/catalog/overview.md).
