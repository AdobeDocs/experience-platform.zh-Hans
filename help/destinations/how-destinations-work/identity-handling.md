---
title: 目标激活工作流中的身份处理
description: 了解如何在激活工作流中处理身份导出，具体取决于目标类型
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: 322510055bd8b8803292a2b4af9df9e1dbee7ffb
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# 目标激活工作流中的身份处理

本页介绍如何将身份导出到不同的目标类型的特性，并教您如何根据目标找到可以导出的身份。

>[!TIP]
>
> 有关身份、身份命名空间以及与身份相关的术语的定义的更多信息，请阅读[身份服务概述](/help/identity-service/home.md)。

[目录](/help/destinations/catalog/overview.md)中的每个目标略有不同，因此没有对所有目标进行一刀切的设置。 但是，有一些模式可指导目标的设置及其身份要求，如下节所述。

## 基于文件的目标 {#file-based}

对于[基于文件的目标](/help/destinations/destination-types.md#file-based)（例如[!DNL Amazon S3]、SFTP、大多数电子邮件营销目标，如[!DNL Adobe Campaign]、[!DNL Oracle Eloqua]、[!DNL Salesforce Marketing Cloud]），其中大多数目标的标识设置处于打开状态，这意味着您无需在批量激活工作流的[选择属性](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)步骤中选择任何标识。

如果您选择将标识添加到文件导出，请注意，在导出中只能选择[标识命名空间](/help/identity-service/features/identity-graph-viewer.md#access-identity-graph-viewer)中的单个标识。 在选择要导出的标识时，会自动将其选为[强制属性](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes)和[重复数据删除键](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys)。

![选为必需属性和重复数据删除键的标识。](/help/destinations/assets/how-destinations-work/selected-identity.png)

作为解决方法，如果这些标识已作为属性引入Experience Platform，则可以向导出添加更多标识。 请参阅下面的示例，其中除了身份命名空间`Phone_E.164`之外，还选择了XDM属性电子邮件地址进行导出。

![为导出选择的电子邮件地址属性示例。](/help/destinations/assets/how-destinations-work/email-selected.png)

## 从身份映射导出身份与将身份导出为XDM属性 — 区别 {#identity-map-or-attribute}

根据您是从标识映射中选择导出标识还是选择已作为属性引入到Experience Platform中的标识，导出的记录数可能会有所不同。 当您从标识映射中选择标识时，[合并策略](/help/profile/merge-policies/overview.md)在导出的记录数中也扮演着重要角色。

例如，假定从两个不同的数据集，您具有以下配置文件片段，这些片段将合并到单个客户配置文件中：

**个人资料片段一**

| 标识映射 | 名字 | 姓氏 | 电子邮件属性 |
|---------|----------|---------|--------|
| 电子邮件1，忠诚度ID1 | John | Doe | 电子邮件1 |


**个人资料片段二**

| 标识映射 | 名字 | 姓氏 | 电子邮件属性 |
|---------|----------|---------|--------|
| 电子邮件2，忠诚度ID1 | John | Doe | 电子邮件2 |

合并后的用户档案如下所示：

| 标识映射 | 名字 | 姓氏 | 电子邮件属性 |
|---------|----------|---------|--------|
| 电子邮件1、电子邮件2、忠诚度ID1 | John | Doe | 电子邮件2 |

导出行为因您选择`IdentityMap: Email`还是`xdm: personalEmail.address`进行导出而有所不同。

如果客户激活`IdentityMap: Email`，导出的文件中将有两个记录，一个用于email1，另一个用于email2。

但是，如果客户激活`xdm: personalEmail.address`，则记录中仅存在email2，因为email attribute字段仅包含email2。 这些情形可以解决不同的用例，在这些用例中，您可能希望激活到您为某个客户归档的所有电子邮件地址，或者仅激活到您为某个客户归档的最新电子邮件地址。

由此得出的结论是，您导出的记录数取决于您选择的合并策略以及在导出中选择的是身份还是属性。

## 基于API的流目标 {#streaming-destinations}

基于[API的流目标](/help/destinations/destination-types.md#streaming-destination)使用[Destination SDK](/help/destinations/destination-sdk/overview.md)生成（例如[!DNL Facebook]、[!DNL Google Customer Match]、[!DNL Pinterest]、[!DNL Braze]等）仅支持特定ID进行导出。 有关可导出到每个目标的特定标识的详细信息，请阅读每个目标文档页面中的&#x200B;*支持的标识*&#x200B;部分（例如，请参阅[!DNL Pinterest]目标页面中的[支持的标识部分](/help/destinations/catalog/advertising/pinterest.md)）。

但请注意，您可以灵活地使用[专用图](/help/profile/merge-policies/overview.md#id-stitching)或属性中的数据作为标识。 这意味着您可以将XDM属性映射到目标所需的标识字段。 查看[!DNL Pinterest]目标的以下示例，其中XDM属性`personalEmail.address`映射到所需的[!DNL Pinterest]标识`pinterest_audience`。

>[!TIP]
>
>当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使Experience Platform在激活时自动对数据进行哈希处理。 详细了解[流式目标激活教程](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation)中的&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项。

![映射到Pinterest目标的标识字段的电子邮件地址属性示例。](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### 依赖第三方Cookie集成的Advertising目标 {#third-party-cookie-destinations}

依赖第三方Cookie的Advertising目标（例如： [!DNL Google Ads]、[!DNL Google Ad Manager]、[!DNL Google DV360]、[!DNL Bing]、[!DNL The Trade Desk]）不要求客户在激活工作流中选择ID。 对于这些目标，在设置激活工作流时，Experience Platform会自动查找由[[!UICONTROL Experience CloudID服务]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans)构建的标识匹配表，并导出配置文件可用的以及目标支持的所有标识。

这些目标需要通过[!UICONTROL Experience CloudID服务]或通过[!UICONTROL Experience PlatformWeb SDK]进行ID同步。

如果您使用的是[!UICONTROL Experience PlatformWeb SDK]，并且页面上未实现旧版[!UICONTROL Experience CloudID服务]，则需要确保相关网站的数据流已启用，以允许第三方ID同步，如[配置数据流文档](/help/datastreams/configure.md#create)中所述。

在按照上面链接的文档中的说明配置数据流时，您需要确保启用&#x200B;**[!UICONTROL 第三方ID同步]**&#x200B;滑块。 大多数客户会将`container_id`字段留空（默认为0）。 仅当旧版Audience Manager实施使用特定的容器ID时，才需要更改此值（但请注意，这将是绝大多数客户）。

>[!NOTE]
>
>Audience Manager支持这些广告目标中的大多数(这些目标类型在Audience Manager中称为基于设备的目标)。 查看Audience Manager[&#128279;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=zh-Hans)中所有支持的基于设备的目标的列表。 Experience Platform中只列出少数几个。 有关在Experience Platform和Audience Manager之间共享数据的信息，请阅读[中有关启用从Experience Platform到Audience Manager的数据共享](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=zh-Hans#enable-aep-to-aam-data)的部分。 目前，没有计划支持更多第三方Cookie目标。

## 企业目标 {#enterprise-destinations}

[企业目标](/help/destinations/destination-types.md#advanced-enterprise-destinations) ([!DNL Amazon Kinesis]、[!DNL Azure Event Hubs]、HTTP API)在数据导出中不需要特定ID，因为这些是专为企业集成用例设计的。 但是，您可以根据需要将身份导出为XDM属性或从身份映射中导出。 查看导出到HTTP目标[&#128279;](/help/destinations/catalog/streaming/http-destination.md#exported-data)的数据的示例，其中包含`personalEmail.address` XDM属性以及标识映射中的标识`ECID`和`email_lc_sha256`（经过哈希处理的电子邮件地址）。

## Personalization目标 {#personalization-destinations}

[Personalization（或edge）目标](/help/destinations/destination-types.md#edge-personalization-destinations)(例如：Adobe Target，[!DNL Custom Personalization])不需要在激活工作流中选择任何标识，因为集成是配置文件查找。 客户端（[!DNL Target]、[!DNL Web SDK]或其他）查询[[!UICONTROL Edge]](/help/collection/home.md#edge)，并提取它进行现场个性化所需的配置文件信息。

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## 后续步骤 {#next-steps}

在阅读本文档后，您现在知道如何找出各个目标支持或所需的身份。 您现在还了解了身份选择如何用于每种目标类型。

接下来，您可以了解哪些目标的[导出设置](/help/destinations/how-destinations-work/destinations-configurations.md)在目标类型中是通用的，开发人员可以在单个目标级别上配置这些设置，以及用户在激活工作流中可以编辑哪些设置。

您还可以签出[目录](/help/destinations/catalog/overview.md)中的所有可用目标。
