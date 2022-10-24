---
title: Adobe Advertising Cloud DSP连接
description: Adobe Advertising Cloud DSP是Adobe Real-time Customer Data Platform的一个集成目标，允许您与已批准的广告商和用户共享经过身份验证的第一方区段，以激活促销活动。
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---

# Adobe Advertising Cloud DSP连接

## 概述 {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP)目标允许您与已批准的广告商和用户共享经过身份验证的第一方区段，以便与DSP一起激活促销活动。 要了解有关Real-Time CDP与DSP集成的更多信息，请参阅 [关于从受众源激活经过身份验证的区段](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>此页面由DSP团队创建。 如有任何查询或更新请求，请直接联系Advertising Cloud支持人员，联系电话： `adcloud_support@adobe.com`.

## 用例 {#use-cases}

为了帮助您更好地了解如何以及何时使用Advertising Cloud DSP目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 品牌广告用例

一家在线零售商希望通过展示型营销活动重新定位其高价值客户，而无需使用Cookie进行定位。 该零售商将一个区段共享，该区段由其Adobe Real-time Customer Data Platform(Real-Time CDP)帐户中高价值客户经过哈希处理的电子邮件ID组成，并共享到其DSP帐户中。 然后，DSP将经过哈希处理的电子邮件ID转换为经过身份验证的ID [!DNL RampIDs] 通过DSP与LiveRamp的合作伙伴关系。 结果 [!DNL RampIDs] 可在展示型营销活动中使用以定位受众。

### 代理用例

拥有DSP帐户的媒体代理正代表其客户（酒店业的顶级品牌）开展重定位活动。 该品牌希望在过去一年通过新的促销活动来重新定位所有客人。 该品牌在 [!DNL Real-Time CDP]. 该品牌可以共享一个区段，该区段包含来自其 [!DNL Real-Time CDP] 帐户转到媒体代理的DSP帐户，以通过媒体营销活动重新定位客人。

## 先决条件 {#prerequisites}

* DSP帐户级别和营销活动级别设置，用于启用与 [!DNL LiveRamp RampID]，将客户数据转换为 [!DNL RampIDs] 创建可定位的区段。 您的DSP帐户团队将执行此配置。 [!DNL RampID] 可通过DSP与 [!DNL LiveRamp]，而且您不需要自己的 [!DNL LiveRamp] 会员资格来使用它。
* Experience Cloud帐户的Experience Platform组织ID。 您可以在 [!DNL Real-Time CDP] 用户配置文件页面。
* A [[!DNL Real-Time CDP] DSP中的源](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) 接收促销活动激活的区段。 您的DSP帐户团队将使用您的Experience Cloud组织ID创建源。
* DSP帐户或广告商的源密钥，在 [[!DNL Real-Time CDP] 源在DSP中创建](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). 您的DSP帐户团队将与您共享此密钥。 您将在Experience Platform中使用它创建到Advertising Cloud DSP目标的目标连接，如 [下文](#authenticate).
* 由电子邮件或经过哈希处理的电子邮件组成的客户数据。

## 支持的身份 {#supported-identities}

Adobe Advertising Cloud DSP目标支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项，让Experience Platform自动对激活时的数据进行哈希处理。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，以及Advertising Cloud DSP目标中使用的标识符（电子邮件或哈希电子邮件）。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 当基于区段评估在Experience Platform中更新用户档案时，连接器将更新发送到下游目标平台。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions) Experience Platform。 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到目标，请按照 [创建目标连接](/help/destinations/ui/connect-destination.md) 使用Experience Platform用户界面。 在目标配置工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

要连接到目标，请在 [!UICONTROL 连接类型] ，然后选择 **[!UICONTROL 连接到目标]**.:

* **[!UICONTROL 帐户或广告商密钥]**:此 [!UICONTROL 源键] 在 [[!DNL Real-Time CDP] 源在DSP用户界面中创建](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). 您的DSP帐户团队在创建源后将与您共享此密钥。

![连接类型字段](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。

![目标详细信息字段](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 验证数据导出 {#exported-data}

要验证数据区段是否已与Advertising Cloud共享，请检查以下内容：

* 您的 [!DNL Real-Time CDP] 目标成功。

* 在DSP中，当您通过 [!UICONTROL 受众] > [!UICONTROL 所有受众] 或 [!UICONTROL 受众定位] 部分。 区段应在 [!UICONTROL Adobe区段] 选项卡 [!UICONTROL Real-Time CDP] 文件夹。

![Real-Time CDP受众设置中的DSP区段](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).
