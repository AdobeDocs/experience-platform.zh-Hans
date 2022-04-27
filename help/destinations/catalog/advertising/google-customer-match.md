---
keywords: google客户匹配；Google客户匹配；Google客户匹配
title: Google客户匹配连接
description: Google客户匹配允许您使用在线和离线数据，通过Google拥有和运营的资产(如搜索、购物、Gmail和YouTube)来访问客户并与其重新互动。
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 1%

---

# [!DNL Google Customer Match] 连接

## 概述 {#overview}

[Google客户匹配](https://support.google.com/google-ads/answer/6379332?hl=en) 允许您使用在线和离线数据，跨Google拥有和运营的资产访问客户并与其重新互动，例如： [!DNL Search], [!DNL Shopping], [!DNL Gmail]和 [!DNL YouTube].

![GoogleAdobe Experience Platform UI中的“客户匹配”目标](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 用例 {#use-cases}

以帮助您更好地了解如何以及何时使用 [!DNL Google Customer Match] 目标中，以下是Adobe Experience Platform客户可以使用此功能解决的示例用例。

### 用例#1

运动服装品牌希望通过 [!DNL Google Search] 和 [!DNL Google Shopping] 以根据过去的购买和浏览历史记录对选件和项目进行个性化。 服装品牌可以将电子邮件地址从自己的CRM摄取到Experience Platform，并根据自己的离线数据构建区段。 然后，他们可以将这些区段发送到 [!DNL Google Customer Match] 用于 [!DNL Search] 和 [!DNL Shopping]，优化广告支出。

### 用例#2

一家知名科技公司推出了一款新手机。 为推广这款新型手机，他们希望将手机的新特性和功能提升到拥有其旧款手机的客户的认识。

要推广此版本，他们会将电子邮件地址从其CRM数据库上传到Experience Platform，并使用电子邮件地址作为标识符。 区段是根据拥有旧手机型号的客户创建的。 然后，区段会被发送到 [!DNL Google Customer Match]，以便公司可以定位当前客户、拥有旧手机型号的客户以及 [!DNL YouTube].

## 的数据管理 [!DNL Google Customer Match] 目标 {#data-governance}

Experience Platform中的某些目标对于发送到目标平台或从目标平台接收的数据具有特定规则和义务。 您有责任了解数据的限制和义务，以及如何在Adobe Experience Platform和目标平台中使用该数据。 Adobe Experience Platform提供了数据管理工具，可帮助您管理其中一些数据使用义务。 [了解更多](../../../data-governance/labels/overview.md) 关于数据管理工具和政策。

## 支持的身份 {#supported-identities}

[!DNL Google Customer Match] 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google Advertising ID | 如果源标识是GAID命名空间，请选择此目标标识。 |
| IDFA | Apple ID for Advertisers | 如果源标识是IDFA命名空间，请选择此目标标识。 |
| phone_sha256_e.164 | E164格式的电话号码，使用SHA256算法进行哈希处理 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 部分和将相应的命名空间分别用于纯文本和哈希电话号码。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 部分和将相应的命名空间分别用于纯文本和经过哈希处理的电子邮件地址。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| user_id | 自定义用户ID | 如果源标识是自定义命名空间，请选择此目标标识。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，以及 [!DNL Google Customer Match] 目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## [!DNL Google Customer Match] 帐户先决条件 {#google-account-prerequisites}

在设置 [!DNL Google Customer Match] 目标Experience Platform中，请确保阅读并遵循Google的使用策略 [!DNL Customer Match]，在 [Google支持文档](https://support.google.com/google-ads/answer/6299717).

接下来，确保您的 [!DNL Google] 为 [!DNL Standard] 或更高的权限级别。 请参阅 [Google Ads文档](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 以了解详细信息。

### 允许列表 {#allowlist}

在创建 [!DNL Google Customer Match] 目标Experience Platform，请确保 [!DNL Google Ads] 账户符合 [Google客户匹配策略](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

具有合规帐户的客户会自动允许由Google列出。

## ID匹配要求 {#id-matching-requirements}

[!DNL Google] 要求不要发送任何个人身份信息(PII)。 因此，激活的受众 [!DNL Google Customer Match] 可以锁上 *哈希* 标识符，如电子邮件地址或电话号码。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵循其相应要求。

### 电话号码哈希处理要求 {#phone-number-hashing-requirements}

在中激活电话号码的方法有两种 [!DNL Google Customer Match]:

* **摄取原始电话号码**:您可以在 [!DNL E.164] 格式到 [!DNL Platform]，且在激活时会自动对其进行哈希处理。 如果选择此选项，请确保始终将原始电话号码摄取到 `Phone_E.164` 命名空间。
* **摄取经过哈希处理的电话号码**:您可以在将电话号码摄取到 [!DNL Platform]. 如果选择此选项，请确保始终将经过哈希处理的电话号码摄取到 `PHONE_SHA256_E.164` 命名空间。

>[!NOTE]
>
>摄取到的电话号码 `Phone` 命名空间无法在中激活 [!DNL Google Customer Match].

### 电子邮件哈希处理要求 {#hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或者在Experience Platform中明确使用电子邮件地址，并且 [!DNL Platform] 在激活时对它们进行哈希处理。

有关Google的哈希处理要求和其他激活限制的更多信息，请参阅Google文档中的以下部分：

* [[!DNL Customer Match] 具有电子邮件地址、地址或用户ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 注意事项](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [客户与电话号码匹配](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [与移动设备ID匹配的客户](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


要了解如何在Experience Platform中摄取电子邮件地址，请参阅 [批量摄取概述](../../../ingestion/batch-ingestion/overview.md) 和 [流摄取概述](../../../ingestion/streaming-ingestion/overview.md).

如果您选择自行对电子邮件地址进行哈希处理，请确保符合上面链接中所述的Google要求。

### 使用自定义命名空间 {#custom-namespaces}

在使用 `User_ID` 将数据发送到Google的命名空间，请确保使用 [!DNL gTag]. 请参阅 [Google官方文档](https://support.google.com/google-ads/answer/9199250) 以了解详细信息。

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:为此目标连接提供名称
* **[!UICONTROL 描述]**:提供此目标连接的描述
* **[!UICONTROL 帐户ID]**:您的Google客户客户ID。 ID的格式为xxx-xxx-xxxx。

>[!IMPORTANT]
>
> * 的 **[!UICONTROL 与PII组合]** 默认情况下，会为 [!DNL Google Customer Match] 目标，无法删除。


## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

在 **[!UICONTROL 区段计划]** 步骤，您必须提供 [!UICONTROL 应用程序ID] 发送 [!DNL IDFA] 或 [!DNL GAID] 区段至 [!DNL Google Customer Match].

![Google客户匹配应用程序ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

有关如何查找 [!DNL App ID]，请参阅 [Google官方文档](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### 映射示例：激活受众数据 [!DNL Google Customer Match] {#example-gcm}

以下是在中激活受众数据时正确映射身份的示例 [!DNL Google Customer Match].

选择源字段：

* 选择 `Email` 命名空间作为源标识，前提是您使用的电子邮件地址未经过哈希处理。
* 选择 `Email_LC_SHA256` 命名空间作为源标识(如果您在数据摄取时将客户电子邮件地址哈希到 [!DNL Platform]，根据 [!DNL Google Customer Match] [电子邮件哈希处理要求](#hashing-requirements).
* 选择 `PHONE_E.164` 命名空间作为源标识（如果您的数据包含非哈希电话号码）。 [!DNL Platform] 将用哈希处理电话号码以符合 [!DNL Google Customer Match] 要求。
* 选择 `Phone_SHA256_E.164` 命名空间作为源标识(如果您在数据摄取时将电话号码哈希到 [!DNL Platform]，根据 [!DNL Facebook] [电话号码哈希要求](#phone-number-hashing-requirements).
* 选择 `IDFA` 命名空间作为源标识（如果数据包含） [!DNL Apple] 设备ID。
* 选择 `GAID` 命名空间作为源标识（如果数据包含） [!DNL Android] 设备ID。
* 选择 `Custom` 命名空间作为源标识（如果您的数据包含其他类型的标识符）。

选择目标字段：

* 选择 `Email_LC_SHA256` 源命名空间为目标标识的命名空间 `Email` 或 `Email_LC_SHA256`.
* 选择 `Phone_SHA256_E.164` 源命名空间为目标标识的命名空间 `PHONE_E.164` 或 `Phone_SHA256_E.164`.
* 选择 `IDFA` 或 `GAID` 源命名空间时，命名空间会作为目标标识 `IDFA` 或 `GAID`.
* 选择 `User_ID` 命名空间作为目标标识的命名空间。

![身份映射](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

来自未哈希命名空间的数据将由自动进行哈希处理 [!DNL Platform] 激活时。

属性源数据不会自动进行哈希处理。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。

![身份映射转换](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## 验证区段激活是否成功 {#verify-activation}

完成激活流程后，切换到 **[!UICONTROL Google Ads]** 帐户。 激活的区段以客户列表的形式显示在您的Google帐户中。 请注意，根据区段大小，某些受众不会填充，除非要提供的活动用户超过100个。

将区段映射到 [!DNL IDFA] 和 [!DNL GAID] 移动ID、 [!DNL Google Customer Match] 为每个ID映射创建单独的区段。 您的 [!DNL Google Ads] 帐户会显示两个不同的区段，一个用于 [!DNL IDFA]，一个用于 [!DNL GAID] 映射。

## 故障排除 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

当客户帐户与 [先决条件](#google-account-prerequisites). 要解决此问题，请联系Google，并确保您的帐户已列入允许列表，且已为 [!DNL Standard] 或更高的权限级别。 请参阅 [Google Ads文档](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 以了解详细信息。

## 其他资源 {#additional-resources}

* [集成Google客户匹配 — 视频教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

