---
title: (Beta) [!DNL Google Ad Manager 360] 连接
description: Google Ad Manager 360是Google的一个广告投放平台，它使发布者能够通过视频和移动应用程序管理其网站上的广告显示。
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 4%

---

# (Beta) [!DNL Google Ad Manager 360]连接

>[!IMPORTANT]
>
> Google将发布对[Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)和[Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)的更改，以支持欧盟（[EU用户同意政策](https://www.google.com/about/company/user-consent-policy/)）中[Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA)定义的合规性和同意相关要求。 自2024年3月6日起，将开始实施对同意要求的这些更改。
><br/>
>为了遵循欧盟用户同意政策并继续为欧洲经济区(EEA)中的用户创建受众列表，广告商和合作伙伴必须确保他们在上传受众数据时获得最终用户同意。 作为Google合作伙伴，Adobe会为您提供在欧洲的DMA中遵守这些同意要求的必要工具。
><br/>
>购买AdobePrivacy &amp; Security Shield并配置了[同意策略](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)以过滤掉未同意的配置文件的客户无需采取任何操作。
><br/>
>未购买AdobePrivacy &amp; Security Shield的客户必须使用[区段生成器](../../../segmentation/ui/segment-builder.md)中的[区段定义](../../../segmentation/home.md#segment-definitions)功能来过滤掉未经同意的用户档案，以便继续不间断地使用现有的Real-Time CDP Google目标。

[!DNL Google Ad Manager 360]连接允许通过[!DNL Google Cloud Storage]将[!DNL publisher provided identifiers] (PPID)的批次上载到[!DNL Google Ad Manager 360]。

有关发布者提供的标识符如何在Google Ad Manager 360中工作的详细信息，请参阅[Google官方文档](https://support.google.com/admanager/answer/2880055?hl=en)。

>[!IMPORTANT]
>
>此目标当前位于Beta中，并且仅对有限数量的客户可用。 要请求访问[!DNL Google Ad Manager 360]连接，请联系您的Adobe代表并提供您的[!DNL organization ID]。

[!DNL Google Ad Manager 360]目标将[!DNL CSV]文件导出到您的[!DNL Google Cloud Storage]存储段。 导出[!DNL CSV]文件后，必须将其导入您的[!DNL Google Ad Manager 360]帐户。

## 目标详情 {#specifics}

请注意以下特定于[!DNL Google Ad Manager 360]目标的详细信息。

* 激活的受众是在Google平台中以编程方式创建的，并在CSV文件中填充。

## 支持的身份 {#supported-identities}

[!DNL This integration]支持激活下表中描述的标识。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | 选择此目标身份以将受众发送到[!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform[分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ {\f13 } | 受众[已将](../../../segmentation/ui/audience-portal.md#import-audience)从CSV文件导入到Experience Platform中。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及适用的架构字段（例如，PPID），如[目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

### 允许列表 {#allow-listing}

在Platform中设置您的第一个[!DNL Google Ad Manager 360]目标之前，必须首先列入允许列表。 在创建目标之前，请确保完成如下所述的允许列表流程。

>[!NOTE]
>
>此规则的例外适用于现有[Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html)客户。 如果您已在Audience Manager中创建了到此Google目标的连接，则无需再次完成允许列表流程，您可以继续后续步骤。

1. 按照[Google Ad Manager文档](https://support.google.com/admanager/answer/3289669?hl=en)中描述的步骤将Adobe添加为链接的数据管理平台(DMP)。
2. 在[!DNL Google Ad Manager]界面中，转到&#x200B;**[!UICONTROL 管理员]** > **[!UICONTROL 全局设置]** > **[!UICONTROL 网络设置]**，并启用&#x200B;**[!UICONTROL API访问]**&#x200B;滑块。


## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)中描述的步骤操作。 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证到目标，请填写必填字段并选择&#x200B;**[!UICONTROL 连接到目标]**。

* **[!UICONTROL 访问密钥ID]**：一个61字符的字母数字字符串，用于向Platform验证您的[!DNL Google Cloud Storage]帐户。
* **[!UICONTROL 访问密钥]**：用于向Platform验证您的[!DNL Google Cloud Storage]帐户的40字符base64编码字符串。

有关这些值的更多信息，请参阅[Google Cloud Storage HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 有关如何生成自己的访问密钥ID和访问密钥的步骤，请参阅[[!DNL Google Cloud Storage] 源概述](/help/sources/connectors/cloud-storage/google-cloud-storage.md)。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="将受众 ID 附加到受众名称"
>abstract="选择此选项可让这一目标中的受众名称包含来自 Experience Platform 的受众 ID，如下所示：`Audience Name (Audience ID)`"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 文件夹路径]**：输入将承载导出文件的目标文件夹的路径。
* **[!UICONTROL Bucket名称]**：输入要由此目标使用的[!DNL Google Cloud Storage]存储段的名称。
* **[!UICONTROL 帐户ID]**：输入您的[!DNL Google]帐户中的[!DNL Audience Link ID]。 这是与您的[!DNL Google Ad Manager]网络（而不是[!DNL Network code]）关联的特定标识符。 您可以在[!DNL Google Ad Manager]界面的&#x200B;**[!UICONTROL 管理员>全局设置]**&#x200B;下找到此项。
* **[!UICONTROL 帐户类型]**：根据您的[!DNL Google]帐户选择一个选项：
   * 将`AdX buyer`用于[!DNL Google AdX]
   * 将`DFP by Google`用于[!DNL DoubleClick]发布者
* **[!UICONTROL 将受众ID附加到受众名称]**：选择此选项可使Google Ad Manager 360中的受众名称包含来自Experience Platform的受众ID，如下所示： `Audience Name (Audience ID)`。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。

在身份映射步骤中，您可以看到以下预填充的映射：

| 预填充映射 | 描述 |
|---------|----------|
| `ECID` -> `ppid` | 这是唯一一个用户可编辑的预填充映射。 您可以从Platform中选择任何属性或身份命名空间并将它们映射到`ppid`。 |
| `metadata.segment.alias` -> `list_id` | 将Experience Platform受众名称映射到Google平台中的受众ID。 |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | 告知Google平台何时从区段中删除不符合条件的用户。 |

这些映射是[!DNL Google Ad Manager 360]所需，由Adobe Experience Platform为所有[!DNL Google Ad Manager 360]连接自动创建。

![显示Google Ad Manager 360映射步骤的UI图像。](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## 导出的数据 {#exported-data}

要验证数据是否已成功导出，请检查您的[!DNL Google Cloud Storage]存储段并确保导出的文件包含预期的配置文件人口。

## 故障排除 {#troubleshooting}

如果您在使用此目标时遇到任何错误，并且需要联系Adobe或Google，请随时保留以下ID。

这些是Adobe的Google帐户ID：

* **[!UICONTROL 帐户ID]**： 87933855
* **[!UICONTROL 客户ID]**： 89690775