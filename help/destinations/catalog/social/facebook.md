---
keywords: facebook连接；facebook连接；facebook目标；facebook;instagram;messenger
title: Facebook连接
description: 根据散列的电子邮件激活Facebook活动的用户档案，以实现受众定位、个性化和抑制。
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 2%

---


# [!DNL Facebook] 连接

## 概述 {#overview}

激活[!DNL Facebook]活动的用户档案，以根据散列电子邮件进行受众定位、个性化和抑制。

您可以在[!DNL Custom Audiences]支持的[!DNL Facebook’s]系列应用程序（包括[!DNL Facebook]、[!DNL Instagram]、[!DNL Audience Network]和[!DNL Messenger]）中使用此目标进行受众定位。 [!DNL Facebook Ads Manager] 中的版面级别会显示您要针对其运行营销活动的所选应用程序。

![Adobe Experience Platform UI中的Facebook目标](../../assets/catalog/social/facebook/catalog.png)

## 用例

为了帮助您更好地了解如何以及何时使用[!DNL Facebook]目标，以下是Adobe Experience Platform客户可以通过使用此功能解决的两个示例使用案例。

### 用例#1

一家在线零售商希望通过社交平台接触现有客户，并根据先前的订单向他们展示个性化的优惠。 这家在线零售商可以将自己的CRM中的电子邮件地址收录到Adobe Experience Platform，根据自己的线下数据构建细分，并将这些细分发送到[!DNL Facebook]社交平台，从而优化其广告支出。

### 用例#2

航空公司拥有不同的客户层（铜牌、银牌和金牌），希望通过社交平台为每个层提供个性化的优惠。 然而，并非所有客户都使用航空公司的移动应用程序，其中一些客户尚未登录公司网站。 公司有关这些客户的唯一标识符是会员ID和电子邮件地址。

要跨社交媒体进行目标，他们可以将客户数据从CRM载入Adobe Experience Platform，然后使用电子邮件地址作为标识符。

接下来，他们可以使用离线数据（包括关联的会员ID和客户层）来构建新的受众细分，以便通过[!DNL Facebook]目标进行目标。

## [!DNL Facebook]目标{#data-governance}的数据管理

>[!IMPORTANT]
>
>发送到[!DNL Facebook]的数据不能包括拼接身份。 您有责任履行此义务，并可通过确保为激活选择的区段在其合并策略中不使用拼接选项来执行。 了解有关[合并策略](/help/profile/ui/merge-policies.md)的更多信息。

## 支持的身份{#supported-identities}

