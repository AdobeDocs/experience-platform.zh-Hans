---
title: Acxiom Real ID&amp；贸易；受众连接
description: 使用 [!DNL Acxiom Real ID&trade; Audience Connection] 目标通过 [!DNL Acxiom's Real ID] 技术增强受众并将受众激活到多个平台，如 [!DNL Altice]、 [!DNL Ampersand]、 [!DNL Comcast]等。
badge: label="Beta 版" type="Informative"
exl-id: 5f1f0f7f-ac46-42bd-8002-be50fab5a76b
source-git-commit: 1013487e2c38aeb1e2b0388f0c317afdcf02ba62
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 3%

---

# [!DNL Acxiom Real ID™ Audience Connection]目标

>[!NOTE]
>
>[!DNL Acxiom Real ID™ Audience Connection]目标为测试版。 此目标连接器和文档页面由[!DNL Acxiom]团队创建和维护。 如有任何查询或更新请求，请直接[此处](mailto:acxiom-adobe-help@acxiom.com)联系Acxiom。

使用[!DNL Acxiom Real ID Audience Connection]目标通过[!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/)技术增强受众并将受众激活到多个平台，如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。

本教程提供了使用[!DNL Acxiom Real ID Audience Connection]用户界面创建[!DNL Adobe Experience Platform]目标连接器的说明。 此连接器用于构建受众并将受众分发到选定的目标。

## 用例 {#use-cases}

此连接器支持将Acxiom真实身份作为标识符加载到Real-Time CDP中的客户端。 为了帮助您更好地了解您应如何以及何时使用[!DNL Acxiom Real ID Audience Connection]目标，以下是[!DNL Adobe Experience Platform]客户可以通过使用此连接器解决的示例用例。

### 将受众从Experience Platform发送到您的Acxiom帐户 {#send-audiences}

如果您是营销专业人员，想要将受众从[!DNL Experience Platform]发送到您的[!DNL Acxiom]帐户以进行跨渠道客户获取，请使用此目标连接器。

例如，一家全球金融服务品牌的营销运营部对通过多个广告平台进行跨渠道客户获取感兴趣。 他们可以使用[!DNL Acxiom Real ID Audience Connection]目标连接器将受众从[!DNL Experience Platform]发送到[!DNL Acxiom]，通过[!DNL Acxiom's Real ID]技术增强受众，并将受众激活到多个平台，如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。


## 先决条件 {#prerequisites}

* **确认使用条款：**&#x200B;在配置新的[!DNL Acxiom Real ID Audience Connection]目标之前，您必须阅读并签署[!DNL Acxiom's]使用条款协议。 在您执行的销售订单完成后，您将收到指向协议的链接。 在您签署协议之前，不会在Experience Platform目标目录中看到[!DNL Acxiom Real ID Audience Connection]目标卡。 在您接受并签署协议后，[!DNL Adobe]将完成您的载入流程，您将会看到[!DNL Acxiom Real ID Audience Connection]目标卡。
* **知道您的Adobe组织ID：**&#x200B;需要您的[!DNL Adobe]组织ID才能完成您的用户协议条款。 有关如何[!DNL Adobe's]查看组织ID *的详细信息，请参阅* [Experience Cloud中的组织](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)主题。
* **获取[!DNL Acxiom's Real ID]产品的许可证：**&#x200B;获取许可证后，在Real-Time CDP中提供Acxiom的实际ID。 有关详细信息，请参阅[Acxiom数据增强](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/data-partner/acxiom-data-enhancement)。


## 支持的身份 {#supported-identities}

[!DNL Acxiom's Real ID Audience Connection]目标支持激活下表中描述的标识。 了解有关[标识](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/identity/features/namespaces)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---------------|----------------|----------------|
| 实际ID | [!DNL Acxiom Real ID] | 当源身份是Acxiom Real ID命名空间时，请选择此目标身份。 |
| extern_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------------|----------------|----------------|
| Segmentation Service | ✓ | 通过Experience Platform [分段服务](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/segmentation/home)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-portal#import-audience)导入Experience Platform。 |


## 支持的目标 {#supported-destinations}

[!DNL Acxiom's Real ID Audience Connection]目标当前支持对以下平台进行受众激活。

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## 连接到目标 {#connect}

为了方便起见，系统将在后台自动处理对[!DNL Acxiom's Real ID Audience Connection]目标的身份验证。

## 目标特定的设置 {#destination-settings}

某些[!DNL Acxiom Real ID Audience Connection]目标需要其他信息。 以下部分提供了有关如何配置这些选项的详细指导。

### [!DNL LG Ads] {#lg-ads}

要配置目标的详细信息，请填写以下字段。

* **区段类别**：您的区段所属的目标类别或垂直类别。 例如：金融服务、汽车、卫生等。

![LG广告目标详细信息](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png)


## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}



有关将受众激活到此目标的说明，请阅读[将受众数据激活到批处理配置文件导出目标](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)。

>[!NOTE]
>
>[!DNL Acxiom Real ID Audience Connection]目标仅支持完整文件导出。


### 映射属性和身份 {#map}

要使[!DNL Acxiom Real ID Audience Connection]目标正确接收受众数据，您必须将源字段从Experience Platform映射到正确的[!DNL Acxiom Real ID Audience Connection]目标字段。

[!DNL Acxiom Real ID Audience Connection]仅允许映射到以下目标字段。

| 字段名称 | 描述 | 必需 |
|--------------------|------------|--------| 
| 实际ID | 实数ID是Acxiom专有身份解析图形中唯一的36字节字母数字标识符(ID)，类似于关系数据库的主键。 它是表示个人、家庭或地址的标识符。 | 是 |



在&#x200B;**[!UICONTROL Source字段]**&#x200B;列中，输入要映射到相应目标字段的源属性的名称，或选择箭头图标以打开&#x200B;**[!UICONTROL 选择源字段]**&#x200B;屏幕。 然后选择&#x200B;**[!UICONTROL 下一步]**。
![映射屏幕](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png)


如果您没有使用[!DNL Adobe's]标准架构，请参阅[查询服务UI指南](../../../query-service/ui/overview.md)文档，以了解如何使用查询服务将您的字段名填充[!DNL Adobe]标准架构。


### 审查 {#review}

完成上述所有步骤后，您就有机会在激活（分发）目标连接之前查看其状态和受众详细信息。 您选择的受众将显示在列表底部。 每个受众将是一个对[!DNL Acxiom Real ID Audience Connection] API的单独调用。

如果您对结果满意，请选择&#x200B;**[!UICONTROL 完成]**&#x200B;以激活您的目标。

![审核您的受众](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png)


## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)。

## 故障排除 {#troubleshooting}

如果目标代表无法找到您的受众，请与[!DNL Adobe]代表联系以获得帮助。

您需要向[!DNL Adobe]代表提供以下信息：

* 受众名称
* 目标名称
* 受众激活日期
* 导出的文件名

## 后续步骤 {#next-steps}

按照本教程，您已成功将受众激活到所选的目标平台。 接下来，请联系您的目标平台代表以开始设置您的营销活动。
