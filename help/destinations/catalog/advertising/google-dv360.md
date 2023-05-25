---
keywords: DoubleClick Bid Manager；DoubleClick Bid Manager；DoubleClick；显示和视频360；显示360；视频360；显示360；显示和视频
title: Google显示和视频360连接
description: Display & Video 360（以前称为DoubleClick Bid Manager）是一种工具，用于在显示器、视频和移动设备库存源中执行重定位和面向受众的数字活动。
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 326127996a27df41383ef67da765f7b0818f17f2
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] 连接

## 概述 {#overview}

[!DNL Display & Video 360]，以前称为 [!DNL DoubleClick Bid Manager]是一个工具，用于在显示、视频和移动设备库存源中执行重定位和面向受众的数字营销活动。

## 目标详情 {#specifics}

请注意以下特定于的详细信息 [!DNL Google Display & Video 360] 目标：

* 激活的受众是在Google平台中以编程方式创建的。
* 将受众回填激活到 [!DNL Google Display & Video 360] 按计划，目标会在区段首次映射到目标连接后的24-48小时内发生。 此更新是为了响应Google等待24小时直到摄取数据的策略，旨在提高Real-time CDP与之间的匹配率 [!DNL Google Display & Video 360]. 请注意，这是只适用于此目标的后端配置，与UI中任何客户可配置的计划选项无关。

>[!IMPORTANT]
>
>如果您希望使用Google Display &amp; Video 360创建第一个目标，但尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去(使用Adobe Audience Manager或其他应用程序)的Experience CloudID服务中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了Google集成，则您设置的ID同步会转移到平台。

## 支持的身份 {#supported-identities}

[!DNL Google Display & Video 360] 支持激活下表中描述的标识。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 当源身份是GAID命名空间时，选择此目标身份。 |
| IDFA | [!DNL Apple ID for Advertisers] | 当源身份是IDFA命名空间时，选择此目标身份。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为 [!DNL Device ID]. 38位数的数字设备ID，Audience Manager将其关联到与其交互的每个设备。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hans) 定位加利福尼亚的用户，以及所有其他用户的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 使用此ID定位加利福尼亚州以外的用户。 |
| RIDA | 适用于广告的Roku ID。 此ID唯一标识Roku设备。 |  |
| MAID | Microsoft广告ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID唯一标识Amazon Fire电视。 |  |

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要将区段（受众）的所有成员导出到Google目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

## 先决条件 {#prerequisites}

### 允许列表 {#allow-listing}

>[!NOTE]
>
>必须先将添加到允许列表，然后才能设置您的第一个 [!DNL Google Display & Video 360] Platform的目标。 请确保以下描述的“允许列表”流程已由完成 [!DNL Google] 创建目标之前。
>此规则的例外情况是 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 客户。 如果您已在Audience Manager中创建了到此Google目标的连接，则无需再次完成允许列表过程，您可以继续后续步骤。

创建之前 [!DNL Google Display & Video 360] 目标，您必须联系Google请求将Adobe添加到允许的数据提供商列表，并将您的帐户添加到允许列表中。 请联系Google并提供以下信息：

* **帐户ID**：Adobe的帐户ID与Google 帐户ID：87933855。
* **客户ID**：Adobe的客户帐户ID与Google。 客户ID：89690775。
* **您的帐户类型**：使用 **[!DNL Invite advertiser]** 仅允许将受众共享给您的Display &amp; Video 360帐户中的特定品牌或使用 **[!DNL Invite partner]** 允许将受众共享给您的Display &amp; Video 360帐户中的所有品牌。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 必须提供以下信息，才能使用此目标：

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：可选。 例如，您可以提及要将此目标用于哪个营销活动。
* **[!UICONTROL 帐户类型]**：根据您在Google中的帐户，选择一个选项：
   * 使用 `Invite Advertiser` 仅允许将受众共享给您的“显示和视频360”帐户中的特定品牌。
   * 使用 `Invite Partner` 允许将受众共享给您的Display &amp; Video 360帐户中的所有品牌。
* **[!UICONTROL 帐户ID]**：填写您的 **[!DNL Invite partner]** 或 **[!DNL Invite advertiser]** Google的帐户ID。 通常，这是一个六位数或七位数的ID。

>[!NOTE]
>
>设置时 [!DNL Google Display & Video 360] 目标，请与您的 [!DNL Google Account Manager] 或Adobe代表，以了解您所拥有的客户类型。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到流式区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据

验证数据是否已成功导出到 [!DNL Google Display & Video 360] 目标，检查您的 [!DNL Google Display & Video 360] 帐户。 如果激活成功，则会在您的帐户中填充受众。

## 故障排除 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

当客户帐户不符合 [先决条件](#prerequisites). 要解决此问题，请联系Google并确保您的帐户已列入允许列表。