[!DNL Facebook Custom Audiences] 支持下表所述身份的激活。了解有关[identities](/help/identity-service/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 当源标识为GAID目标时，选择GAID命名空间标识。 |
| IDFA | 面向广告商的Apple ID | 当源标识为IDFA目标时，选择IDFA命名空间标识。 |
| phone_sha256 | 使用SHA256算法散列化电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 按照[ID matching requirements](#id-matching-requirements-id-matching-requirements)部分中的说明，分别对纯文本和散列电话号码使用适当的命名空间。 当源字段包含未哈希化属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]自动对激活上的数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法散列化的电子邮件地址 | 纯文本和SHA256哈希电子邮件地址都受Adobe Experience Platform支持。 按照[ID matching requirements](#id-matching-requirements-id-matching-requirements)部分中的说明，分别对纯文本和散列电子邮件地址使用相应的命名空间。 当源字段包含未哈希化属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]自动对激活上的数据进行哈希处理。 |
| extern_id | 自定义用户ID | 当源标识是自定义目标时，请选择此命名空间标识。 |

## 导出类型{#export-type}

**区段导出**  — 您正在导出区段(受众)的所有成员，其中包含Facebook目标中使用的标识符（名称、电话号码或其他）。

## Facebook帐户先决条件{#facebook-account-prerequisites}

在将受众区段发送到[!DNL Facebook]之前，请确保满足以下要求：

- 您的[!DNL Facebook]用户帐户必须为您计划使用的Ad帐户启用&#x200B;**[!DNL Manage campaigns]**&#x200B;权限。
- **Adobe Experience Cloud**&#x200B;业务帐户必须作为广告合作伙伴添加到您的[!DNL Facebook Ad Account]中。 使用 `business ID=206617933627973`. 有关详细信息，请参阅Facebook文档中的[将合作伙伴添加到您的业务经理](https://www.facebook.com/business/help/1717412048538897)。
   >[!IMPORTANT]
   >
   > 配置Adobe Experience Cloud的权限时，必须启用&#x200B;**管理活动**&#x200B;权限。 [!DNL Adobe Experience Platform]集成需要权限。
- 阅读并签署[!DNL Facebook Custom Audiences]服务条款。 要执行此操作，请转至`https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中`accountID`是您的[!DNL Facebook Ad Account ID]。

## ID匹配要求{#id-matching-requirements}

[!DNL Facebook] 要求不要发送任何清晰的个人身份信息(PII)。因此，激活到[!DNL Facebook]的受众可以键出&#x200B;*散列*&#x200B;标识符，如电子邮件地址或电话号码。

根据您输入到Adobe Experience Platform的ID类型，您必须遵守其相应要求。

## 电话号码哈希要求{#phone-number-hashing-requirements}

在[!DNL Facebook]中激活电话号码有两种方法：

- **接收原始电话号码**:您可以将格式的原始电话号码 [!DNL E.164] 收录为 [!DNL Platform]。它们自动散列到激活。 如果选择此选项，请确保始终将原始电话号码收录到`Phone_E.164`命名空间。
- **正在获取哈希电话号码**:你可以先对电话号码进行哈希处理，然后再将其引入 [!DNL Platform]。如果选择此选项，请确保始终将哈希电话号码收录到`Phone_SHA256`命名空间。

>[!NOTE]
>
>无法在[!DNL Facebook]中激活被引入`Phone`命名空间的电话号码。


## 电子邮件散列要求{#email-hashing-requirements}

您可以先对电子邮件地址进行哈希处理，然后将其引入Adobe Experience Platform，或者在Experience Platform中使用电子邮件地址进行清除，并在激活上对它们进行[!DNL Platform]哈希处理。

要了解在Experience Platform中摄取电子邮件地址的信息，请参阅[批摄取概述](/help/ingestion/batch-ingestion/overview.md)和[流摄取概述](/help/ingestion/streaming-ingestion/overview.md)。

如果您选择自己对电子邮件地址进行哈希处理，请确保符合以下要求：

- 裁切电子邮件字符串中的所有前导和尾随空格；示例：`johndoe@example.com`，不是`<space>johndoe@example.com<space>`;
- 对电子邮件字符串进行散列时，请确保对小写字符串进行散列；
   - 示例：`example@email.com`，不是`EXAMPLE@EMAIL.COM`;
- 确保哈希字符串全为小写
   - 示例：`55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，不是`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- 不要用盐分。

>[!NOTE]
>
>未散列命名空间的数据在激活时由[!DNL Platform]自动散列。
> 属性源数据不会自动散列。 当源字段包含未哈希化属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]自动对激活上的数据进行哈希处理。
> **[!UICONTROL Apply transformation]**&#x200B;选项仅在选择属性作为源字段时显示。 在您选择命名空间时，不显示。

![身份映射转换](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 使用自定义命名空间{#custom-namespaces}

在使用`Extern_ID`命名空间向[!DNL Facebook]发送数据之前，请确保使用[!DNL Facebook Pixel]同步您自己的标识符。 有关详细信息，请参阅[官方文档](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers)。

## 连接到目标{#connect-destination}

要连接到[!DNL Facebook]目标，请参阅[社交网络目标身份验证工作流](./workflow.md)。

## 将区段激活到[!DNL Facebook] {#activate-segments}

有关如何将区段激活到[!DNL Facebook]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。

在&#x200B;**[!UICONTROL Segment schedule]**&#x200B;步骤中，向[!DNL Facebook Custom Audiences]发送区段时，必须提供[!UICONTROL Origin of audience]。

![Facebook来源受众](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## 导出的数据{#exported-data}

对于[!DNL Facebook]，成功的激活意味着将在[[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/)中以编程方式创建[!DNL Facebook]自定义受众。 由于用户对已激活的区段具有资格或取消资格，将会添加和删除该受众中的区段成员资格。

>[!TIP]
>
>Adobe Experience Platform与[!DNL Facebook]之间的集成支持历史受众回填。 在将区段激活到目标时，所有历史区段资格都将发送到[!DNL Facebook]。