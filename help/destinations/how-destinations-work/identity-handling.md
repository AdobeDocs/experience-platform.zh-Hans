---
title: 目标激活工作流中的身份处理
description: 了解激活工作流中如何处理身份导出，具体取决于目标类型
source-git-commit: 372231ab4fc1148c1c2c0c5fdbfd3cd5328b17cc
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 1%

---

# 目标激活工作流中的身份处理

本页介绍如何将身份导出到不同的目标类型，并教您如何根据目标查找可导出的身份。

>[!TIP]
>
> 有关身份、身份命名空间和身份相关术语定义的详细信息，请阅读 [identity service概述](/help/identity-service/home.md).

中的每个目标 [目录](/help/destinations/catalog/overview.md) 略有不同，因此没有跨所有目标进行一刀切的设置。 但是，有一些模式可指导目标的设置及其身份要求，如以下各节所述。

## 基于文件的目标 {#file-based}

对于 [基于文件的目标](/help/destinations/destination-types.md#file-based) (例如 [!DNL Amazon S3]、SFTP，大多数电子邮件营销目标，例如 [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud])，则这些目标中的大多数身份设置都是打开的，这意味着您无需在 [选择属性](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) 批量激活工作流的步骤。

如果选择向文件导出中添加标识，请注意， [标识命名空间](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) 可在导出中选择。 当您选择要导出的标识时，系统会自动将其选作 [强制属性](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) 和 [重复数据删除键](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![选择作为强制属性和重复数据删除键的标识。](/help/destinations/assets/how-destinations-work/selected-identity.png)

作为解决方法，如果已将身份作为属性引入Experience Platform中，则可以向导出中添加更多标识。 请参阅以下示例，其中除了标识命名空间之外，还选择了XDM属性电子邮件地址进行导出 `Phone_E.164`.

![选择导出的电子邮件地址属性的示例。](/help/destinations/assets/how-destinations-work/email-selected.png)

## 从身份映射导出身份与将身份导出为XDM属性 — 区别 {#identity-map-or-attribute}

导出的记录数可能不同，具体取决于您是从身份映射中选择导出身份，还是已作为属性引入Experience Platform的身份。 [合并策略](/help/profile/merge-policies/overview.md) 此外，在从身份映射中选择身份时，还会在导出的记录数中发挥重要作用。

例如，假定从两个不同的数据集中，您具有以下将合并到单个客户配置文件中的配置文件片段：

**配置文件片段1**

| 身份映射 | 名字 | 姓氏 | 电子邮件属性 |
|---------|----------|---------|--------|
| email1，忠诚度ID1 | 约翰 | Doe | 电子邮件1 |


**配置文件片段2**

| 身份映射 | 名字 | 姓氏 | 电子邮件属性 |
|---------|----------|---------|--------|
| email2，忠诚度ID1 | 约翰 | Doe | 电子邮件2 |

合并的用户档案如下所示：

| 身份映射 | 名字 | 姓氏 | 电子邮件属性 |
|---------|----------|---------|--------|
| 电子邮件1，电子邮件2，忠诚度ID1 | 约翰 | Doe | 电子邮件2 |

根据您是否选择了 `IdentityMap: Email` 或 `xdm: personalEmail.address` 导出时。

如果客户激活 `IdentityMap: Email`，则导出文件中将有两个记录，一个用于email1，另一个用于email2。

但是，如果客户激活 `xdm: personalEmail.address`，则记录中将仅显示email2，因为email属性字段仅包含email2。 这些情况可能涉及不同的用例，您可能希望激活到您为客户存档的所有电子邮件地址，或者仅激活到您为客户存档的最新电子邮件地址。

另外，您导出的记录数取决于您选择的合并策略以及您是否在导出中选择了标识或属性。

## 基于API的流目标 {#streaming-destinations}

[基于API的流目标](/help/destinations/destination-types.md#streaming-destination) 内置 [Destination SDK](/help/destinations/destination-sdk/overview.md) (例如 [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze]等)仅支持特定的ID进行导出。 有关可导出到每个目标的特定标识的详细信息，请阅读 *受支持身份* 部分(例如，请参阅 [受支持标识部分](/help/destinations/catalog/advertising/pinterest.md) 在 [!DNL Pinterest] 目标页面)。

但请注意，您可以灵活地使用 [专用图](/help/profile/merge-policies/overview.md#id-stitching) 或属性作为标识。 这意味着您可以将XDM属性映射到目标所需的标识字段。 请参阅下面的示例 [!DNL Pinterest] 目标，其中XDM属性 `personalEmail.address` 映射到所需 [!DNL Pinterest] 身份 `pinterest_audience`.

>[!TIP]
>
>当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项，让Experience Platform自动对激活时的数据进行哈希处理。 有关 **[!UICONTROL 应用转换]** 选项 [流目标激活教程](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![映射到Pinterest目标标识字段的电子邮件地址属性示例。](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### 依赖第三方Cookie集成的广告目标 {#third-party-cookie-destinations}

依赖第三方Cookie的广告目标(例如： [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk])不要求客户在激活工作流中选择ID。 对于这些目标，在设置激活工作流时，Experience Platform会自动查找由 [[!UICONTROL Experience CloudID服务]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en) 和会导出可用于用户档案且受目标支持的所有身份。

这些目标需要通过 [!UICONTROL Experience CloudID服务] 或 [!UICONTROL Experience PlatformWeb SDK].

如果您使用 [!UICONTROL Experience PlatformWeb SDK] 和遗产 [!UICONTROL Experience CloudID服务] 未在页面上实施，则您需要确保相关网站的数据流已启用，以允许进行第三方ID同步，如 [配置数据流文档](/help/edge/datastreams/configure.md#create).

按照以上链接的文档中所述配置数据流时，您需要确保 **[!UICONTROL 第三方ID同步]** 滑块已启用。 大多数客户会离开 `container_id` 字段留空（默认为0）。 仅当旧版Audience Manager实施使用了特定的容器ID时，您才需要更改此值（但请注意，这将是绝大多数客户所需的容器ID）。

>[!NOTE]
>
>这些广告目标中的大多数都受Audience Manager支持(这些目标类型在Audience Manager中称为基于设备的目标。 查看 [Audience Manager中所有受支持的基于设备的目标列表](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en))。 Experience Platform中只列出少数内容。 有关在Experience Platform和Audience Manager之间共享数据的信息，请阅读 [启用从Experience Platform到Audience Manager的数据共享](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data). 目前，没有计划支持更多第三方Cookie目标。

## 企业目标 {#enterprise-destinations}

[企业目标](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], HTTP API)在数据导出中不需要特定ID，因为这些ID是为企业集成用例设计的。 但是，您可以将身份导出为XDM属性，也可以根据需要从身份映射中导出。 查看 [将数据导出到HTTP目标的示例](/help/destinations/catalog/streaming/http-destination.md#exported-data)，包括 `personalEmail.address` XDM属性和标识 `ECID` 和 `email_lc_sha256` （经过哈希处理的电子邮件地址）。

## 个性化目标 {#personalization-destinations}

[个性化（或边缘）目标](/help/destinations/destination-types.md#edge-personalization-destinations) (例如：Adobe Target, [!DNL Custom Personalization])不需要在激活工作流中选择任何身份，因为集成是用户档案查找。 客户端([!DNL Target], [!DNL Web SDK]，或其他)查询 [[!UICONTROL Edge]](/help/collection/home.md#edge) 并提取网站个性化所需的用户档案信息。

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何确定各个目标支持或需要哪些身份。 您现在还可以了解身份选择如何适用于每个目标类型。

接下来，您可以阅读 [导出设置](/help/destinations/how-destinations-work/destinations-configurations.md) 目标类型在目标中很常见，可由开发人员在单个目标级别配置目标，并且用户可以在激活工作流中编辑哪些设置。

您还可以在 [目录](/help/destinations/catalog/overview.md).