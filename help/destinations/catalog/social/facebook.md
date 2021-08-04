---
keywords: facebook连接；facebook连接；facebook目标；facebook;instagram;Messenger;facebook Messenger
title: Facebook连接
description: 根据经过哈希处理的电子邮件，激活Facebook营销活动的用户档案以进行受众定位、个性化和抑制。
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 32da733eda61049738e87bce48978196a1fea96d
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 2%

---

# [!DNL Facebook] 连接

## 概述 {#overview}

激活[!DNL Facebook]营销活动的用户档案，以便根据经过哈希处理的电子邮件进行受众定位、个性化和抑制。

您可以使用此目标在[!DNL Facebook’s]系列应用程序（包括[!DNL Facebook]、[!DNL Instagram]、[!DNL Audience Network]和[!DNL Messenger]）中定位受众。 [!DNL Custom Audiences][!DNL Facebook Ads Manager] 中的版面级别会显示您要针对其运行营销活动的所选应用程序。

![FacebookAdobe Experience Platform UI中的目标](../../assets/catalog/social/facebook/catalog.png)

## 用例

为了帮助您更好地了解如何以及何时使用[!DNL Facebook]目标，以下是Adobe Experience Platform客户可以使用此功能解决的两个示例用例。

### 用例#1

一家在线零售商希望通过社交平台与现有客户联系，并根据其先前的订单向他们显示个性化优惠。 该在线零售商可以将电子邮件地址从自己的CRM摄取到Adobe Experience Platform，从自己的离线数据构建区段，并将这些区段发送到[!DNL Facebook]社交平台，从而优化其广告支出。

### 用例#2

一家航空公司拥有不同的客户层（Bronze、Silver和Gold），并希望通过社交平台为每个层提供个性化优惠。 但是，并非所有客户都使用航空公司的移动设备应用程序，其中一些客户尚未登录公司网站。 公司关于这些客户的唯一标识符是会员ID和电子邮件地址。

要在社交媒体中定位客户，他们可以将客户数据从CRM载入Adobe Experience Platform，并将电子邮件地址作为标识符。

接下来，他们可以使用离线数据（包括关联的会员ID和客户层）来构建新的受众区段，并通过[!DNL Facebook]目标进行定位。

## 支持的身份 {#supported-identities}

[!DNL Facebook Custom Audiences] 支持激活下表所述的身份。了解有关[identities](/help/identity-service/namespaces.md)的更多信息。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 如果源标识是GAID命名空间，请选择GAID目标标识。 |
| IDFA | 适用于广告商的Apple ID | 如果源标识是IDFA命名空间，请选择IDFA目标标识。 |
| phone_sha256 | 使用SHA256算法进行哈希处理的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明，分别将相应的命名空间用于纯文本和经过哈希处理的电话号码。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明，分别对纯文本和经过哈希处理的电子邮件地址使用适当的命名空间。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |
| extern_id | 自定义用户ID | 如果源标识是自定义命名空间，请选择此目标标识。 |

## 导出类型 {#export-type}

**区段导出**  — 您要导出区段（受众）的所有成员，以及Facebook目标中使用的标识符（名称、电话号码或其他）。

## Facebook帐户先决条件 {#facebook-account-prerequisites}

在将受众区段发送到[!DNL Facebook]之前，请确保满足以下要求：

- 您的[!DNL Facebook]用户帐户必须为您计划使用的广告帐户启用&#x200B;**[!DNL Manage campaigns]**&#x200B;权限。
- **Adobe Experience Cloud**&#x200B;业务帐户必须作为广告合作伙伴添加到您的[!DNL Facebook Ad Account]中。 使用 `business ID=206617933627973`. 有关详细信息，请参阅Facebook文档中的[将合作伙伴添加到您的业务经理](https://www.facebook.com/business/help/1717412048538897)。
   >[!IMPORTANT]
   >
   > 配置Adobe Experience Cloud的权限时，必须启用&#x200B;**管理促销活动**&#x200B;权限。 [!DNL Adobe Experience Platform]集成需要权限。
