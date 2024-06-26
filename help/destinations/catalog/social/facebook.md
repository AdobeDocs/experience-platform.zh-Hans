---
keywords: facebook连接；facebook连接；facebook目标；facebook；instagram；messenger；facebook messenger
title: facebook连接
description: 根据哈希电子邮件激活Facebook营销活动的配置文件，以实现受众定位、个性化和抑制。
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 7%

---

# [!DNL Facebook] 连接

## 概述 {#overview}

激活您的配置文件 [!DNL Facebook] 基于哈希电子邮件的受众定位、个性化和抑制营销活动。

您可以将此目标用于中的受众定位 [!DNL Facebook's] 支持的应用程序系列 [!DNL Custom Audiences]，包括 [!DNL Facebook]， [!DNL Instagram]， [!DNL Audience Network]、和 [!DNL Messenger]. [!DNL Facebook Ads Manager] 中的版面级别会显示您要针对其运行营销活动的所选应用程序。

![Adobe Experience Platform UI中的Facebook目标。](../../assets/catalog/social/facebook/catalog.png)

## 用例

为了帮助您更好地了解如何以及何时使用 [!DNL Facebook] 目标，以下是Adobe Experience Platform客户可以使用此功能解决的两个示例用例。

### 用例#1

在线零售商希望通过社交平台与现有客户联系，并向他们显示基于先前订单的个性化优惠。 在线零售商可以将他们自己的CRM中的电子邮件地址摄取到Adobe Experience Platform，从他们自己的离线数据构建受众，并将这些受众发送到 [!DNL Facebook] 社交平台，优化广告支出。

### 用例#2

航空公司有不同的客户层（青铜、银牌和金牌），并希望通过社交平台为每个层提供个性化优惠。 然而，并非所有客户都使用马航的移动应用，其中一些客户尚未登录该公司网站。 公司拥有的关于这些客户的唯一标识符是会员ID和电子邮件地址。

要通过社交媒体定位他们，他们可以使用电子邮件地址作为标识符，将客户数据从其CRM载入到Adobe Experience Platform中。

接下来，他们可以使用离线数据（包括关联的会员ID和客户层）构建新的受众，他们可以通过 [!DNL Facebook] 目标。

## 支持的身份 {#supported-identities}

[!DNL Facebook Custom Audiences] 支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service/features/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| phone_sha256 | 使用SHA256算法散列的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 请按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 部分并使用相应的命名空间分别用于纯文本和经过哈希处理的电话号码。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 请按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 部分，并分别将相应的命名空间用于纯文本和经过哈希处理的电子邮件地址。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |
| extern_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有Facebook目标中所用标识符（姓名、电话号码或其他）的受众所有成员。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## facebook帐户先决条件 {#facebook-account-prerequisites}

在将受众发送至 [!DNL Facebook]，确保您满足以下要求：

* 您的 [!DNL Facebook] 用户帐户必须具有对 [!DNL Facebook Business Account] 拥有您使用的广告帐户。
* 您的 [!DNL Facebook] 用户帐户必须具有 **[!DNL Manage campaigns]** 为您计划使用的Ad帐户启用的权限。
* 此 **Adobe Experience Cloud** 必须将商业帐户作为广告合作伙伴添加到您的 [!DNL Facebook Ad Account]. 使用 `business ID=206617933627973`。请参阅 [将合作伙伴添加到您的业务经理](https://www.facebook.com/business/help/1717412048538897) 有关详细信息，请参阅Facebook文档。
  >[!IMPORTANT]
  >
  > 配置Adobe Experience Cloud的权限时，必须启用 **管理营销活动** 许可。 以下各项需要权限： [!DNL Adobe Experience Platform] 集成。
* 阅读并签署 [!DNL Facebook Custom Audiences] 服务条款。 要执行此操作，请转到 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID].
  >[!IMPORTANT]
  >
  >签名时 [!DNL Facebook Custom Audiences] 服务条款，确保使用您在Facebook API中用于进行身份验证的相同用户帐户。

## ID匹配要求 {#id-matching-requirements}

[!DNL Facebook] 要求不发送明确的个人身份信息(PII)。 因此，受众激活到 [!DNL Facebook] 可以中断连接 *哈希* 标识符，例如电子邮件地址或电话号码。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵守其相应的要求。

## 电话号码散列要求 {#phone-number-hashing-requirements}

激活中的电话号码有两种方法 [!DNL Facebook]：

* **摄取原始电话号码**：您可以摄取中的原始电话号码 [!DNL E.164] 格式化为 [!DNL Platform]. 它们在激活时自动进行哈希处理。 如果选择此选项，请确保始终将原始电话号码摄取到 `Phone_E.164` 命名空间。
* **摄取经过哈希处理的电话号码**：您可以在将其引入之前预散列电话号码 [!DNL Platform]. 如果选择此选项，请确保始终将经过哈希处理的电话号码摄取到 `Phone_SHA256` 命名空间。

>[!NOTE]
>
>电话号码已引入 `Phone` 命名空间不能在中激活 [!DNL Facebook].

## 电子邮件哈希处理要求 {#email-hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或者在Experience Platform中使用清晰的电子邮件地址，并且您可以 [!DNL Platform] 激活时对其进行哈希处理。

要了解如何在Experience Platform中引入电子邮件地址，请参阅 [批量摄取概述](/help/ingestion/batch-ingestion/overview.md) 和 [流式摄取概述](/help/ingestion/streaming-ingestion/overview.md).

如果选择自己对电子邮件地址进行哈希处理，请确保符合以下要求：

* 修剪电子邮件字符串中的所有前导空格和尾随空格；示例： `johndoe@example.com`，不是 `<space>johndoe@example.com<space>`；
* 在对电子邮件字符串进行哈希处理时，请确保对小写字符串进行哈希处理；
   * 示例： `example@email.com`，不是 `EXAMPLE@EMAIL.COM`；
* 确保散列字符串全部为小写
   * 示例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，不是 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`；
* 不要把字串加盐。

>[!NOTE]
>
>来自未经过哈希处理的命名空间的数据自动进行哈希处理 [!DNL Platform] 激活时。
> 属性源数据不会自动进行哈希处理。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。
> 此 **[!UICONTROL 应用转换]** 选项仅在选择属性作为源字段时显示。 当您选择命名空间时，它不会显示。

![应用映射步骤中突出显示的转换控件。](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 使用自定义命名空间 {#custom-namespaces}

在使用 `Extern_ID` 要将数据发送到的命名空间 [!DNL Facebook]，确保使用同步您自己的标识符 [!DNL Facebook Pixel]. 请参阅 [facebook官方文档](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) 以了解详细信息。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

以下视频还演示了配置 [!DNL Facebook] 目标和激活受众。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform用户界面经常更新，自从录制此视频以来，该界面可能已发生更改。 有关最新信息，请参阅 [目标配置教程](../../ui/connect-destination.md).

### 验证目标 {#authenticate}

1. 在目标目录中找到Facebook目标并选择 **[!UICONTROL 设置]**.
2. 选择 **[!UICONTROL 连接到目标]**.
   ![对激活工作流中显示的Facebook步骤进行身份验证。](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. 输入您的Facebook凭据并选择 **登录**.

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="帐户 ID"
>abstract="您的 Facebook 广告帐户 ID。您可以在 Facebook 广告管理器帐户中找到此 ID。在输入此 ID 时，请始终为其添加前缀 `act_`。"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的 [!DNL Facebook Ad Account ID]. 您可以在您的网站中找到此ID [!DNL Facebook Ads Manager] 帐户。 在输入此 ID 时，请始终为其添加前缀 `act_`。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="受众来源"
>abstract="选择最初收集受众中的客户数据的方式。当用户被区段定位时，数据会显示在 Facebook 中"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="受众来源"
>abstract="广告商直接从客户那里收集数据。"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="受众来源"
>abstract="广告商直接从合作伙伴那里收集数据。"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="受众来源"
>abstract="广告商直接从客户和合作伙伴那里收集数据。"

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

请参阅 [将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

在 **[!UICONTROL 区段计划]** 步骤，您必须提供 [!UICONTROL 受众来源] 将受众发送至 [!DNL Facebook Custom Audiences].

![facebook激活步骤中显示的“受众来源”下拉列表。](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### 映射示例：激活中的受众数据 [!DNL Facebook Custom Audience] {#example-facebook}

下面是在中激活受众数据时正确标识映射的示例 [!DNL Facebook Custom Audience].

选择源字段：

* 选择 `Email` namespace作为源标识（如果您使用的电子邮件地址未经过哈希处理）。
* 选择 `Email_LC_SHA256` 作为源标识的命名空间（如果您在数据摄取时对客户电子邮件地址进行哈希处理） [!DNL Platform]，根据的 [!DNL Facebook] [电子邮件哈希处理要求](#email-hashing-requirements).
* 选择 `PHONE_E.164` namespace作为源标识（如果您的数据由非散列电话号码组成）。 [!DNL Platform] 将散列电话号码以符合 [!DNL Facebook] 要求。
* 选择 `Phone_SHA256` 作为源标识的命名空间(如果您在数据摄取时将数据散列到 [!DNL Platform]，根据的 [!DNL Facebook] [电话号码散列要求](#phone-number-hashing-requirements).
* 选择 `IDFA` 作为源标识的命名空间（如果您的数据包含） [!DNL Apple] 设备ID。
* 选择 `GAID` 作为源标识的命名空间（如果您的数据包含） [!DNL Android] 设备ID。
* 选择 `Custom` 作为源标识的命名空间（如果您的数据包含其他类型的标识符）。

选择目标字段：

* 选择 `Email_LC_SHA256` 当源命名空间满足以下任一条件时，将命名空间作为目标身份 `Email` 或 `Email_LC_SHA256`.
* 选择 `Phone_SHA256` 当源命名空间满足以下任一条件时，将命名空间作为目标身份 `PHONE_E.164` 或 `Phone_SHA256`.
* 选择 `IDFA` 或 `GAID` 当源命名空间满足以下条件时，命名空间作为目标身份 `IDFA` 或 `GAID`.
* 选择 `Extern_ID` 当源命名空间是自定义命名空间时，将命名空间作为目标身份。

>[!IMPORTANT]
>
>来自未经过哈希处理的命名空间的数据自动进行哈希处理 [!DNL Platform] 激活时。
> 
>属性源数据不会自动进行哈希处理。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。

![应用映射步骤中突出显示的转换控件。](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 导出的数据 {#exported-data}

对象 [!DNL Facebook]，成功激活意味着 [!DNL Facebook] 自定义受众将以编程方式创建于 [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). 由于用户符合或不符合激活受众的资格，因此将添加和删除受众成员资格。

>[!TIP]
>
>Adobe Experience Platform与之间的集成 [!DNL Facebook] 支持历史受众回填。 所有历史受众资格都将被发送到 [!DNL Facebook] 将受众激活到目标时。

## 故障排除 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

当客户使用新创建的帐户，并且 [!DNL Facebook] 权限尚未激活。

如果您收到 `400 Bad Request` 执行中的步骤后的错误消息 [facebook帐户先决条件](#facebook-account-prerequisites)，留出几天时间 [!DNL Facebook] 权限将生效。
