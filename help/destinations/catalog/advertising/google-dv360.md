---
keywords: 双击竞价管理器；双击竞价管理器；双击；显示和视频360；显示360；视频360；视频360；显示360；显示360；显示360；显示360；显示
title: Google Display & Video 360连接
description: 显示和视频360（以前称为“双击竞价管理器”）是一种工具，用于在显示、视频和移动设备库存源中执行重定位和受众定位的数字促销活动。
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] 连接

## 概述 {#overview}

[!DNL Display & Video 360]，以前称为 [!DNL DoubleClick Bid Manager]，是用于跨显示、视频和移动设备库存源执行重定向和受众定位的数字促销活动的工具。

## 目标详情 {#specifics}

请注意以下特定于 [!DNL Google Display & Video 360] 目标：

* 激活的受众在Google平台中以编程方式创建。
* [!DNL Platform] 当前不包括用于验证激活是否成功的测量量度。 请参阅Google中的受众计数，以验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用Google Display &amp; Video 360创建第一个目标，但尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去的Experience CloudID服务(使用Adobe Audience Manager或其他应用程序)中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了Google集成，则您设置的ID同步会传递到Platform。

## 支持的身份 {#supported-identities}

[!DNL Google Display & Video 360] 支持激活下表所述的身份。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 如果源标识是GAID命名空间，请选择此目标标识。 |
| IDFA | [!DNL Apple ID for Advertisers] | 如果源标识是IDFA命名空间，请选择此目标标识。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为 [!DNL Device ID]. 一个38位数的数字设备ID，Audience Manager会将其与之交互的每个设备相关联。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) 来定位加利福尼亚州的用户，以及所有其他用户的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 会使用此ID来定位加州以外的用户。 |
| RIDA | 用于广告的Roku ID。 此ID唯一标识Roku设备。 |  |
| 女佣 | Microsoft广告ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID可唯一标识Amazon Fire TV。 |  |

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您将区段（受众）的所有成员导出到Google目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

## 先决条件 {#prerequisites}

### 允许列表 {#allow-listing}

>[!NOTE]
>
>在设置第一个允许列表之前，必须将其添加到允许列表 [!DNL Google Display & Video 360] 目标。 在创建目标之前，请确保Google已完成下面描述的允许列表流程。

在创建 [!DNL Google Display & Video 360] 目标中，您必须联系Google，要求将Adobe添加到允许的数据提供程序列表中，并将您的帐户添加到允许列表中。 联系Google并提供以下信息：

* **帐户ID**:Adobe的帐户ID与Google。 帐户ID:87933855。
* **客户ID**:Adobe的客户帐户ID和Google。 客户ID:89690775。
* **您的帐户类型**:use **[!DNL Invite advertiser]** 允许将受众仅共享到您的Display &amp; Video 360帐户中的特定品牌，或使用 **[!DNL Invite partner]** 以允许将受众共享到您的Display &amp; Video 360帐户中的所有品牌。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 帐户类型]**:根据您使用Google的帐户选择一个选项：
   * 使用 `Invite Advertiser` ，以便仅将受众共享到您的Display &amp; Video 360帐户中的特定品牌。
   * 使用 `Invite Partner` 以允许将受众共享到您的Display &amp; Video 360帐户中的所有品牌。
* **[!UICONTROL 帐户ID]**:填写 **[!DNL Invite partner]** 或 **[!DNL Invite advertiser]** 帐户ID与Google。 通常是一个六位或七位数的ID。

>[!NOTE]
>
>设置 [!DNL Google Display & Video 360] 目标，请与您的 [!DNL Google Account Manager] 或Adobe代表，了解您拥有的帐户类型。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据

验证数据是否已成功导出到 [!DNL Google Display & Video 360] 目标位置，检查 [!DNL Google Display & Video 360] 帐户。 如果激活成功，则帐户中会填充受众。

## 故障排除 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

当客户帐户与 [先决条件](#prerequisites). 要解决此问题，请联系Google并确保您的帐户已允许列出。