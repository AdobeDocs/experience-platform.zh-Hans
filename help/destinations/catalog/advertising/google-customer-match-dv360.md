---
title: Google客户匹配+显示和视频360连接
description: 借助Google Customer Match + Display & Video 360目标连接器，您可以使用Experience Platform中的在线和离线数据在Google自有和运营的资产(如Search、Shopping、Gmail和YouTube)中与客户联系并重新互动。
badge: 有限发布版
exl-id: f6da3eae-bf3f-401a-99a1-2cca9a9058d2
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 5%

---

# [!DNL Google Customer Match + Display & Video 360]连接

>[!NOTE]
>
>**Google Customer Match + Display &amp; Video 360连接器的可用性有限**<br>&#x200B;随着我们与Google的集成进入到成熟的整个生命周期，我们会看到指出实施中需要更正的弱点的数据，只有这样才能获得更广泛的采用。 鉴于这些担忧，Adobe已将此目标的可见性降低到有限数量的客户。 我们正在与Google积极交谈，以改善产品体验。 我们理解这可能是一个令人失望的消息，但我们相信，这是确保为我们的客户提供高质量、可靠体验的负责任方法。</br>

使用此目标将您的第一方基于PII的[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en)列表直接激活到[!DNL Google Display & Video 360]属性，如[!DNL Search]、[!DNL YouTube]、[!DNL Gmail]和[!DNL Google Display Network]。

某些Google集成的第三方(如Adobe Real-Time CDP)可以使用[!DNL Google Audience Partner API]直接在客户的[!DNL Customer Match]帐户中创建[!DNL Display & Video 360]受众。

由于新引入的功能能够在[!DNL Customer Matched]中利用[!DNL Display & Video 360]受众，您现在可以在扩展的清单源名册中定位受众。

Adobe Experience Platform UI中的![Google Customer Match + DV360目标。](/help/destinations/assets/catalog/advertising/gcm-dv360/catalog.png)

## 与欧盟的更新同意要求相关的Google目标更改的重要通知

