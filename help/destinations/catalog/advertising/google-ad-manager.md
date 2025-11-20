---
keywords: google广告管理器；google广告；doubleclick；DoubleClick AdX；DoubleClick；Google广告管理器；Google广告管理器；DFP
title: Google Ad Manager连接
description: Google Ad Manager（以前称为DoubleClick for Publishers或DoubleClick AdX）是Google的一个广告投放平台，它使发布者能够通过视频和移动应用程序管理其网站上的广告显示。
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 7%

---

# [!DNL Google Ad Manager]连接

>[!IMPORTANT]
>
> Google将发布对[Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)和[Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)的更改，以支持欧盟（[EU用户同意政策](https://digital-markets-act.ec.europa.eu/index_en)）中[Digital Markets Act](https://www.google.com/about/company/user-consent-policy/) (DMA)定义的合规性和同意相关要求。 自2024年3月6日起，将开始实施对同意要求的这些更改。
><br/>
>为遵守欧盟用户同意政策并继续为欧洲经济区(EEA)用户创建受众列表，广告商和合作伙伴必须确保在上传受众数据时获得最终用户同意。 作为 Google 合作伙伴，Adobe 为您提供必要的工具，以遵守欧盟 DMA 下的这些同意要求。
><br/>
>如果客户购买了Adobe Privacy &amp; Security Shield并配置了[同意策略](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)以过滤掉未经同意的用户档案，则无需采取任何操作。
><br/>
>未购买Adobe Privacy &amp; Security Shield的客户必须使用[区段生成器](../../../segmentation/home.md#segment-definitions)中的[区段定义](../../../segmentation/ui/segment-builder.md)功能来过滤掉未经同意的用户档案，以便继续使用现有的Real-Time CDP Google目标而不中断。


[!DNL Google Ad Manager] (以前称为[!DNL DoubleClick for Publishers] (DFP)或[!DNL DoubleClick AdX])是来自[!DNL Google]的广告投放平台，它使发布者能够通过视频和移动应用程序管理在其网站上显示的广告。

## 目标详情 {#specifics}

请注意以下特定于[!DNL Google Ad Manager]目标的详细信息：

* 在[!DNL Google]平台中以编程方式创建激活的受众。
* [!DNL Experience Platform]当前不包括用于验证激活是否成功的度量指标。 请参阅Google中的受众计数，以验证集成并了解受众定位大小。
* 将受众映射到[!DNL Google Ad Manager]目标后，受众名称会立即出现在[!DNL Google Ad Manager]用户界面中。
* 区段填充需要24-48小时才能显示在[!DNL Google Ad Manager]中。 此外，受众必须具有至少50个配置文件才能在[!DNL Google Ad Manager]中显示。 不会在[!DNL Google Ad Manager]中填充配置文件小于50的受众。

## 支持的身份 {#supported-identities}

[!DNL Google Ad Manager]支持根据下表所示的标识激活受众。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 身份标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hans)，也称为[!DNL Device ID]。 38位数字设备ID，Audience Manager与与其交互的每个设备相关联。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hans)来定位加利福尼亚州的用户，并使用Google Cookie ID来定位所有其他用户。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google]使用此ID定位加州以外的用户。 |
| RIDA | Advertising的Roku ID。 此ID唯一标识Roku设备。 |  |
| 女佣 | Microsoft Advertising ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID唯一标识Amazon Fire电视。 |  |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform[分段服务](../../../segmentation/home.md)生成的访问群体。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您要将受众的所有成员导出到Google目标。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

如果您希望使用[!DNL Google Ad Manager]创建您的第一个目标，并且以前未在Experience Cloud ID服务(使用Audience Manager或其他应用程序)中启用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=zh-Hans)，请联系Adobe Consulting或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了[!DNL Google]集成，则您设置的ID同步将会转移到Experience Platform。

### 允许列表 {#allow-listing}

在Experience Platform中设置您的第一个[!DNL Google Ad Manager]目标之前，必须将该目标列入允许列表。 在创建目标之前，请确保完成如下所述的允许列表流程。

1. 按照[Google Ad Manager文档](https://support.google.com/admanager/answer/3289669?hl=en)中描述的步骤，将Adobe添加为链接的数据管理平台(DMP)。
2. 在[!DNL Google Ad Manager]界面中，转到&#x200B;**[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]**&#x200B;并启用&#x200B;**[!UICONTROL API Access]**&#x200B;滑块。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="将受众 ID 附加到受众名称"
>abstract="选择此选项可让 Google Ad Manager 中的受众名称包含来自 Experience Platform 的受众 ID，如下所示：`Audience Name (Audience ID)`"

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL Name]**：填写此目标的首选名称。
* **[!UICONTROL Description]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL Account ID]**：输入您的[!DNL Audience Link ID]帐户中的[!DNL Google]。 这是与您的[!DNL Google Ad Manager]网络（而不是[!DNL Network code]）关联的特定标识符。 您可以在&#x200B;**[!UICONTROL Admin > Global settings]**&#x200B;界面的[!DNL Google Ad Manager]下找到此内容。
* **[!UICONTROL Account Type]**：根据您在Google中的帐户，选择一个选项：
   * 将`DFP by Google`用于[!DNL DoubleClick]发布者
   * 将`AdX buyer`用于[!DNL Google AdX]
* **[!UICONTROL Append audience ID to audience name]**：选择此选项以使Google广告管理器中的受众名称包含Experience Platform中的受众ID，如下所示： `Audience Name (Audience ID)`。

>[!NOTE]
>
>在设置[!DNL Google Ad Manager]目标时，请与您的[!DNL Google Account Manager]或Adobe代表合作，以了解您的帐户类型。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到[!DNL Google Ad Manager]目标，请检查您的[!DNL Google Ad Manager]帐户。 如果激活成功，则会在您的帐户中填充受众。

## 故障排除 {#troubleshooting}

如果您在使用此目标时遇到任何错误，并且需要访问Adobe或Google，请保留以下ID。

这些是Adobe的Google帐户ID：

* **[!UICONTROL Account ID]**： 87933855
* **[!UICONTROL Customer ID]**： 89690775