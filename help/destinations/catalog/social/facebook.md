---
keywords: facebook连接；facebook连接；facebook目标；facebook;instagram;Messenger;facebook Messenger
title: Facebook连接
description: 根据经过哈希处理的电子邮件，激活Facebook营销活动的用户档案以进行受众定位、个性化和抑制。
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 70670f7aec2ab6a5594f5e69672236c7bcc3ce81
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 1%

---

# [!DNL Facebook] 连接

## 概述 {#overview}

为 [!DNL Facebook] 基于经过哈希处理的电子邮件的受众定位、个性化和抑制促销活动。

您可以使用此目标在 [!DNL Facebook’s] 支持的一系列应用程序 [!DNL Custom Audiences]，包括 [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]和 [!DNL Messenger]. [!DNL Facebook Ads Manager] 中的版面级别会显示您要针对其运行营销活动的所选应用程序。

![FacebookAdobe Experience Platform UI中的目标](../../assets/catalog/social/facebook/catalog.png)

## 用例

以帮助您更好地了解如何以及何时使用 [!DNL Facebook] 目标中，以下是Adobe Experience Platform客户可通过使用此功能解决的两个示例用例。

### 用例#1

一家在线零售商希望通过社交平台与现有客户联系，并根据其先前的订单向他们显示个性化优惠。 该在线零售商可以将电子邮件地址从自己的CRM摄取到Adobe Experience Platform，从自己的离线数据构建区段，并将这些区段发送到 [!DNL Facebook] 社交平台，优化广告支出。

### 用例#2

一家航空公司拥有不同的客户层（Bronze、Silver和Gold），并希望通过社交平台为每个层提供个性化优惠。 但是，并非所有客户都使用航空公司的移动设备应用程序，其中一些客户尚未登录公司网站。 公司关于这些客户的唯一标识符是会员ID和电子邮件地址。

要在社交媒体中定位客户，他们可以将客户数据从CRM载入Adobe Experience Platform，并将电子邮件地址作为标识符。

接下来，他们可以使用离线数据（包括关联的会员ID和客户层）构建新的受众区段，并通过 [!DNL Facebook] 目标。

## 支持的身份 {#supported-identities}