>[!IMPORTANT]
>
> Google将发布对[Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)和[Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)的更改，以支持欧盟（[EU用户同意政策](https://digital-markets-act.ec.europa.eu/index_en)）中[Digital Markets Act](https://www.google.com/about/company/user-consent-policy/) (DMA)定义的合规性和同意相关要求。 自2024年3月6日起，将开始实施对同意要求的这些更改。
><br/>
>为了遵循欧盟用户同意政策并继续为欧洲经济区(EEA)中的用户创建受众列表，广告商和合作伙伴必须确保他们在上传受众数据时获得最终用户同意。 作为 Google 合作伙伴，Adobe 为您提供必要的工具，以遵守欧盟 DMA 下的这些同意要求。
><br/>
>如果客户购买了Adobe Privacy &amp; Security Shield并配置了[同意策略](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)以过滤掉未经同意的用户档案，则无需采取任何操作。
><br/>
>未购买Adobe Privacy &amp; Security Shield的客户必须使用[区段生成器](../../../segmentation/home.md#segment-definitions)中的[区段定义](../../../segmentation/ui/segment-builder.md)功能来过滤掉未经同意的用户档案，以便继续使用现有的Real-Time CDP Google目标而不中断。

## 何时使用此目标

目标目录中提供了与Google的多个集成，并且可能很难了解何时使用每个可用的Google目标。 阅读下表中的信息，了解不同的用例：

| [Google 目标客户匹配功能](/help/destinations/catalog/advertising/google-customer-match.md) | [Google显示和视频360](/help/destinations/catalog/advertising/google-dv360.md) | [!DNL Google Customer Match] + [!DNL Display & Video 360] （此连接器） |
|---------|----------|---------|
| 导出基于PII的受众，并根据[!DNL Google Customer Match]中提供的清单联系他们。 | 在可通过[!DNL Google Display & Video 360]查看的库存、Google拥有并运营的资产（如Youtube和[!DNL Search]）及其他位置上覆盖基于Cookie的受众。 | 在[!DNL Google Customer Match]中创建基于PII的受众，并在[!DNL Google Display & Video 360]中可用的清单中仅在Google拥有和运营的资产中访问这些受众。 |

## 用例 {#use-cases}

为了帮助您更好地了解如何以及何时使用此目标，以下是Adobe Experience Platform客户可以通过使用此功能解决的示例用例。

### 用例#1

运动服装品牌希望通过[!DNL Google Search]和[!DNL Google Shopping]联系现有客户，以根据优惠和项目的过去购买和浏览历史记录对其进行个性化设置。 服装品牌可以从自己的CRM中将电子邮件地址摄取到Experience Platform，并从自己的离线数据中构建受众。 然后，他们可以将这些受众发送到[!DNL Google Customer Match + Display & Video 360]目标，以在[!DNL Google Display & Video 360]属性（如[!DNL Search]、[!DNL YouTube]、[!DNL Gmail]和[!DNL Google Display Network]）中使用。

### 用例#2

一家知名科技公司发布了一款新手机。 为了推广这种新手机型号，他们正寻求让拥有旧款手机的客户了解手机的新特性和功能。

为了提升此版本，客户需要使用电子邮件地址作为标识符，将电子邮件地址从CRM数据库上传到Experience Platform。 受众是基于拥有旧版手机模型的客户创建的。 然后，受众会被发送到[!DNL Google Customer Match]，以便公司可以定位当前客户、拥有旧手机型号的客户以及具有[!DNL Google Display & Video 360]属性（如[!DNL Search]、[!DNL YouTube]、[!DNL Gmail]和[!DNL Google Display Network]）的类似客户。

## 支持的身份 {#supported-identities}

[!DNL Google Customer Match]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| phone_sha256_e.164 | E164格式的电话号码，使用SHA256算法进行哈希处理 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明进行操作，并分别使用适当的命名空间作为纯文本和经过哈希处理的电话号码。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明进行操作，并分别使用适当的命名空间作为纯文本和经过哈希处理的电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有[!DNL Google Customer Match]目标中使用的标识符（姓名、电话号码等）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## [!DNL Google Customer Match]帐户先决条件 {#google-account-prerequisites}

在Experience Platform中设置[!DNL Google Customer Match]目标之前，请确保已阅读并遵守Google关于使用[!DNL Customer Match]的策略，如[Google支持文档](https://support.google.com/google-ads/answer/6299717)中所述。

接下来，确保为您的[!DNL Google]帐户配置了[!DNL Standard]或更高权限级别。 有关详细信息，请参阅[Google广告文档](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1)。

### 帐户关联要求 {#linking}

在配置此目标连接器之前，必须将Google帐户ID关联到Adobe的Google帐户ID：`4641108541`。

如果您的Google帐户未正确关联到Adobe的帐户ID，则数据导出将失败。

>[!NOTE]
>
>对于参与此连接器的Beta测试计划的客户： Adobe已将Google合作伙伴帐户ID从`6219889373`更新为`4641108541`。
>
>**如果您是Google Customer Match + Display &amp; Video 360连接器测试版计划的成员，并且您的Google帐户当前已链接到旧的Adobe合作伙伴帐户ID (`6219889373`)，请执行以下步骤：**
>
>1. 取消您的Google帐户与旧Adobe合作伙伴帐户ID (`6219889373`)的链接
>2. 将您的Google帐户关联到新的Adobe合作伙伴帐户ID (`4641108541`)
>3. 从现有数据流中删除所有受众
>4. 创建新数据流并映射您的受众
>
>如果您的Google帐户已链接到新的Adobe合作伙伴帐户ID (`4641108541`)，则无需您执行任何操作即可使用此连接器。

**对于具有经理帐户的组织：**

如果贵组织使用[经理 [!DNL Google] 帐户](https://support.google.com/google-ads/answer/6139186)管理多个客户端帐户，请遵循以下特定关联要求：

* **要导出到特定的客户端帐户：**&#x200B;将该单个客户端帐户（而非经理帐户）关联到Adobe的Google帐户ID：`4641108541`
* 仅关联&#x200B;**Manager帐户是不够的**，将导致数据导出失败

### 允许列表 {#allowlist}

在Experience Platform中创建[!DNL Google Customer Match]目标之前，请确保您的[!DNL Google Ads]帐户符合[[!DNL Google Customer Match] 策略](https://support.google.com/google-ads/answer/6299717/customer-match-policy)。

拥有合规账户的客户由Google自动列入允许列表。

## ID匹配要求 {#id-matching-requirements}

[!DNL Google]要求不发送明确的个人身份信息(PII)。 因此，激活到[!DNL Google Customer Match]的受众必须脱离&#x200B;*散列的*&#x200B;标识符，例如散列电子邮件地址或电话号码。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵守其相应的要求。

### 电话号码散列要求 {#phone-number-hashing-requirements}

在[!DNL Google Customer Match]中激活电话号码的方法有两种：

* **摄取原始电话号码**：您可以将[!DNL E.164]格式的原始电话号码摄取到[!DNL Experience Platform]，激活时会自动对其进行哈希处理。 如果选择此选项，请确保始终将原始电话号码摄取到`Phone_E.164`命名空间。
* **正在引入经过哈希处理的电话号码**：您可以在引入到[!DNL Experience Platform]之前对电话号码进行预哈希处理。 如果选择此选项，请确保始终将经过哈希处理的电话号码摄取到`PHONE_SHA256_E.164`命名空间。

>[!NOTE]
>
>无法将摄取到`Phone`命名空间中的电话号码激活到[!DNL Google Customer Match + DV360]目标。

### 电子邮件哈希处理要求 {#hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或者在Experience Platform中明确使用电子邮件地址，并在激活时对其进行[!DNL Experience Platform]哈希处理。

有关Google的哈希要求和其他激活限制的详细信息，请参阅Google文档中的以下部分：

* [[!DNL Customer Match] 电子邮件地址、地址或用户ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 注意事项](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] 使用电话号码](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* 具有移动设备ID的[[!DNL Customer Match] ](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)

要了解如何在Experience Platform中摄取电子邮件地址，请参阅[批次摄取概述](../../../ingestion/batch-ingestion/overview.md)和[流式摄取概述](../../../ingestion/streaming-ingestion/overview.md)。

如果选择自己对电子邮件地址进行哈希处理，请确保符合Google的要求，如上面的链接中所述。

<!-- ### Using custom namespaces {#custom-namespaces}

Before you can use the `User_ID` namespace to send data to Google, make sure you synchronize your own identifiers using [!DNL gTag]. Refer to the [Google official documentation](https://support.google.com/google-ads/answer/9199250) for detailed information. -->

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## 连接到目标 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_gcm_dv360_accountID"
>title="链接 Google 和 Adobe 帐户"
>abstract="请确保您在此处输入的 Google 账户 ID 已与您的 Adobe 账户关联。如果您拥有一个包含多个客户账户的 Google 管理员账户，并希望将 Experience Platform 中的数据导出至某个特定的客户账户，则必须先将该客户账户与您的 Adobe 账户关联，并在此处输入对应的账户 ID。"

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL Name]**：为此目标连接提供一个名称
* **[!UICONTROL Description]**：为此目标连接提供描述
* **[!UICONTROL Account ID]**：您的[Google广告客户ID](https://support.google.com/google-ads/answer/1704344?hl=en)。 ID的格式为xxx-xxx-xxxx。 如果您使用的是[!DNL Google Ads Manager Account (My Client Center)]，请不要使用您的经理帐户ID。 请改用[Google广告客户ID](https://support.google.com/google-ads/answer/1704344?hl=en)。
* **[!UICONTROL Account type]**：您的Google帐户类型。 根据您在Google中的广告帐户类型，选择一个选项：
   * **[!UICONTROL Display Video Partner]**
   * **[!UICONTROL Display Video Advertiser]**

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要将&#x200B;*标识*&#x200B;导出到目标，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](../../assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

<!-- In the **[!UICONTROL Segment schedule]** step, you must provide the [!UICONTROL App ID] when sending [!DNL IDFA] or [!DNL GAID] audiences to [!DNL Google Customer Match].

![Google Customer Match App ID field highlighted in the Segment schedule step of the activation workflow.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

For details on how to find the [!DNL App ID], refer to the [Google official documentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) or ask your Google representative. -->

### 映射示例：在[!DNL Google Customer Match + Display & Video 360]中激活受众数据 {#example-gcm}

这是在[!DNL Google Customer Match + Display & Video 360]中激活受众数据时正确标识映射的示例。

选择源字段：

* 如果您使用的电子邮件地址未经过哈希处理，请选择`Email`命名空间作为源标识。
* 如果您根据`Email_LC_SHA256` [!DNL Experience Platform]电子邮件哈希处理要求[!DNL Google Customer Match]将数据摄取到[时已将客户电子邮件地址哈希处理，请选择](#hashing-requirements)命名空间作为源标识。
* 如果您的数据由非散列电话号码组成，请选择`PHONE_E.164`命名空间作为源标识。 [!DNL Experience Platform]将散列电话号码以符合[!DNL Google Customer Match]要求。
* 如果您根据`Phone_SHA256_E.164` [!DNL Experience Platform]电话号码散列要求[!DNL Facebook]将数据提取到[中时散列电话号码，请选择](#phone-number-hashing-requirements)命名空间作为源标识。

选择目标字段：

* 当源命名空间为`Email_LC_SHA256`或`Email`时，选择`Email_LC_SHA256`命名空间作为目标标识。
* 当源命名空间为`Phone_SHA256_E.164`或`PHONE_E.164`时，选择`Phone_SHA256_E.164`命名空间作为目标标识。

![在激活工作流的“映射”步骤中显示的源字段和目标字段之间的标识映射。](../../assets/catalog/advertising/google-customer-match-dv360/identity-mapping-gcm-dv360.png)

来自未经过哈希处理的命名空间的数据在激活时会由[!DNL Experience Platform]自动进行哈希处理。

属性源数据不会自动进行哈希处理。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。

![应用激活工作流的映射步骤中突出显示的转换控件。](../../assets/catalog/advertising/google-customer-match-dv360/transformation.png)

## 监视目标 {#monitor-destination}

连接到目标并建立目标数据流后，您可以使用Real-Time CDP中的[监视功能](/help/dataflows/ui/monitor-destinations.md)获取有关在每次数据流运行中激活到目标的配置文件记录的更多信息。

[!DNL Google Customer Match + Display & Video 360]连接的监视信息包括与每个数据流和数据流运行中激活、排除和失败的身份相关的受众级别信息。 [参阅更多](/help/dataflows/ui/monitor-destinations.md#segment-level-view)关于该功能的信息。

## 验证受众激活是否成功 {#verify-activation}

完成激活流程后，切换到您的&#x200B;**[!UICONTROL Google Ads]**&#x200B;帐户。 激活的受众在您的Google帐户中显示为客户列表。 根据您的受众规模，除非有1000多个活动用户可提供服务，否则不会填充某些受众。 在[Google Audience Partner文档](https://developers.google.com/audience-partner/api/docs/customer-match/get-started#verify-list)中查找更多信息。 请注意，您需要向Google请求获取对链接中文档的访问权限。

## 数据治理

Experience Platform中的某些目标对于发送到目标平台或从目标平台接收的数据具有某些规则和义务。 您有责任了解数据的限制和义务，以及如何在Adobe Experience Platform和目标平台中使用该数据。 Adobe Experience Platform提供数据治理工具，帮助您管理其中一些数据使用义务。 [了解有关Data Governance工具和策略的更多信息](../../../data-governance/labels/overview.md)。

## 疑难解答 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

当客户帐户不符合[先决条件](#google-account-prerequisites)时，会发生此错误。 要解决此问题，请联系Google并确保您的帐户已列入允许列表并配置为[!DNL Standard]或更高权限级别。 有关详细信息，请参阅[Google广告文档](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1)。
