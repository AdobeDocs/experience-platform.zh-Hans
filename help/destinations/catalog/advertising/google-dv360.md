---
title: Google显示和视频360连接
description: Display & Video 360（以前称为DoubleClick Bid Manager）是一种工具，用于在显示器、视频和移动设备库存源中执行重定位和面向受众的数字活动。
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 4%

---

# [!DNL Google Display & Video 360]连接

>[!IMPORTANT]
>
> Google将发布对[Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)和[Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)的更改，以支持欧盟（[EU用户同意政策](https://digital-markets-act.ec.europa.eu/index_en)）中[Digital Markets Act](https://www.google.com/about/company/user-consent-policy/) (DMA)定义的合规性和同意相关要求。 自2024年3月6日起，将开始实施对同意要求的这些更改。
> &#x200B;><br/>
> &#x200B;>为了遵循欧盟用户同意政策并继续为欧洲经济区(EEA)中的用户创建受众列表，广告商和合作伙伴必须确保他们在上传受众数据时获得最终用户同意。 作为 Google 合作伙伴，Adobe 为您提供必要的工具，以遵守欧盟 DMA 下的这些同意要求。
> &#x200B;><br/>
> &#x200B;>如果客户购买了Adobe Privacy &amp; Security Shield并配置了[同意策略](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)以过滤掉未经同意的用户档案，则无需采取任何操作。
> &#x200B;><br/>
> &#x200B;>未购买Adobe Privacy &amp; Security Shield的客户必须使用[区段生成器](../../../segmentation/home.md#segment-definitions)中的[区段定义](../../../segmentation/ui/segment-builder.md)功能来过滤掉未经同意的用户档案，以便继续使用现有的Real-Time CDP Google目标而不中断。

[!DNL Display & Video 360]（以前称为[!DNL DoubleClick Bid Manager]）是一种工具，用于在显示、视频和移动设备清单源中执行重定位和面向受众的数字营销活动。

## 目标详情 {#specifics}

请注意以下特定于[!DNL Google Display & Video 360]目标的详细信息：

* 激活的受众是在Google平台中以编程方式创建的。
* 将受众回填激活到[!DNL Google Display & Video 360]目标的工作安排在受众首次映射到目标连接后的24-48小时内进行。 此更新是为了响应Google的策略，该策略等待24小时直到摄取数据，旨在提高Real-Time CDP和[!DNL Google Display & Video 360]之间的匹配率。 这是仅适用于此目标的后端配置，与UI中任何客户可配置的计划选项无关。

>[!IMPORTANT]
>
>如果您希望使用Google Display &amp; Video 360创建您的第一个目标，并且以前未在Experience Cloud ID服务(使用Adobe Audience Manager或其他应用程序)中启用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe Consulting或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了Google集成，则您设置的ID同步功能将会转移到Experience Platform。

## 支持的身份 {#supported-identities}

[!DNL Google Display & Video 360]支持根据下表所示的标识激活受众。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 身份标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为[!DNL Device ID]。 Audience Manager与其交互的每个设备相关联的38位数字设备ID。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)来定位加利福尼亚州的用户，并使用Google Cookie ID来定位所有其他用户。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google]使用此ID定位加州以外的用户。 |
| RIDA | Advertising的Roku ID。 此ID唯一标识Roku设备。 |  |
| 女佣 | Microsoft Advertising ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID唯一标识Amazon Fire电视。 |  |

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您要将受众的所有成员导出到Google目标。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

## 先决条件 {#prerequisites}

### 允许列表 {#allow-listing}

>[!NOTE]
>
>在Experience Platform中设置您的第一个[!DNL Google Display & Video 360]目标之前，必须将该目标列入允许列表。 在创建目标之前，请确保[!DNL Google]已完成下面描述的允许列表流程。
>&#x200B;>此规则的例外情况适用于[Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html)客户。 如果您已在Audience Manager中创建了到此Google目标的连接，则无需再次完成允许列表流程，您可以继续后续步骤。

在Experience Platform中创建[!DNL Google Display & Video 360]目标之前，您必须联系Google以请求将Adobe列入允许列表添加到允许的数据提供商列表中，并将您的帐户添加到中。 请联系Google并提供以下信息：

* **帐户ID**： Adobe与Google的帐户ID。 帐户ID：87933855。
* **客户ID**： Adobe的客户帐户ID与Google。 客户ID：89690775。
* **您的帐户类型**：使用&#x200B;**[!DNL Invite advertiser]**&#x200B;允许仅将受众共享给您的Display &amp; Video 360帐户中的特定品牌，或使用&#x200B;**[!DNL Invite partner]**&#x200B;允许将受众共享给您的Display &amp; Video 360帐户中的所有品牌。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL Name]**：填写此目标的首选名称。
* **[!UICONTROL Description]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL Account Type]**：根据您在Google中的帐户，选择一个选项：
   * 使用`Invite Advertiser`以允许仅将受众共享到您的Display &amp; Video 360帐户中的特定品牌。
   * 使用`Invite Partner`允许将受众共享给您的Display &amp; Video 360帐户中的所有品牌。
* **[!UICONTROL Account ID]**：使用Google填写您的&#x200B;**[!DNL Invite partner]**&#x200B;或&#x200B;**[!DNL Invite advertiser]**&#x200B;帐户ID。 通常，这是一个六到七位数的ID。

>[!NOTE]
>
>在设置[!DNL Google Display & Video 360]目标时，请与您的[!DNL Google Account Manager]或Adobe代表合作，以了解您的帐户类型。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到[!DNL Google Display & Video 360]目标，请检查您的[!DNL Google Display & Video 360]帐户。 如果激活成功，则会在您的帐户中填充受众。

## 故障排除 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

当客户帐户不符合[先决条件](#prerequisites)时，会发生此错误。 要解决此问题，请联系Google并确保您的帐户已列入允许列表。