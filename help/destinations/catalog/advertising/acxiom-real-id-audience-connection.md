---
title: Acxiom Real ID&trade；受众连接
description: 使用 [!DNL Acxiom Real ID&trade; Audience Connection] 目标增强和激活跨平台（如 [!DNL Altice]、 [!DNL Ampersand]和 [!DNL Comcast]）的受众。
source-git-commit: 3aefb36bbf525a5eebe3a9330e25587501167a64
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 4%

---


# [!DNL Acxiom Real ID™ Audience Connection] 目标

使用[!DNL Acxiom Real ID Audience Connection]目标通过[!DNL Acxiom]的[Real ID™](https://www.acxiom.com/real-id/real-id/)技术增强受众。 然后跨平台（如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等）激活这些受众。

>[!NOTE]
>
>此目标连接器和文档页面由[!DNL Acxiom]团队创建和维护。 如有任何查询或更新请求，请直接通过[acxiom-adobe-help@acxiom.com](mailto:acxiom-adobe-help@acxiom.com)联系[!DNL Acxiom]。

按照以下步骤使用[!DNL Adobe Experience Platform]用户界面创建[!DNL Acxiom Real ID Audience Connection]目标连接器。 使用此连接器可构建受众并将受众分发到选定的目标。

## 用例 {#use-cases}

如果将[!DNL Acxiom]的[!DNL Real ID]作为标识符加载到[!DNL Real-Time CDP]中，请使用此目标。 以下用例显示如何使用[!DNL Acxiom Real ID Audience Connection]目标。

### 将受众从[!DNL Experience Platform]发送到您的[!DNL Acxiom]帐户 {#send-audiences}

使用此目标连接器将受众从[!DNL Experience Platform]发送到您的[!DNL Acxiom]帐户以进行跨渠道客户获取。

例如，一家全球金融服务品牌的营销运营部对通过多个广告平台进行跨渠道客户获取感兴趣。 他们可以使用[!DNL Acxiom Real ID Audience Connection]目标连接器将受众从[!DNL Experience Platform]发送到[!DNL Acxiom]，通过[!DNL Acxiom]的[!DNL Real ID]技术增强受众，并将受众激活到多个平台，如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。

## 先决条件 {#prerequisites}

在配置[!DNL Acxiom Real ID Audience Connection]目标之前，请完成以下先决条件。

* **确认使用条款：**&#x200B;阅读并签署[!DNL Acxiom]的使用条款协议。 在您执行的销售订单完成后，您将收到指向协议的链接。 在您签署协议之前，[!DNL Acxiom Real ID Audience Connection]目标卡不会出现在[!DNL Experience Platform]目标目录中。 在您接受并签署协议后，[!DNL Adobe]将完成您的设置并显示[!DNL Acxiom Real ID Audience Connection]目标卡。
* **知道您的[!DNL Adobe]组织ID：**&#x200B;需要您的[!DNL Adobe]组织ID才能完成您的使用条款协议。 有关如何[查看组织ID](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)的详细信息，请参阅[!DNL Adobe]的Experience Cloud中的&#x200B;*组织*&#x200B;主题。
* **获取[!DNL Acxiom]的[!DNL Real ID]产品的许可证：**&#x200B;获取许可证后，在[!DNL Real-Time CDP]内使[!DNL Acxiom]的[!DNL Real ID]可用。 有关详细信息，请参阅[Acxiom数据增强](/help/destinations/catalog/data-partner/acxiom-data-enhancement.md)。

## 支持的身份 {#supported-identities}

[!DNL Acxiom]的[!DNL Real ID]受众连接目标支持以下标识激活。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
| --------------- | ----------- | -------------- |
| [!DNL Real ID] | [!DNL Real ID] | 将源字段映射到此目标标识。 您的源字段可以是[!DNL Acxiom] [!DNL Real ID]或自定义标识符。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
| --------------- | --------- | ----------- |
| [!DNL Segmentation Service] | 是 | 通过[!DNL Experience Platform] [分段服务](/help/segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 是 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li>自定义上传受众[从CSV文件导入[!DNL Experience Platform]，](/help/segmentation/ui/audience-portal.md#import-audience)</li><li>相似的受众，</li><li>联合受众，</li><li>在其他[!DNL Experience Platform]应用（如[!DNL Adobe Journey Optimizer]）中生成的受众，</li><li>等等。</li></ul> |

{style="table-layout:auto"}

### 按数据类型显示的受众支持 {#supported-audiences-data-type}

下表描述了您可以导出到此目标的受众数据类型。

| 受众数据类型 | 受支持 | 描述 | 用例 |
| -------------------- | --------- | ----------- | --------- |
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 基于客户配置文件。 使用它们定位营销活动的特定人员组。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

下表描述了目标导出类型和频率。

| 项目 | 类型 | 注释 |
| ---- | ---- | ----- |
| 导出类型 | **[!UICONTROL Audience export]** | 使用[!DNL Acxiom Real ID Audience Connection]目标中使用的标识符导出受众的所有成员。 |
| 导出频率 | **[!UICONTROL Batch]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 支持的目标 {#supported-destinations}

通过[!DNL Acxiom Real ID Audience Connection]目标将受众激活到以下平台。

* [!DNL Altice]
* [[!DNL Amazon]](#amazon)
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL Facebook]](#facebook)
* [[!DNL LG Ads]](#lg-ads)
* [[!DNL Pinterest]](#pinterest)
* [!DNL Spectrum]
* [!DNL Viant]
* [[!DNL Vizio]](#vizio)

## 连接到目标 {#connect}

[!DNL Experience Platform]自动为您的[!DNL Acxiom Real ID Audience Connection]目标处理身份验证。

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

## 目标特定的设置 {#destination-settings}

某些[!DNL Acxiom Real ID Audience Connection]目标需要其他信息。 以下部分提供了有关如何配置这些选项的详细指导。

### [!DNL Amazon] {#amazon}

要配置目标的详细信息，请完成以下字段。

* **[!UICONTROL Publisher Account ID]**：输入与此目标关联的发布者帐户ID。

  ![显示“发布者帐户ID”字段的[!DNL Amazon]目标详细信息面板屏幕截图。](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_amazon_destination_details.png){zoomable="yes"}

### [!DNL Facebook] {#facebook}

要配置目标的详细信息，请完成以下字段。

* **[!UICONTROL Destination Account ID]**：输入此目标的目标帐户ID。

  ![显示“目标帐户ID”字段的[!DNL Facebook]目标详细信息面板屏幕截图。](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_facebook_destination_details.png){zoomable="yes"}

### [!DNL LG Ads] {#lg-ads}

要配置目标的详细信息，请完成以下字段。

* **[!UICONTROL Segment Category]**：您的区段所属的目标类别或垂直类别。 例如：金融服务、汽车或健康。

  ![显示“区段类别”字段的[!DNL LG Ads]目标详细信息面板屏幕截图。](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png){zoomable="yes"}

### [!DNL Pinterest] {#pinterest}

要配置目标的详细信息，请完成以下字段。

* **[!UICONTROL Destination Account ID]**：输入此目标的目标帐户ID。

  ![显示“目标帐户ID”字段的[!DNL Pinterest]目标详细信息面板屏幕截图。](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_pinterest_destination_details.png){zoomable="yes"}

### [!DNL Vizio] {#vizio}

要配置目标的详细信息，请完成以下字段。

* **[!UICONTROL Advertiser Name]**：输入此目标的广告商名称。

  ![显示“广告商名称”字段的[!DNL Vizio]目标详细信息面板的屏幕截图。](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_vizio_destination_details.png){zoomable="yes"}

## 激活此目标的受众 {#activate}

有关将受众激活到此目标的说明，请阅读[将受众数据激活到批处理配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png){width="100" zoomable="yes"}

>[!NOTE]
>
>[!DNL Acxiom Real ID Audience Connection]目标仅支持完整文件导出。

### 映射属性和身份 {#map}

要使[!DNL Acxiom Real ID Audience Connection]目标正确接收受众数据，请将源字段从[!DNL Experience Platform]映射到正确的[!DNL Acxiom Real ID Audience Connection]目标字段。

在映射步骤中自动预填充&#x200B;**[!UICONTROL Real ID]**&#x200B;目标字段。 将您的源字段映射到它：自定义标识符命名空间或配置文件架构中存储的实际[!DNL Acxiom] [!DNL Real ID]。

| 字段名称 | 描述 | 必需 |
| ---------- | ----------- | -------- |
| [!DNL Real ID] | [!DNL Real ID]是[!DNL Acxiom]专有身份解析图中的36字节的唯一字母数字标识符。 它是一个标识符，表示个人、家庭或地址。 | 是 |

{style="table-layout:auto"}

在&#x200B;**[!UICONTROL Source Field]**&#x200B;列中，输入要映射到&#x200B;**[!UICONTROL Real ID]**&#x200B;目标字段的源属性的名称。 或者选择&#x200B;**[!UICONTROL Select source field]**&#x200B;浏览可用的源字段。 然后选择&#x200B;**[!UICONTROL Next]**。

![显示[!UICONTROL Source Field]列和[!UICONTROL Select source field]面板的映射屏幕截图。](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png){zoomable="yes"}

如果您没有使用[!DNL Adobe]的标准架构，请参阅[查询服务UI指南](/help/query-service/ui/overview.md)以使用您的字段名填充[!DNL Adobe]标准架构。

### 查看您的目标 {#review}

完成所有步骤后，请先查看目标连接状态和受众详细信息，然后再激活目标连接。 您选择的受众会显示在列表中。 每个受众都是对[!DNL Acxiom Real ID Audience Connection] API的单独调用。

当结果正确时，选择&#x200B;**[!UICONTROL Finish]**&#x200B;以激活您的目标。

![在激活前显示目标连接状态和所选受众的“审阅”屏幕截图。](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png){zoomable="yes"}

## 疑难解答 {#troubleshooting}

如果目标代表无法找到您的受众，请与[!DNL Adobe]代表联系以获得帮助。

向您的[!DNL Adobe]代表提供以下信息：

* 受众名称
* 目标名称
* 受众激活日期
* 导出的文件名

## 后续步骤 {#next-steps}

您已将受众成功激活到所选的目标平台。 接下来，请联系您的目标平台代表以开始设置您的营销活动。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。
