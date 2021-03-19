---
keywords: linkedin连接；linkedin连接；linkedin目标；linkedin;
title: Linkedin匹配受众连接
description: 根据经过散列处理的电子邮件，为您的LinkedIn活动激活用户档案以进行受众定位、个性化和抑制。
translation-type: tm+mt
source-git-commit: fd95357f3e3533fe6b7b9752798dd99eb1cc0eb5
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# [!DNL LinkedIn Matched Audiences] 连接

根据经过散列处理的电子邮件和移动ID，激活[!DNL LinkedIn]活动的用户档案，以实现受众定位、个性化和抑制。

![Adobe Experience Platform UI中的LinkedIn目标](../../assets/catalog/social/linkedin/catalog.png)

## 用例

为了帮助您更好地了解如何以及何时使用[!DNL LinkedIn Matched Audiences]目标，以下是Adobe Experience Platform客户可通过使用此功能解决的用例。

软件公司会组织会议并希望与参加者保持联系，并根据参加者的会议出席状态向他们展示个性化的优惠。 公司可以将自己的[!DNL CRM]电子邮件地址或移动设备ID收录到Adobe Experience Platform中。 然后，他们可以根据自己的线下数据构建细分，并将这些细分发送到[!DNL LinkedIn]社交平台，优化广告支出。

## 目标特性{#destination-specs}

[!DNL LinkedIn Matched Audiences] 支持激活以下身份：散乱的 [!DNL GAID]电子邮件 [!DNL IDFA]。

### 支持的身份{#supported-identities}

[!DNL LinkedIn Matched Audiences] 支持下表所述身份的激活。了解有关[identities](/help/identity-service/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 当源标识为GAID命名空间时，选择此目标标识。 |
| IDFA | 面向广告商的Apple ID | 当源标识为IDFA命名空间时，选择此目标标识。 |
| email_lc_sha256 | 使用SHA256算法散列化的电子邮件地址 | 纯文本和SHA256哈希电子邮件地址都受Adobe Experience Platform支持。 按照[ID matching requirements](#id-matching-requirements-id-matching-requirements)部分中的说明，分别对纯文本和散列电子邮件使用相应的命名空间。 当源字段包含未哈希化属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]自动对激活上的数据进行哈希处理。 |


### 导出类型{#export-type}

**区段导出**  — 您正在导出区段(受众)的所有成员，其中包含目标中使用的标识符(名称、电话号码和其他 [!DNL LinkedIn Matched Audiences] )。

### LinkedIn帐户先决条件{#LinkedIn-account-prerequisites}

在使用[!UICONTROL LinkedIn Matched Audience]目标之前，请确保您的[!DNL LinkedIn Campaign Manager]帐户具有[!DNL Creative Manager]权限级别或更高级别。

要了解如何编辑您的[!DNL LinkedIn Campaign Manager]用户权限，请参阅LinkedIn文档中的[添加、编辑和删除广告帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753)。

### ID匹配要求{#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 要求不要发送任何清晰的个人身份信息(PII)。因此，激活到[!DNL LinkedIn Matched Audiences]的受众可以键出&#x200B;*散列*&#x200B;标识符，如电子邮件地址或移动设备ID。

根据您输入到Adobe Experience Platform的ID类型，您必须遵守其相应要求。

#### 电子邮件散列要求{#email-hashing-requirements}

您可以先对电子邮件地址进行哈希处理，然后将其引入Adobe Experience Platform，或者在Experience Platform中使用电子邮件地址进行清除，并在激活上对它们进行[!DNL Platform]哈希处理。

要了解在Experience Platform中摄取电子邮件地址的信息，请参阅[批摄取概述](/help/ingestion/batch-ingestion/overview.md)和[流摄取概述](/help/ingestion/streaming-ingestion/overview.md)。

如果您选择自己对电子邮件地址进行哈希处理，请确保符合以下要求：

- 修剪电子邮件字符串中的所有前导和尾随空格。 例如：`johndoe@example.com`，不是`<space>johndoe@example.com<space>`;
- 对电子邮件字符串进行散列时，请确保对小写字符串进行散列；
   - 示例：`example@email.com`，不是`EXAMPLE@EMAIL.COM`;
- 确保哈希字符串全为小写
   - 示例：`55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，不是`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- 不要用盐分。

>[!NOTE]
>
>未散列命名空间的数据在激活时由[!DNL Platform]自动散列。
> 属性源数据不会自动散列。
> 
> 在[标识映射](../../ui/activate-destinations.md#identity-mapping)步骤中，当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]自动对激活上的数据进行哈希处理。
> 
> **[!UICONTROL Apply transformation]**&#x200B;选项仅在选择属性作为源字段时显示。 在您选择命名空间时，不显示。

![身份映射转换](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 连接到目标{#connect-destination}

要连接到[!DNL LinkedIn Matched Audiences]目标，请参阅[社交网络目标身份验证工作流](./workflow.md)。

## 将区段激活到[!DNL LinkedIn Matched Audiences] {#activate-segments}

有关如何将区段激活到[!DNL LinkedIn Matched Audiences]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。

## 导出的数据{#exported-data}

成功的激活意味着将在[[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)中以编程方式创建[!DNL LinkedIn]自定义受众。 由于用户对已激活的区段具有资格或取消资格，将会添加和删除该受众中的区段成员资格。

>[!TIP]
>
>Adobe Experience Platform与[!DNL LinkedIn Matched Audiences]之间的集成支持历史受众回填。 在将区段激活到目标时，所有历史区段资格都将发送到[!DNL LinkedIn]。