---
keywords: google广告管理器；google广告；doubleclick；DoubleClick AdX；DoubleClick；Google广告管理器；Google广告管理器；DFP
title: Google Ad Manager连接
description: Google Ad Manager（以前称为DoubleClick for Publishers或DoubleClick AdX）是Google的一个广告投放平台，它使发布者能够通过视频和移动应用程序管理其网站上的广告显示。
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 4%

---

# [!DNL Google Ad Manager] 连接

>[!IMPORTANT]
>
> Google将发布对 [Google Ads API](https://developers.google.com/google-ads/api/docs/start)， [客户匹配](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)，和 [显示和视频360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) ，以支持 [数字市场法案](https://digital-markets-act.ec.europa.eu/index_en) (DMA)在欧盟([欧盟用户同意政策](https://www.google.com/about/company/user-consent-policy/))。 自2024年3月6日起，将开始实施对同意要求的这些更改。
><br/>
>为了遵循欧盟用户同意政策并继续为欧洲经济区(EEA)中的用户创建受众列表，广告商和合作伙伴必须确保他们在上传受众数据时获得最终用户同意。 作为Google合作伙伴，Adobe会为您提供在欧洲的DMA中遵守这些同意要求的必要工具。
><br/>
>已购买AdobePrivacy &amp; Security Shield并配置了 [同意政策](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 无需执行任何操作，即可过滤掉未经同意的用户档案。
><br/>
>未购买AdobePrivacy &amp; Security Shield的客户必须使用 [区段定义](../../../segmentation/home.md#segment-definitions) 中的功能 [区段生成器](../../../segmentation/ui/segment-builder.md) 筛选未经同意的用户档案，以便能够继续使用现有的Real-Time CDP Google目标，而不会出现中断。


[!DNL Google Ad Manager]，以前称为 [!DNL DoubleClick for Publishers] (DFP)或 [!DNL DoubleClick AdX]是一个广告服务平台，来自 [!DNL Google] 这给了出版商管理其网站上通过视频和移动应用程序展示广告的方式。

## 目标详情 {#specifics}

请注意以下特定于的详细信息 [!DNL Google Ad Manager] 目标：

* 激活的受众以编程方式创建于 [!DNL Google] 平台。
* [!DNL Platform] 当前不包括用于验证激活是否成功的测量指标。 请参阅Google中的受众计数，以验证集成并了解受众定位大小。
* 将受众映射到后 [!DNL Google Ad Manager] 目标，受众名称会立即显示在 [!DNL Google Ad Manager] 用户界面。
* 区段人口需要24-48小时才能显示在 [!DNL Google Ad Manager]. 此外，受众必须具有至少50个配置文件才能在中显示 [!DNL Google Ad Manager]. 大小小于50个配置文件的受众将不会填充到 [!DNL Google Ad Manager].

## 支持的身份 {#supported-identities}

[!DNL Google Ad Manager] 支持根据下表所示的标识激活受众。 了解有关 [身份](/help/identity-service/features/namespaces.md).

| 标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为 [!DNL Device ID]. 38位数的设备ID，Audience Manager与每台与其交互的设备相关联。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) 定位加利福尼亚的用户，以及所有其他用户的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 使用此ID定位加利福尼亚州以外的用户。 |
| RIDA | Advertising的Roku ID。 此ID唯一标识Roku设备。 |  |
| 女佣 | Microsoft Advertising ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID唯一标识Amazon Fire电视。 |  |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ {\f13 } | 受众 [已导入](../../../segmentation/ui/audience-portal.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您要将受众的所有成员导出到Google目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

如果您希望使用创建您的第一个目标 [!DNL Google Ad Manager] 并且尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 以往(使用Audience Manager或其他应用程序)在Experience CloudID服务中，请联系Adobe Consulting或客户关怀团队以启用ID同步。 如果您之前已设置 [!DNL Google] Audience Manager中的集成，即您设置的ID同步功能会转移到Platform。

### 允许列表 {#allow-listing}

必须先将添加到允许列表，然后才能设置您的第一个 [!DNL Google Ad Manager] Platform的目标。 在创建目标之前，请确保完成如下所述的允许列表流程。

1. 请按照 [Google Ad Manager文档](https://support.google.com/admanager/answer/3289669?hl=en) 将Adobe添加为链接的数据管理平台(DMP)。
2. 在 [!DNL Google Ad Manager] 界面，转到 **[!UICONTROL 管理员]** > **[!UICONTROL 全局设置]** > **[!UICONTROL 网络设置]**，并启用 **[!UICONTROL API访问]** 滑块。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="将受众 ID 附加到受众名称"
>abstract="选择此选项可让 Google Ad Manager 中的受众名称包含来自 Experience Platform 的受众 ID，如下所示：`Audience Name (Audience ID)`"

同时 [设置](../../ui/connect-destination.md) 此目标必须提供以下信息：

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 帐户ID]**：输入您的 [!DNL Audience Link ID] 来自您的 [!DNL Google] 帐户。 这是与您的关联的特定标识符 [!DNL Google Ad Manager] 网络(不是您的 [!DNL Network code])。 您可以在以下位置找到它 **[!UICONTROL 管理员>全局设置]** 在 [!DNL Google Ad Manager] 界面。
* **[!UICONTROL 帐户类型]**：根据您在Google中的帐户，选择一个选项：
   * 使用 `DFP by Google` 对象 [!DNL DoubleClick] 适用于发布者的
   * 使用 `AdX buyer` 对象 [!DNL Google AdX]
* **[!UICONTROL 将受众ID附加到受众名称]**：选择此选项可使Google Ad Manager中的受众名称包含Experience Platform中的受众ID，如下所示： `Audience Name (Audience ID)`.

>[!NOTE]
>
>设置时 [!DNL Google Ad Manager] 目标，请与您的 [!DNL Google Account Manager] 或Adobe代表以了解您的客户类型。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

请参阅 [将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

## 导出的数据 {#exported-data}

验证数据是否已成功导出到 [!DNL Google Ad Manager] 目标，检查您的 [!DNL Google Ad Manager] 帐户。 如果激活成功，则会在您的帐户中填充受众。

## 故障排除 {#troubleshooting}

如果您在使用此目标时遇到任何错误，并且需要联系Adobe或Google，请随时保留以下ID。

这些是Adobe的Google帐户ID：

* **[!UICONTROL 帐户ID]**：87933855
* **[!UICONTROL 客户ID]**：89690775