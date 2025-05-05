---
title: Adobe Advertising Cloud DSP连接
description: Adobe Advertising Cloud DSP是Adobe Real-time Customer Data Platform的一个集成目标，允许您与批准广告商和用户共享经过身份验证的第一方受众，以便激活campaign。
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 2%

---

# Adobe Advertising Cloud DSP连接

## 概述 {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP)目标允许您与已批准的广告商和用户共享经过身份验证的第一方受众，以便通过DSP激活营销活动。 要了解有关Real-Time CDP与DSP集成的更多信息，请参阅[关于从受众源激活经过身份验证的受众](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html?lang=zh-Hans)。

>[!IMPORTANT]
>
>此页面由DSP团队创建。 如有任何查询或更新请求，请直接通过`adcloud_support@adobe.com`联系Advertising Cloud支持部门。

## 用例 {#use-cases}

为了帮助您更好地了解应当如何以及何时使用Advertising Cloud DSP目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 品牌广告用例

一家在线零售商希望通过展示促销活动重新定位其高价值客户，而无需使用Cookie进行定位。 该零售商共享受众，其中包括其Adobe Real-time Customer Data Platform (Real-Time CDP)帐户到其DSP帐户中高价值客户的经过哈希处理的电子邮件ID。 然后，DSP通过DSP和LiveRamp之间的合作关系将经过哈希处理的电子邮件ID转换为经过身份验证的[!DNL RampIDs]。 生成的[!DNL RampIDs]可用于显示营销活动以定位受众。

### 机构用例

一家拥有DSP账户的媒体机构正代表其客户（酒店业顶级品牌）开展重新定位活动。 该品牌希望通过新的促销活动重新定位去年所有客人。 该品牌在[!DNL Real-Time CDP]中托管所有来宾信息。 品牌可以共享受众，该受众包含其[!DNL Real-Time CDP]帐户中访客的经过哈希处理的电子邮件ID，以通过媒体营销活动重新定位访客。媒体代理的DSP帐户中包含受众。

## 先决条件 {#prerequisites}

* DSP帐户级别和营销活动级别的设置以启用与[!DNL LiveRamp RampID]的受众共享，这会将客户数据转换为[!DNL RampIDs]以创建可定位的区段。 您的DSP帐户团队将执行此配置。 [!DNL RampID]可通过DSP与[!DNL LiveRamp]之间的合作关系使用，您不需要自己的[!DNL LiveRamp]成员资格即可使用它。
* Experience PlatformExperience Cloud的组织ID。 您可以在[!DNL Real-Time CDP]用户配置文件页面上找到您的ID。
* DSP[&#128279;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=zh-Hans)中用于接收营销活动激活受众的[!DNL Real-Time CDP] 源。 您的DSP客户团队将使用您的Experience Cloud组织ID创建源。
* DSP帐户或广告商的源密钥，在DSP[&#128279;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=zh-Hans)中创建[[!DNL Real-Time CDP] 源时生成。 您的DSP帐户团队将与您共享此密钥。 您将在Experience Platform中使用它来创建到Advertising Cloud DSP目标的目标连接，如下面](#authenticate)所述。
* 包含电子邮件或经过哈希处理的电子邮件的客户数据。

## 支持的身份 {#supported-identities}

Adobe Advertising Cloud DSP目标支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使Experience Platform在激活时自动对数据进行哈希处理。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在使用Advertising Cloud DSP目标中使用的标识符（电子邮件或哈希电子邮件）导出受众的所有成员。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 当基于受众评估在Experience Platform中更新用户档案时，连接器将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要具有&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)才能进行Experience Platform。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到目标，请按照说明[使用Experience Platform用户界面创建目标连接](/help/destinations/ui/connect-destination.md)。 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

若要连接到目标，请在[!UICONTROL 连接类型]部分提供以下参数，然后选择&#x200B;**[!UICONTROL 连接到目标]**：

* **[!UICONTROL 帐户或广告商密钥]**：在DSP用户界面[&#128279;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=zh-Hans)中创建[!DNL Real-Time CDP] 源时生成此[!UICONTROL Source密钥]。 您的DSP客户团队将在创建源后与您共享此密钥。

![连接类型字段](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

![目标详细信息字段](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

## 验证数据导出 {#exported-data}

要验证是否与Advertising Cloud共享了数据受众，请检查以下各项：

* [!DNL Real-Time CDP]目标中的数据流成功。

* 在DSP中，当您从[!UICONTROL 受众] > [!UICONTROL 所有受众]中创建或编辑受众时，或者从版面设置的[!UICONTROL 受众定位]部分中创建或编辑受众时，该受众可用。 受众应显示在[!UICONTROL Real-Time CDP]文件夹下的[!UICONTROL Adobe区段]选项卡中。

DSP受众设置中的![Real-Time CDP受众](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。
