---
keywords: Google客户匹配；Google客户匹配；Google客户匹配
title: Google客户匹配连接
description: Google客户匹配允许您使用在线和离线数据，通过Google自有资产和运营资产(如搜索、购物、Gmail和YouTube)来联系客户并与其重新互动。
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 183aff5a3b6bcc1635ae7b4b0e503a9d4b6d4d31
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---

# [!DNL Google Customer Match] 连接

## 概述 {#overview}

[Google客户](https://support.google.com/google-ads/answer/6379332?hl=en) 匹配功能允许您使用在线和离线数据，通过Google自有和运营的资产来联系和重新吸引客户，例如： [!DNL Search]、  [!DNL Shopping]、  [!DNL Gmail]和 [!DNL YouTube]。

![Adobe Experience Platform UI中的Google客户匹配目标](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 用例

为了帮助您更好地了解如何以及何时使用[!DNL Google Customer Match]目标，以下是Adobe Experience Platform客户可以使用此功能解决的示例用例。

### 用例#1

运动服装品牌希望通过[!DNL Google Search]和[!DNL Google Shopping]联系现有客户，以根据其过去的购买和浏览历史个性化选件和项目。 服装品牌可以将电子邮件地址从自己的CRM摄取到Experience Platform，并根据自己的离线数据构建区段。 然后，他们可以将这些区段发送到[!DNL Google Customer Match]以用于[!DNL Search]和[!DNL Shopping]，从而优化其广告支出。

### 用例#2

一家知名科技公司推出了一款新手机。 为推广这款新型手机，他们希望将手机的新特性和功能提升到拥有其旧款手机的客户的认识。

要推广此版本，他们会将电子邮件地址从其CRM数据库上传到Experience Platform，并使用电子邮件地址作为标识符。 区段是根据拥有旧手机型号的客户创建的。 然后，区段会发送到[!DNL Google Customer Match]，以便公司可以定位当前客户、拥有旧手机型号的客户以及[!DNL YouTube]上的类似客户。

## [!DNL Google Customer Match]目标的数据管理 {#data-governance}

Experience Platform中的某些目标对于发送到目标平台或从目标平台接收的数据具有特定规则和义务。 您有责任了解数据的限制和义务，以及如何在Adobe Experience Platform和目标平台中使用该数据。 Adobe Experience Platform提供了数据管理工具，可帮助您管理其中一些数据使用义务。 [进一](../../../data-governance/labels/overview.md) 步了解数据管理工具和策略。

## 支持的身份 {#supported-identities}

[!DNL Google Customer Match] 支持激活下表所述的身份。了解有关[identities](/help/identity-service/namespaces.md)的更多信息。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 如果源标识是GAID命名空间，请选择此目标标识。 |
| IDFA | 适用于广告商的Apple ID | 如果源标识是IDFA命名空间，请选择此目标标识。 |
| phone_sha256_e.164 | E164格式的电话号码，使用SHA256算法进行哈希处理 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明，分别将相应的命名空间用于纯文本和经过哈希处理的电话号码。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明，分别对纯文本和经过哈希处理的电子邮件地址使用适当的命名空间。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |
| user_id | 自定义用户ID | 如果源标识是自定义命名空间，请选择此目标标识。 |

## 导出类型 {#export-type}

**区段导出**  — 您正在导出区段（受众）的所有成员，以及目标中使用的标识符（名称、电话号码和其他） [!DNL Google Customer Match] 。

## [!DNL Google Customer Match] 帐户先决条件 {#google-account-prerequisites}

在Experience Platform中设置[!DNL Google Customer Match]目标之前，请确保阅读并遵循Google关于使用[!DNL Customer Match]的策略，如[Google支持文档](https://support.google.com/google-ads/answer/6299717)中所述。

接下来，确保为[!DNL Standard]或更高访问级别配置了[!DNL Google]帐户。 有关详细信息，请参阅[Google Ads文档](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1)。

### 允许列表 {#allowlist}

在Experience Platform中创建[!DNL Google Customer Match]目标之前，请确保您的[!DNL Google Ads]帐户符合[Google客户匹配策略](https://support.google.com/google-ads/answer/6299717/customer-match-policy)。

具有合规帐户的客户会自动被Google允许列出。

## ID匹配要求 {#id-matching-requirements}

[!DNL Google] 要求不要发送任何个人身份信息(PII)。因此，激活到[!DNL Google Customer Match]的受众可以与&#x200B;*哈希*&#x200B;标识符（如电子邮件地址或电话号码）关联。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵循其相应要求。

## 电话号码哈希处理要求 {#phone-number-hashing-requirements}

在[!DNL Google Customer Match]中激活电话号码的方法有两种：

* **摄取原始电话号码**:您可以将格式的原始电话号码摄 [!DNL E.164] 入到中 [!DNL Platform]，激活后这些电话号码会自动进行哈希处理。如果选择此选项，请确保始终将原始电话号码摄取到`Phone_E.164`命名空间中。
* **摄取经过哈希处理的电话号码**:您可以在将电话号码摄取到中之前，对您的电话号码进行 [!DNL Platform]哈希处理。如果选择此选项，请确保始终将您经过哈希处理的电话号码摄取到`PHONE_SHA256_E.164`命名空间中。

>[!NOTE]
>
>无法在[!DNL Google Customer Match]中激活被摄取到`Phone`命名空间的电话号码。

## 电子邮件哈希处理要求 {#hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或在Experience Platform中明确使用电子邮件地址，并在激活时对它们进行[!DNL Platform]哈希处理。

有关Google哈希要求和其他激活限制的更多信息，请参阅Google文档中的以下部分：

* [[!DNL Customer Match] 具有电子邮件地址、地址或用户ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 注意事项](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [客户与电话号码匹配](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [与移动设备ID匹配的客户](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


要了解如何在Experience Platform中摄取电子邮件地址，请参阅[批量摄取概述](../../../ingestion/batch-ingestion/overview.md)和[流摄取概述](../../../ingestion/streaming-ingestion/overview.md)。

如果您选择自行对电子邮件地址进行哈希处理，请确保符合上面链接中所述的Google要求。

## 使用自定义命名空间 {#custom-namespaces}

在使用`User_ID`命名空间将数据发送到Google之前，请确保使用[!DNL gTag]同步您自己的标识符。 有关详细信息，请参阅[Google官方文档](https://support.google.com/google-ads/answer/9199250)。

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**:为此目标连接提供名称
* **[!UICONTROL 描述]**:提供此目标连接的描述
* **[!UICONTROL 帐户ID]**:您的Google客户客户ID。ID的格式为xxx-xxx-xxxx。

>[!IMPORTANT]
>
> * 默认情况下，**[!UICONTROL 与PII]**&#x200B;组合营销操作会为[!DNL Google Customer Match]目标选中，且无法删除。


## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请参阅[将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md)。

在&#x200B;**[!UICONTROL 区段计划]**&#x200B;步骤中，在向[!DNL Google Customer Match]发送[!DNL IDFA]或[!DNL GAID]区段时，必须提供[!UICONTROL 应用程序ID]。

![Google客户匹配应用程序ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

有关如何查找[!DNL App ID]的详细信息，请参阅[Google官方文档](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid)。

### 映射示例：在[!DNL Google Customer Match]中激活受众数据 {#example-gcm}

以下示例用于在[!DNL Google Customer Match]中激活受众数据时正确映射身份。

选择源字段：

* 如果您使用的电子邮件地址没有经过哈希处理，请选择`Email`命名空间作为源标识。
* 如果您根据[!DNL Google Customer Match] [电子邮件哈希处理要求](#hashing-requirements)对数据摄取时的客户电子邮件地址进行哈希处理，并将其转换为[!DNL Platform]，请选择`Email_LC_SHA256`命名空间作为源标识。
* 如果您的数据包含非哈希电话号码，请选择`PHONE_E.164`命名空间作为源标识。 [!DNL Platform] 将对电话号码进行哈希处理以符合 [!DNL Google Customer Match] 要求。
* 如果您根据[!DNL Facebook] [电话号码哈希处理要求](#phone-number-hashing-requirements)对数据摄取时的电话号码进行哈希处理，请选择`Phone_SHA256_E.164`命名空间作为源标识。[!DNL Platform]
* 如果您的数据包含[!DNL Apple]设备ID，请选择`IDFA`命名空间作为源标识。
* 如果您的数据包含[!DNL Android]设备ID，请选择`GAID`命名空间作为源标识。
* 如果您的数据包含其他类型的标识符，请选择`Custom`命名空间作为源标识。

选择目标字段：

* 当源命名空间为`Email`或`Email_LC_SHA256`时，选择`Email_LC_SHA256`命名空间作为目标标识。
* 当源命名空间为`PHONE_E.164`或`Phone_SHA256_E.164`时，选择`Phone_SHA256_E.164`命名空间作为目标标识。
* 当源命名空间为`IDFA`或`GAID`时，选择`IDFA`或`GAID`命名空间作为目标标识。
* 如果源命名空间是自定义命名空间，请选择`User_ID`命名空间作为目标标识。

![身份映射](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

未哈希命名空间中的数据在激活后由[!DNL Platform]自动进行哈希处理。

属性源数据不会自动进行哈希处理。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。

![身份映射转换](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## 验证区段激活是否成功 {#verify-activation}

完成激活流程后，切换到您的&#x200B;**[!UICONTROL Google Ads]**&#x200B;帐户。 激活的区段将作为客户列表显示在您的Google帐户中。 请注意，根据区段大小，某些受众不会填充，除非要提供的活动用户超过100个。

将区段同时映射到[!DNL IDFA]和[!DNL GAID]移动ID时， [!DNL Google Customer Match]会为每个ID映射创建一个单独的区段。 您的[!DNL Google Ads]帐户显示两个不同的区段，一个用于[!DNL IDFA]，另一个用于[!DNL GAID]映射。

## 额外资源 {#additional-resources}

* [集成Google客户匹配 — 视频教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)
