---
title: Acxiom Audience Distribution
description: 使用 [!DNL Acxiom Audience Distribution] 目标通过 [!DNL Acxiom's Real ID] 技术增强受众并将受众激活到多个平台，如 [!DNL Altice]、 [!DNL Ampersand]、 [!DNL Comcast]等。
badge: label="Beta 版" type="Informative"
exl-id: bac0f337-bfab-4779-acc8-f70239552666
source-git-commit: 290d6eb20b7d35839b4bb37e71e2c993b112d896
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 6%

---

# [!DNL Acxiom Audience Distribution]目标

>[!NOTE]
>
>[!DNL Acxiom Audience Distribution]目标为测试版。 此目标连接器和文档页面由[!DNL Acxiom]团队创建和维护。 如有任何查询或更新请求，请直接[此处](mailto:acxiom-adobe-help@acxiom.com)联系Acxiom。

使用[!DNL Acxiom Audience Distribution]目标通过[!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/)技术增强受众并将受众激活到多个平台，如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。

本教程提供了使用[!DNL Acxiom Audience Distribution]用户界面创建[!DNL Adobe Experience Platform]目标连接器的说明。 此连接器用于构建受众并将受众分发到选定的目标。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Acxiom Audience Distribution]目标，以下是[!DNL Adobe Experience Platform]客户可以通过使用此连接器解决的示例用例。

### 将受众从Experience Platform发送到您的Acxiom帐户 {#send-audiences}

如果您是营销专业人员，想要将受众从[!DNL Experience Platform]发送到您的[!DNL Acxiom]帐户以进行跨渠道客户获取，请使用此目标连接器。

例如，一家全球金融服务品牌的营销运营部对通过多个广告平台进行跨渠道客户获取感兴趣。 他们可以使用[!DNL Acxiom Audience Distribution]目标连接器将受众从[!DNL Experience Platform]发送到[!DNL Acxiom]，通过[!DNL Acxiom's Real ID]技术增强受众，并将受众激活到多个平台，如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。

## 先决条件 {#prerequisites}

* **确认使用条款：**&#x200B;在配置新的[!DNL Acxiom Audience Distribution]目标之前，您必须阅读并签署[!DNL Acxiom's]使用条款协议。 在您执行的销售订单完成后，您将收到指向协议的链接。 在您签署协议之前，不会在Experience Platform目标目录中看到[!DNL Acxiom Audience Distribution]目标卡。 在您接受并签署协议后，[!DNL Adobe]将完成您的载入流程，您将会看到[!DNL Acxiom Audience Distribution]目标卡。
* **知道您的Adobe组织ID：**&#x200B;需要您的[!DNL Adobe]组织ID才能完成您的用户协议条款。 有关如何[!DNL Adobe's]查看组织ID *的详细信息，请参阅* [Experience Cloud中的组织](https://experienceleague.adobe.com/zh-hans/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)主题。

## 支持的目标 {#supported-destinations}

[!DNL Acxiom Audience Distribution]目标当前支持对以下平台进行受众激活。<br>

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## 连接到目标 {#connect}

为了方便起见，系统将在后台自动处理对[!DNL Acxiom's Audience Distribution]目标的身份验证。

## 目标特定的设置 {#destination-settings}

某些[!DNL Acxiom Audience Distribution]目标需要其他信息。 以下部分提供了有关如何配置这些选项的详细指导。

### [!DNL LG Ads] {#lg-ads}

要配置目标的详细信息，请填写以下字段。

* **区段类别**：您的区段所属的目标类别或垂直类别。 例如：金融服务、汽车、卫生等。

![LG广告目标详细信息](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png)

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将受众数据激活到批处理配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

>[!NOTE]
>
>[!DNL Acxiom Audience Distribution]目标仅支持完整文件导出。

### 映射属性和身份 {#map}

要使[!DNL Acxiom Audience Distribution]目标正确接收受众数据，您必须将源字段从Experience Platform映射到正确的[!DNL Acxiom Audience Distribution]目标字段。

[!DNL Acxiom Audience Distribution]仅允许映射到以下目标字段。 必须按照以下显示的顺序映射下表中描述的目标字段。

| 字段名称 | 描述 | 必需 | 字段顺序 | 最大长度 |
|---|---|---|---|---|          
| 名字 | 个人的名字 | 否 | 1 | 255 |
| 中 | 个人的中间名或首字母 | 否 | 2 | 50 |
| 姓氏 | 个人的姓氏 | 是 | 3 | 255 |
| 代后缀 | 个人后缀 | 否 | 4 | 10 |
| 地址行1 | 地址1主要居住地字段 | 是 | 5 | 255 |
| 地址行2 | 主要居住地的地址2字段 | 否 | 6 | 255 |
| 城市 | 主要居住地城市 | 是 | 7 | 255 |
| State | 主要居住地的缩写 | 是 | 8 | 2 |
| 邮政编码 | 主要居住地的完整邮政编码 | 是 | 9 | 10 |
| 电子邮件 | 主电子邮件默认情况下，此字段用作重复数据删除键以使记录唯一 | 否 | 10 | 255 |
| 电话 | 个人电话号码（区号+号码）<br>默认情况下，此字段用作重复数据删除键以使记录唯一。 | 否 | 11 | 10 |

在&#x200B;**[!UICONTROL Source字段]**&#x200B;列中，输入要映射到相应目标字段的每个源属性的名称，或选择箭头图标以打开&#x200B;**[!UICONTROL 选择源字段]**&#x200B;屏幕。<br>
![映射屏幕](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png)

映射所有字段后，选择&#x200B;**[!UICONTROL 下一步]**。

如果您没有使用[!DNL Adobe's]标准架构，请参阅[查询服务UI指南](../../../query-service/ui/overview.md)文档，以了解如何使用查询服务将您的字段名填充[!DNL Adobe]标准架构。

### 审查 {#review}

完成上述所有步骤后，您就有机会在激活（分发）目标连接之前查看其状态和受众详细信息。 您选择的受众将显示在列表底部。 每个受众将是一个对[!DNL Acxiom Audience Distribution] API的单独调用。

如果您对结果满意，请选择&#x200B;**[!UICONTROL 完成]**&#x200B;以激活您的目标。

![审核您的受众](../../assets/catalog/advertising/acxiom-audience-distribution/review_audience.png)

## 故障排除 {#troubleshooting}

如果目标代表无法找到您的受众，请与[!DNL Adobe]代表联系以获得帮助。

您需要向[!DNL Adobe]代表提供以下信息：

* 受众名称
* 目标名称
* 受众激活日期
* 导出的文件名

## 后续步骤 {#next-steps}

按照本教程，您已成功将受众激活到所选的目标平台。 接下来，请联系您的目标平台代表以开始设置您的营销活动。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/data-governance/home)。