- 阅读并签署[!DNL Facebook Custom Audiences]服务条款。 为此，请转到`https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中`accountID`是您的[!DNL Facebook Ad Account ID]。

## ID匹配要求 {#id-matching-requirements}

[!DNL Facebook] 要求不要发送任何个人身份信息(PII)。因此，激活到[!DNL Facebook]的受众可以与&#x200B;*哈希*&#x200B;标识符（如电子邮件地址或电话号码）关联。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵循其相应要求。

## 电话号码哈希处理要求 {#phone-number-hashing-requirements}

在[!DNL Facebook]中激活电话号码的方法有两种：

- **摄取原始电话号码**:您可以将格式的原始电话号码 [!DNL E.164] 摄取到 [!DNL Platform]中。激活后，它们会自动进行哈希处理。 如果选择此选项，请确保始终将原始电话号码摄取到`Phone_E.164`命名空间中。
- **摄取经过哈希处理的电话号码**:您可以在将电话号码摄取到中之前，对您的电话号码进行 [!DNL Platform]哈希处理。如果选择此选项，请确保始终将您经过哈希处理的电话号码摄取到`Phone_SHA256`命名空间中。

>[!NOTE]
>
>无法在[!DNL Facebook]中激活被摄取到`Phone`命名空间的电话号码。


## 电子邮件哈希处理要求 {#email-hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或在Experience Platform中明确使用电子邮件地址，并在激活时对它们进行[!DNL Platform]哈希处理。

要了解如何在Experience Platform中摄取电子邮件地址，请参阅[批量摄取概述](/help/ingestion/batch-ingestion/overview.md)和[流摄取概述](/help/ingestion/streaming-ingestion/overview.md)。

如果您选择自行对电子邮件地址进行哈希处理，请确保符合以下要求：

- 从电子邮件字符串中裁切所有前导和尾随空格；示例：`johndoe@example.com`，不是`<space>johndoe@example.com<space>`;
- 对电子邮件字符串进行哈希处理时，请确保对小写字符串进行哈希处理；
   - 示例：`example@email.com`，不是`EXAMPLE@EMAIL.COM`;
- 确保经过哈希处理的字符串全部为小写
   - 示例：`55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，不是`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- 不要加盐。

>[!NOTE]
>
>未哈希命名空间中的数据在激活后由[!DNL Platform]自动进行哈希处理。
> 属性源数据不会自动进行哈希处理。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。
> 仅当选择属性作为源字段时，才会显示&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项。 选择命名空间时，不会显示该参数。

![身份映射转换](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 使用自定义命名空间 {#custom-namespaces}

在使用`Extern_ID`命名空间将数据发送到[!DNL Facebook]之前，请确保使用[!DNL Facebook Pixel]同步您自己的标识符。 有关详细信息，请参阅[Facebook官方文档](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers)。

## 连接到目标 {#connect-destination}

要连接到[!DNL Facebook]目标，请参阅[社交目标身份验证工作流](./workflow.md)。

以下视频还演示了配置社交目标和激活区段的步骤。 视频以LinkedIn为例，但各个社交目标的步骤相似。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## 将区段激活到[!DNL Facebook] {#activate-segments}

有关如何将区段激活到[!DNL Facebook]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。

在&#x200B;**[!UICONTROL 区段计划]**&#x200B;步骤中，向[!DNL Facebook Custom Audiences]发送区段时，必须提供[!UICONTROL 受众的来源]。

![Facebook受众来源](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## 导出的数据 {#exported-data}

对于[!DNL Facebook]，成功激活意味着将在[[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/)中以编程方式创建[!DNL Facebook]自定义受众。 由于用户符合激活区段的资格条件或被取消资格，因此将会添加和删除受众中的区段成员资格。

>[!TIP]
>
>Adobe Experience Platform与[!DNL Facebook]之间的集成支持历史受众回填。 当您将区段激活到目标时，所有历史区段资格都会发送到[!DNL Facebook]。

## 疑难解答 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

将区段激活到[!DNL Facebook]时，可能会收到以下错误：

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

当客户使用新创建的帐户，且[!DNL Facebook]权限尚未激活时，会发生此错误。

如果按照[Facebook帐户先决条件](#facebook-account-prerequisites)中的步骤操作后收到`400 Bad Request`错误消息，请允许几天时间[!DNL Facebook]权限生效。