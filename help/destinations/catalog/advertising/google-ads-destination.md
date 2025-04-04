---
title: Google Ads连接
description: Google Ads以前称为Google AdWords，是一种在线广告服务，它允许企业通过基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示，按每次点击付费进行广告。
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 2%

---

# [!DNL Google Ads]连接

## 概述 {#overview}

[!DNL Google Ads]（以前称为[!DNL Google AdWords]）是一种在线广告服务，它允许企业通过基于文本的搜索、图形显示、[!DNL YouTube]视频和应用程序内移动显示，按点击付费广告。

## 目标详情 {#specifics}

请注意以下特定于[!DNL Google Ads]目标的详细信息：

* 在[!DNL Google]平台中以编程方式创建激活的受众。
* [!DNL Experience Platform]当前不包括用于验证激活是否成功的度量指标。 请参阅Google中的受众计数，以验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用[!DNL Google Ads]创建您的第一个目标，并且以前未在Experience Cloud ID服务(使用Audience Manager或其他应用程序)中启用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe Consulting或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了Google集成，则您设置的ID同步功能将会转移到Experience Platform。

## 支持的身份 {#supported-identities}

[!DNL Google Ads]支持激活下表中描述的标识。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 当源身份是GAID命名空间时，请选择此目标身份。 |
| IDFA | [!DNL Apple ID for Advertisers] | 当源身份是IDFA命名空间时，请选择此目标身份。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为[!DNL Device ID]。 Audience Manager与其交互的每个设备相关联的38位数字设备ID。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)来定位加利福尼亚州的用户，并使用Google Cookie ID来定位所有其他用户。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google]使用此ID定位加州以外的用户。 |
| RIDA | Advertising的Roku ID。 此ID唯一标识Roku设备。 |  |
| 女佣 | Microsoft Advertising ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID唯一标识Amazon Fire电视。 |  |

{style="table-layout:auto"}

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
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您要将受众的所有成员导出到Google目标。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

### 现有[!DNL Google Ads]帐户

>[!IMPORTANT]
>
> [!DNL Google]已弃用与第三方供应商的新[!DNL Google Ads] Cookie集成。 要执行下一节中的允许列表步骤，您必须与[!DNL Google Ads]现有集成。 因此，推荐使用[!DNL Google Ads]的方法是设置[!DNL Google Customer Match]集成。 有关创建[!DNL Google Customer Match]集成的更多详细信息，请阅读有关创建[[!DNL Google Customer Match]](./google-customer-match.md)连接的教程。

### 允许列表 {#allow-listing}

>[!NOTE]
>
>在Experience Platform中设置您的第一个[!DNL Google Ads]目标之前，必须将该目标列入允许列表。 在创建目标之前，请确保[!DNL Google]已完成下面描述的允许列表流程。
>此规则的例外情况适用于[Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html)客户。 如果您已在Audience Manager中创建了到此Google目标的连接，则无需再次完成允许列表流程，您可以继续后续步骤。

在Experience Platform中创建[!DNL Google Ads]目标之前，您必须联系[!DNL Google]，以便Adobe列入允许列表被列入允许的数据提供程序列表，并且您的帐户将被添加到中。 联系[!DNL Google]并提供以下信息：

* **帐户ID**： Adobe与Google的帐户ID。 帐户ID：87933855。
* **客户ID**： Adobe的客户帐户ID与Google。 客户ID：89690775。
* 您的帐户类型： **AdWords**
* **Google AdWords ID**：这是您与[!DNL Google]的ID。 ID格式通常为123-456-7890。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 帐户类型]**： AdWords是唯一可用的选项。
* **[!UICONTROL 帐户ID]**：使用[!DNL Google Ads]填写帐户ID。 ID格式通常为123-456-7890。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到[!DNL Google Ads]目标，请检查您的[!DNL Google Ads]帐户。 如果激活成功，则会在您的帐户中填充受众。

## 故障排除 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

当客户帐户不符合[先决条件](#prerequisites)或客户尝试在没有现有[!DNL Google Ads]帐户的情况下配置目标时，会发生此错误。

[!DNL Google]已弃用与第三方供应商的新[!DNL Google Ads] Cookie集成。 要执行[允许列表](#allow-listing)步骤，您必须与[!DNL Google Ads]现有集成。

使用[!DNL Google Ads]的建议方法是设置[[!DNL Google Customer Match]](google-customer-match.md)集成。
