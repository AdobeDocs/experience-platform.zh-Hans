---
keywords: facebook连接；facebook连接；facebook目标；facebook；instagram；messenger；facebook messenger
title: Facebook连接
description: 根据散列邮件激活 Facebook 营销活动的轮廓，以实现受众定位、个性化和抑制。
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: c8eedc1f020b8605c9565015461cb1dfd47bba1f
workflow-type: tm+mt
source-wordcount: '2690'
ht-degree: 5%

---

# [!DNL Facebook]连接

## 概述 {#overview}

根据哈希电子邮件激活[!DNL Facebook]营销活动的配置文件，以实现受众定位、个性化和抑制。

您可以将此目标用于[!DNL Facebook's]支持的[!DNL Custom Audiences]系列应用中的受众定位，包括[!DNL Facebook]、[!DNL Instagram]、[!DNL Audience Network]和[!DNL Messenger]。 [!DNL Facebook Ads Manager]中的版面级别显示您要针对其运行营销活动的所选应用程序。

Adobe Experience Platform UI中的![Facebook目标。](../../assets/catalog/social/facebook/catalog.png)

## 用例

为了帮助您更好地了解如何使用[!DNL Facebook]目标以及何时使用，以下是Adobe Experience Platform客户可以使用此功能解决的两个示例用例。

### 用例#1

在线retailer希望通过社交平台与现有客户联系，并向他们显示基于先前订单的个性化优惠。 在线retailer可将他们自己的CRM中的电子邮件地址摄取到Adobe Experience Platform，从他们自己的离线数据中构建受众，并将这些受众发送到[!DNL Facebook]社交平台，从而优化他们的广告支出。

### 用例#2

航空公司有不同的客户层（青铜、银牌和金牌），并希望通过社交平台为每个层提供个性化优惠。 然而，并非所有客户都使用马航的移动应用，其中一些客户尚未登录该公司网站。 公司拥有的关于这些客户的唯一标识符是会员ID和电子邮件地址。

要通过社交媒体定位他们，他们可以使用电子邮件地址作为标识符，将客户数据从其CRM载入到Adobe Experience Platform中。

接下来，他们可以使用离线数据（包括关联的会员ID和客户层）构建新的受众，可以通过[!DNL Facebook]目标定位这些受众。

## 支持的身份 {#supported-identities}

[!DNL Facebook Custom Audiences]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| `GAID` | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| `IDFA` | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| `phone_sha256` | 使用SHA256算法散列的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明进行操作，并分别使用适当的命名空间作为纯文本和经过哈希处理的电话号码。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `email_lc_sha256` | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明进行操作，并分别使用适当的命名空间作为纯文本和经过哈希处理的电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |
| `extern_id` | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |
| `gender` | 性别 | 接受的值： <ul><li>男性`m`</li><li>女性`f`</li></ul> Experience Platform **在将此值发送到Facebook之前会自动对其进行哈希处理**。 这种自动哈希处理是遵守Facebook安全和隐私要求所必需的。 请&#x200B;**不**&#x200B;为此字段提供预哈希值，因为这将导致匹配过程失败。 |
| `date_of_birth` | 出生日期 | 接受的格式： `yyyy-MM-DD`。 <br>Experience Platform **在将此值发送到Facebook之前会自动对其进行哈希处理**。 这种自动哈希处理是遵守Facebook安全和隐私要求所必需的。 请&#x200B;**不**&#x200B;为此字段提供预哈希值，因为这将导致匹配过程失败。 |
| `last_name` | 姓氏 | 接受的格式：小写，仅`a-z`个字符，无标点。 对特殊字符使用UTF-8编码。  <br>Experience Platform **在将此值发送到Facebook之前会自动对其进行哈希处理**。 这种自动哈希处理是遵守Facebook安全和隐私要求所必需的。 请&#x200B;**不**&#x200B;为此字段提供预哈希值，因为这将导致匹配过程失败。 |
| `first_name` | 名字 | 接受的格式：小写，仅`a-z`个字符，无标点，无空格。 对特殊字符使用UTF-8编码。  <br>Experience Platform **在将此值发送到Facebook之前会自动对其进行哈希处理**。 这种自动哈希处理是遵守Facebook安全和隐私要求所必需的。 请&#x200B;**不**&#x200B;为此字段提供预哈希值，因为这将导致匹配过程失败。 |
| `first_name_initial` | 名字首字母缩写 | 接受的格式：小写，仅`a-z`个字符。 对特殊字符使用UTF-8编码。  <br>Experience Platform **在将此值发送到Facebook之前会自动对其进行哈希处理**。 这种自动哈希处理是遵守Facebook安全和隐私要求所必需的。 请&#x200B;**不**&#x200B;为此字段提供预哈希值，因为这将导致匹配过程失败。 |
| `state` | State | 使用小写的[2字符ANSI缩写代码](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standard_state_code)。 对于非美国州，请使用小写字符、无标点、无特殊字符和空格。  <br>Experience Platform **在将此值发送到Facebook之前会自动对其进行哈希处理**。 这种自动哈希处理是遵守Facebook安全和隐私要求所必需的。 请&#x200B;**不**&#x200B;为此字段提供预哈希值，因为这将导致匹配过程失败。 |
| `city` | 城市 | 接受的格式：小写、仅`a-z`个字符、无标点、无特殊字符、无空格。  <br>Experience Platform **在将此值发送到Facebook之前会自动对其进行哈希处理**。 这种自动哈希处理是遵守Facebook安全和隐私要求所必需的。 请&#x200B;**不**&#x200B;为此字段提供预哈希值，因为这将导致匹配过程失败。 |
| `zip` | 邮政编码 | 接受的格式：小写，无空格。 对于美国邮政编码，仅使用前5位。 在英国，请使用`Area/District/Sector`格式。  <br>Experience Platform **在将此值发送到Facebook之前会自动对其进行哈希处理**。 这种自动哈希处理是遵守Facebook安全和隐私要求所必需的。 请&#x200B;**不**&#x200B;为此字段提供预哈希值，因为这将导致匹配过程失败。 |
| `country` | 国家/地区 | 接受的格式：小写，2字母国家/地区代码，采用[ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)格式。  <br>Experience Platform **在将此值发送到Facebook之前会自动对其进行哈希处理**。 这种自动哈希处理是遵守Facebook安全和隐私要求所必需的。 请&#x200B;**不**&#x200B;为此字段提供预哈希值，因为这将导致匹配过程失败。 |

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
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有Facebook目标中所用标识符（姓名、电话号码或其他）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## Facebook帐户先决条件 {#facebook-account-prerequisites}

在将受众发送到[!DNL Facebook]之前，请确保您满足以下要求：

* 您的[!DNL Facebook]用户帐户必须具有对拥有您正在使用的广告帐户的[!DNL Facebook Business Account]的完全访问权限。
* 您的[!DNL Facebook]用户帐户必须为计划使用的广告帐户启用&#x200B;**[!DNL Manage campaigns]**&#x200B;权限。
* **Adobe Experience Cloud**&#x200B;商业帐户必须添加为您[!DNL Facebook Ad Account]中的广告合作伙伴。 使用`business ID=206617933627973`。 有关详细信息，请参阅Facebook文档中的[将合作伙伴添加到业务管理器](https://www.facebook.com/business/help/1717412048538897)。

  >[!IMPORTANT]
  >
  > 配置Adobe Experience Cloud的权限时，必须启用&#x200B;**管理营销活动**&#x200B;权限。 [!DNL Adobe Experience Platform]集成需要权限。

* 阅读并签署[!DNL Facebook Custom Audiences]服务条款。 为此，请转到`https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]&business_id=206617933627973`，其中`accountID`是您的[!DNL Facebook Ad Account ID]。 签署服务条款时，确保URL中存在`business_id=206617933627973`部分。

  >[!IMPORTANT]
  >
  >签署[!DNL Facebook Custom Audiences]服务条款时，请确保使用您在Facebook API中用于进行身份验证的相同用户帐户。

## ID匹配要求 {#id-matching-requirements}

[!DNL Facebook]要求不发送明确的个人身份信息(PII)。 因此，激活到[!DNL Facebook]的受众可以用&#x200B;*散列的*&#x200B;标识符作为键值，例如电子邮件地址或电话号码。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵守其相应的要求。

## 最大化受众匹配率 {#match-rates}

若要在[!DNL Facebook]中实现最高的受众匹配率，强烈建议使用`phone_sha256`和`email_lc_sha256`目标身份。

这些标识符是[!DNL Facebook]用于在其平台上匹配受众的主要标识符。 请确保您的源数据正确映射到这些目标身份并遵循[!DNL Facebook's]哈希要求。

## 电话号码散列要求 {#phone-number-hashing-requirements}

在[!DNL Facebook]中激活电话号码的方法有两种：

* **正在摄取原始电话号码**：您可以将[!DNL E.164]格式的原始电话号码摄取到[!DNL Experience Platform]。 它们在激活时自动进行哈希处理。 如果选择此选项，请确保始终将原始电话号码摄取到`Phone_E.164`命名空间。
* **正在引入经过哈希处理的电话号码**：您可以在引入到[!DNL Experience Platform]之前对电话号码进行预哈希处理。 如果选择此选项，请确保始终将经过哈希处理的电话号码摄取到`Phone_SHA256`命名空间。

>[!NOTE]
>
>无法在`Phone`中激活摄取到[!DNL Facebook]命名空间中的电话号码。

## 电子邮件哈希处理要求 {#email-hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或者在Experience Platform中明确使用电子邮件地址，并在激活时对其进行[!DNL Experience Platform]哈希处理。

要了解如何在Experience Platform中摄取电子邮件地址，请参阅[批次摄取概述](/help/ingestion/batch-ingestion/overview.md)和[流式摄取概述](/help/ingestion/streaming-ingestion/overview.md)。

如果选择自己对电子邮件地址进行哈希处理，请确保符合以下要求：

* 从电子邮件字符串中修剪所有前导空格和尾随空格；示例： `johndoe@example.com`，而不是`<space>johndoe@example.com<space>`；
* 在对电子邮件字符串进行哈希处理时，请确保对小写字符串进行哈希处理；
   * 示例： `example@email.com`，而不是`EXAMPLE@EMAIL.COM`；
* 确保散列字符串全部为小写
   * 示例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，而不是`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`；
* 不要把字串加盐。

>[!NOTE]
>
>来自未经过哈希处理的命名空间的数据在激活时会由[!DNL Experience Platform]自动进行哈希处理。
>&#x200B;> 属性源数据不会自动进行哈希处理。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。
>&#x200B;> **[!UICONTROL 应用转换]**&#x200B;选项仅在您选择属性作为源字段时显示。 当您选择命名空间时，它不会显示。

![应用映射步骤中突出显示的转换控件。](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 使用自定义命名空间 {#custom-namespaces}

在使用`Extern_ID`命名空间将数据发送到[!DNL Facebook]之前，请确保使用[!DNL Facebook Pixel]同步您自己的标识符。 有关详细信息，请参阅[Facebook官方文档](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers)。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

以下视频还演示了配置[!DNL Facebook]目标和激活受众的步骤。

>[!VIDEO](https://video.tv.adobe.com/v/3411783/?quality=12&learn=on&captions=chi_hans)

>[!NOTE]
>
>Experience Platform用户界面经常更新，自从录制此视频以来，可能已经发生了变化。 有关最新信息，请参阅[目标配置教程](../../ui/connect-destination.md)。

### 验证目标 {#authenticate}

1. 在目标目录中查找Facebook目标，然后选择&#x200B;**[!UICONTROL 设置]**。
2. 选择&#x200B;**[!UICONTROL 连接到目标]**。
   ![对激活工作流中显示的Facebook步骤进行身份验证。](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. 输入您的Facebook凭据并选择&#x200B;**登录**。

### 刷新身份验证凭据 {#refresh-authentication-credentials}

Facebook身份验证令牌每60天过期一次。 令牌过期后，数据导出到目标的操作将停止。

您可以在&#x200B;**[!UICONTROL 帐户]**&#x200B;或&#x200B;**[[!UICONTROL 浏览]](../../ui/destinations-workspace.md#accounts)**&#x200B;选项卡中从&#x200B;**[[!UICONTROL 帐户到期日期]](../../ui/destinations-workspace.md#browse)**&#x200B;列监视令牌到期日期。

在“浏览”选项卡中![Facebook帐户令牌过期日期列](../../assets/catalog/social/facebook/account-expiration-browse.png)

在“帐户”选项卡中![Facebook帐户令牌过期日期列](../../assets/catalog/social/facebook/account-expiration-accounts.png)

要防止令牌过期导致激活数据流中断，请执行以下步骤以重新进行身份验证：

1. 导航到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 帐户]**
2. （可选）使用页面上的可用过滤器仅显示Facebook帐户。
   ![筛选以仅显示Facebook帐户](/help/destinations/assets/catalog/social/facebook/refresh-oauth-filters.png)
3. 选择要刷新的帐户，选择省略号并选择&#x200B;**[!UICONTROL 编辑详细信息]**。
   ![选择“编辑详细信息”控件](/help/destinations/assets/catalog/social/facebook/refresh-oauth-edit-details.png)
4. 在模式窗口中，选择&#x200B;**[!UICONTROL 重新连接OAuth]**&#x200B;并使用Facebook凭据重新进行身份验证。
   使用Reconnect OAuth选项的![模式窗口](/help/destinations/assets/catalog/social/facebook/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>您的身份验证凭据已刷新，其过期时间将重置为60天。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="帐户 ID"
>abstract="您的 Facebook 广告帐户 ID。您可以在 Facebook 广告管理器帐户中找到此 ID。在输入此 ID 时，请始终为其添加前缀 `act_`。"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的[!DNL Facebook Ad Account ID]。 您可以在您的[!DNL Facebook Ads Manager]帐户中找到此ID。 在输入此 ID 时，请始终为其添加前缀 `act_`。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

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
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

在&#x200B;**[!UICONTROL 区段计划]**&#x200B;步骤中，在向[!UICONTROL 发送受众时，必须提供]受众来源[!DNL Facebook Custom Audiences]。

![Facebook激活步骤中显示的“受众来源”下拉列表。](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### 映射示例：在[!DNL Facebook Custom Audience]中激活受众数据 {#example-facebook}

下面是在[!DNL Facebook Custom Audience]中激活受众数据时正确标识映射的示例。

选择源字段：

* 如果您使用的电子邮件地址未经过哈希处理，请选择`Email`命名空间作为源标识。
* 如果您根据`Email_LC_SHA256` [!DNL Experience Platform]电子邮件哈希处理要求[!DNL Facebook]将数据摄取到[时已将客户电子邮件地址哈希处理，请选择](#email-hashing-requirements)命名空间作为源标识。
* 如果您的数据由非散列电话号码组成，请选择`PHONE_E.164`命名空间作为源标识。 [!DNL Experience Platform]将散列电话号码以符合[!DNL Facebook]要求。
* 如果您根据`Phone_SHA256` [!DNL Experience Platform]电话号码散列要求[!DNL Facebook]将数据提取到[中时散列电话号码，请选择](#phone-number-hashing-requirements)命名空间作为源标识。
* 如果您的数据包含`IDFA`个设备ID，请选择[!DNL Apple]命名空间作为源标识。
* 如果您的数据包含`GAID`个设备ID，请选择[!DNL Android]命名空间作为源标识。
* 如果您的数据包含其他类型的标识符，请选择`Custom`命名空间作为源标识。

选择目标字段：

* 当源命名空间为`Email_LC_SHA256`或`Email`时，选择`Email_LC_SHA256`命名空间作为目标标识。
* 当源命名空间为`Phone_SHA256`或`PHONE_E.164`时，选择`Phone_SHA256`命名空间作为目标标识。
* 当源命名空间为`IDFA`或`GAID`时，选择`IDFA`或`GAID`命名空间作为目标标识。
* 当源命名空间是自定义命名空间时，选择`Extern_ID`命名空间作为目标身份。

>[!IMPORTANT]
>
>来自未经过哈希处理的命名空间的数据在激活时会由[!DNL Experience Platform]自动进行哈希处理。
> 
>属性源数据不会自动进行哈希处理。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。

![应用映射步骤中突出显示的转换控件。](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 导出的数据 {#exported-data}

对于[!DNL Facebook]，成功激活意味着将在[!DNL Facebook][[!DNL Facebook Ads Manager]中以编程方式创建](https://www.facebook.com/adsmanager/manage/)自定义受众。 由于用户符合或不符合激活受众的资格，因此将添加和删除受众成员资格。

>[!TIP]
>
>Adobe Experience Platform与[!DNL Facebook]之间的集成支持历史受众回填。 在将受众激活到目标时，所有历史受众资格都会发送到[!DNL Facebook]。

## 故障排除 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

当客户使用新创建的帐户，并且[!DNL Facebook]权限尚未处于活动状态时，会发生此错误。

>[!IMPORTANT]
>
>确保您接受[!DNL Facebook Custom Audience Terms of Service]下的`business ID 206617933627973`，如[帐户先决条件](#facebook-account-prerequisites)部分中的URL模板所示。

如果在执行`400 Bad Request`Facebook帐户先决条件[中的步骤后收到](#facebook-account-prerequisites)错误消息，请等几天时间，[!DNL Facebook]权限即可生效。


