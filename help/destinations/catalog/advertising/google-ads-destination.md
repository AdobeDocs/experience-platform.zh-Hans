---
keywords: Google ads；google ads；google adwords；Google AdWords；Google Adwords
title: Google Ads连接
description: Google Ads以前称为Google AdWords，是一种在线广告服务，它允许企业通过基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示，按每次点击付费进行广告。
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 3%

---

# [!DNL Google Ads] 连接

## 概述 {#overview}

[!DNL Google Ads]，以前称为 [!DNL Google AdWords]，是一种在线广告服务，它允许企业通过基于文本的搜索、图形显示 [!DNL YouTube] 视频和应用程序内移动显示。

## 目标详情 {#specifics}

请注意以下特定于的详细信息 [!DNL Google Ads] 目标：

* 激活的受众以编程方式创建于 [!DNL Google] 平台。
* [!DNL Platform] 当前不包括用于验证激活是否成功的测量指标。 请参阅Google中的受众计数，以验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用创建您的第一个目标 [!DNL Google Ads] 并且尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去(使用Audience Manager或其他应用程序)的Experience CloudID服务中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了Google集成，则您设置的ID同步将会结转到Platform。

## 支持的身份 {#supported-identities}

[!DNL Google Ad Manager] 支持激活下表中描述的标识。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 当源身份是GAID命名空间时，请选择此目标身份。 |
| IDFA | [!DNL Apple ID for Advertisers] | 当源身份是IDFA命名空间时，请选择此目标身份。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为 [!DNL Device ID]. 38位数的设备ID，Audience Manager与每台与其交互的设备相关联。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) 定位加利福尼亚的用户，以及所有其他用户的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 使用此ID定位加利福尼亚州以外的用户。 |
| RIDA | 适用于广告的Roku ID。 此ID唯一标识Roku设备。 |  |
| 女佣 | Microsoft广告ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID唯一标识Amazon Fire电视。 |  |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您要将受众的所有成员导出到Google目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

### 现有 [!DNL Google Ads] 帐户

>[!IMPORTANT]
>
> [!DNL Google] 已弃用新的 [!DNL Google Ads] Cookie与第三方供应商集成。 要执行下一节中的允许列表步骤，您必须与集成 [!DNL Google Ads]. 因此，推荐使用 [!DNL Google Ads] 正在设置 [!DNL Google Customer Match] 集成。 有关创建 [!DNL Google Customer Match] 集成，请阅读有关创建 [[!DNL Google Customer Match]](./google-customer-match.md) 连接。

### 允许列表 {#allow-listing}

>[!NOTE]
>
>必须先将添加到允许列表，然后才能设置您的第一个 [!DNL Google Ads] Platform的目标。 请确保以下说明的允许列表流程已由完成 [!DNL Google] 创建目标之前。
>此规则的例外情况是 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 客户。 如果您已在Audience Manager中创建了到此Google目标的连接，则无需再次完成允许列表流程，您可以继续后续步骤。

创建 [!DNL Google Ads] Platform中的目标，您必须联系 [!DNL Google] 用于将Adobe添加到允许的数据提供程序列表，以及用于将您的帐户添加到允许列表。 联系人 [!DNL Google] 并提供以下信息：

* **帐户ID**：Adobe在Google中的帐户ID。 帐户ID：87933855。
* **客户ID**：AdobeGoogle的客户帐户ID。 客户ID：89690775。
* 您的帐户类型： **AdWords**
* **Google AdWords ID**：这是您的ID，包含 [!DNL Google]. ID格式通常为123-456-7890。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

同时 [设置](../../ui/connect-destination.md) 此目标必须提供以下信息：

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 帐户类型]**： AdWords是唯一可用的选项。
* **[!UICONTROL 帐户ID]**：使用填写您的帐户ID [!DNL Google Ads]. ID格式通常为123-456-7890。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

请参阅 [将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

## 导出的数据

验证数据是否已成功导出到 [!DNL Google Ads] 目标，检查您的 [!DNL Google Ads] 帐户。 如果激活成功，则会在您的帐户中填充受众。

## 故障排除 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

当客户帐户不符合 [先决条件](#prerequisites) 或客户尝试在没有现有的情况下配置目标时 [!DNL Google Ads] 帐户。

[!DNL Google] 已弃用新的 [!DNL Google Ads] Cookie与第三方供应商集成。 要执行 [允许列表](#allow-listing) 步骤，您必须现有与的集成 [!DNL Google Ads].

使用的推荐方法 [!DNL Google Ads] 正在设置 [[!DNL Google Customer Match]](google-customer-match.md) 集成。