[!DNL Facebook Custom Audiences] 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google Advertising ID | 如果源标识是GAID命名空间，请选择GAID目标标识。 |
| IDFA | Apple ID for Advertisers | 如果源标识是IDFA命名空间，请选择IDFA目标标识。 |
| phone_sha256 | 使用SHA256算法进行哈希处理的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 部分和将相应的命名空间分别用于纯文本和哈希电话号码。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 部分和将相应的命名空间分别用于纯文本和经过哈希处理的电子邮件地址。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| extern_id | 自定义用户ID | 如果源标识是自定义命名空间，请选择此目标标识。 |

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出区段（受众）的所有成员，以及Facebook目标中使用的标识符（名称、电话号码或其他）。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Facebook帐户先决条件 {#facebook-account-prerequisites}

在将受众区段发送到 [!DNL Facebook]，请确保满足以下要求：

* 您的 [!DNL Facebook] 用户帐户必须具有 **[!DNL Manage campaigns]** 为您计划使用的广告帐户启用的权限。
* 的 **Adobe Experience Cloud** 业务帐户必须作为广告合作伙伴添加到您的 [!DNL Facebook Ad Account]. 使用 `business ID=206617933627973`. 请参阅 [将合作伙伴添加到您的业务经理](https://www.facebook.com/business/help/1717412048538897) (在Facebook文档中)。
   >[!IMPORTANT]
   >
   > 配置Adobe Experience Cloud的权限时，必须启用 **管理营销活动** 权限。 需要权限才能 [!DNL Adobe Experience Platform] 集成。
* 阅读并签署 [!DNL Facebook Custom Audiences] 服务条款。 要执行此操作，请转到 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是 [!DNL Facebook Ad Account ID].
   >[!IMPORTANT]
   >
   >签署 [!DNL Facebook Custom Audiences] 服务条款，请确保使用您在Facebook API中进行身份验证时使用的相同用户帐户。

## ID匹配要求 {#id-matching-requirements}

[!DNL Facebook] 要求不要发送任何个人身份信息(PII)。 因此，激活的受众 [!DNL Facebook] 可以锁上 *哈希* 标识符，如电子邮件地址或电话号码。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵循其相应要求。

## 电话号码哈希处理要求 {#phone-number-hashing-requirements}

在中激活电话号码的方法有两种 [!DNL Facebook]:

* **摄取原始电话号码**:您可以在 [!DNL E.164] 格式到 [!DNL Platform]. 激活后，它们会自动进行哈希处理。 如果选择此选项，请确保始终将原始电话号码摄取到 `Phone_E.164` 命名空间。
* **摄取经过哈希处理的电话号码**:您可以在将电话号码摄取到 [!DNL Platform]. 如果选择此选项，请确保始终将经过哈希处理的电话号码摄取到 `Phone_SHA256` 命名空间。

>[!NOTE]
>
>摄取到的电话号码 `Phone` 命名空间无法在中激活 [!DNL Facebook].

## 电子邮件哈希处理要求 {#email-hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或者在Experience Platform中明确使用电子邮件地址，并且 [!DNL Platform] 在激活时对它们进行哈希处理。

要了解如何在Experience Platform中摄取电子邮件地址，请参阅 [批量摄取概述](/help/ingestion/batch-ingestion/overview.md) 和 [流摄取概述](/help/ingestion/streaming-ingestion/overview.md).

如果您选择自行对电子邮件地址进行哈希处理，请确保符合以下要求：

* 从电子邮件字符串中裁切所有前导和尾随空格；示例： `johndoe@example.com`，否 `<space>johndoe@example.com<space>`;
* 对电子邮件字符串进行哈希处理时，请确保对小写字符串进行哈希处理；
   * 示例： `example@email.com`，否 `EXAMPLE@EMAIL.COM`;
* 确保经过哈希处理的字符串全部为小写
   * 示例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，否 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 不要加盐。

>[!NOTE]
>
>来自未哈希命名空间的数据将由自动进行哈希处理 [!DNL Platform] 激活时。
> 属性源数据不会自动进行哈希处理。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。
> 的 **[!UICONTROL 应用转换]** 选择属性作为源字段时，才会显示选项。 选择命名空间时，不会显示该参数。

![身份映射转换](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 使用自定义命名空间 {#custom-namespaces}

在使用 `Extern_ID` 将数据发送到的命名空间 [!DNL Facebook]，请确保使用 [!DNL Facebook Pixel]. 请参阅 [Facebook官方文档](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) 以了解详细信息。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

以下视频还演示了配置 [!DNL Facebook] 目标和激活区段。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform用户界面经常更新，自此视频录制以来可能已发生更改。 有关最新信息，请参阅 [目标配置教程](../../ui/connect-destination.md).

### 对目标进行身份验证 {#authenticate}

1. 在目标目录中找到Facebook目标，然后选择 **[!UICONTROL 设置]**.
2. 选择 **[!UICONTROL 连接到目标]**.
   ![验证Facebook](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. 输入Facebook凭据并选择 **登录**.

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="帐户 ID"
>abstract="您的Facebook广告帐户ID。 您可以在Facebook广告管理器帐户中找到此ID。 输入此ID时，应始终为其添加前缀 `act_`."

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的 [!DNL Facebook Ad Account ID]. 您可以在 [!DNL Facebook Ads Manager] 帐户。 输入此ID时，应始终为其添加前缀 `act_`.

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="受众来源"
>abstract="选择区段中客户数据的最初收集方式。 当区段定向用户时，数据将显示在Facebook中"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="受众来源"
>abstract="广告商直接从客户那里收集数据。"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="受众来源"
>abstract="广告商直接从其合作伙伴那里收集数据。"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="受众来源"
>abstract="广告商直接从其客户和合作伙伴那里收集数据。"

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

在 **[!UICONTROL 区段计划]** 步骤，您必须提供 [!UICONTROL 受众来源] 将区段发送到 [!DNL Facebook Custom Audiences].

![Facebook受众来源](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### 映射示例：激活受众数据 [!DNL Facebook Custom Audience] {#example-facebook}

以下是在中激活受众数据时正确映射身份的示例 [!DNL Facebook Custom Audience].

选择源字段：

* 选择 `Email` 命名空间作为源标识，前提是您使用的电子邮件地址未经过哈希处理。
* 选择 `Email_LC_SHA256` 命名空间作为源标识(如果您在数据摄取时将客户电子邮件地址哈希到 [!DNL Platform]，根据 [!DNL Facebook] [电子邮件哈希处理要求](#email-hashing-requirements).
* 选择 `PHONE_E.164` 命名空间作为源标识（如果您的数据包含非哈希电话号码）。 [!DNL Platform] 将用哈希处理电话号码以符合 [!DNL Facebook] 要求。
* 选择 `Phone_SHA256` 命名空间作为源标识(如果您在数据摄取时将电话号码哈希到 [!DNL Platform]，根据 [!DNL Facebook] [电话号码哈希要求](#phone-number-hashing-requirements).
* 选择 `IDFA` 命名空间作为源标识（如果数据包含） [!DNL Apple] 设备ID。
* 选择 `GAID` 命名空间作为源标识（如果数据包含） [!DNL Android] 设备ID。
* 选择 `Custom` 命名空间作为源标识（如果您的数据包含其他类型的标识符）。

选择目标字段：

* 选择 `Email_LC_SHA256` 源命名空间为目标标识的命名空间 `Email` 或 `Email_LC_SHA256`.
* 选择 `Phone_SHA256` 源命名空间为目标标识的命名空间 `PHONE_E.164` 或 `Phone_SHA256`.
* 选择 `IDFA` 或 `GAID` 源命名空间时，命名空间会作为目标标识 `IDFA` 或 `GAID`.
* 选择 `Extern_ID` 命名空间作为目标标识的命名空间。

>[!IMPORTANT]
>
>来自未哈希命名空间的数据将由自动进行哈希处理 [!DNL Platform] 激活时。
> 
>属性源数据不会自动进行哈希处理。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。

![身份映射](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 导出的数据 {#exported-data}

对于 [!DNL Facebook]，则成功激活表示 [!DNL Facebook] 自定义受众将在 [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). 由于用户符合激活区段的资格条件或被取消资格，因此将会添加和删除受众中的区段成员资格。

>[!TIP]
>
>Adobe Experience Platform与 [!DNL Facebook] 支持历史受众回填。 所有历史区段资格都将发送到 [!DNL Facebook] 在您将区段激活到目标时。

## 故障排除 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

当客户使用新创建的帐户，并且 [!DNL Facebook] 权限尚未激活。

如果您收到 `400 Bad Request` 执行 [Facebook帐户先决条件](#facebook-account-prerequisites)，请为 [!DNL Facebook] 权限生效。
