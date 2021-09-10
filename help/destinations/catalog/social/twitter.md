---
title: Twitter自定义受众连接
description: 通过激活在Twitter中构建的受众，定位您的现有关注者和客户，并创建相关的再营销活动
source-git-commit: 3ea3f9ed156ba3a1fbc790153a4b8fa193d5e2da
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---


# [!DNL Twitter Custom Audiences] 连接

## 概述 {#overview}

通过激活在Twitter中构建的受众，定位您的现有关注者和客户，并创建相关的再营销活动。

## 先决条件 {#prerequisites}

在配置[!DNL Twitter Custom Audiences]目标之前，请确保查看您需要满足的以下Twitter先决条件。

1. 您的[!DNL Twitter Ads]帐户必须符合广告资格。 新的[!DNL Twitter Ads]帐户在创建后的前2周内不符合广告资格。
2. 您授权在[!DNL Twitter Audience Manager]中访问的Twitter用户帐户必须启用&#x200B;*[!DNL Partner Audience Manager]*&#x200B;权限。


## 支持的身份 {#supported-identities}

[!DNL Twitter Custom Audiences] 支持激活下表所述的身份。了解有关[identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)的更多信息。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Adobe Experience Platform支持Google广告ID(GAID)和Apple ID for Advertisers(IDFA)。 请在目标激活工作流的[映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中，相应地从源架构映射这些命名空间和/或属性。 |
| 电子邮件 | 用户的电子邮件地址 | 请将纯文本电子邮件地址和SHA256哈希电子邮件地址映射到此字段。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 如果您在将客户电子邮件地址上传到Adobe Experience Platform之前对其进行哈希处理，请注意，这些身份必须使用SHA256进行哈希处理，而不必加任何盐。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型 {#export-type}

**区段导出**  — 您要导出区段（受众）的所有成员，以及在Twitter自定义受众目标中使用的标识符。

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时使用[!DNL Twitter Custom Audiences]目标，以下是Adobe Experience Platform客户可通过使用此目标解决的示例用例。

### 用例#1

通过在Twitter中将Adobe Experience Platform中构建的受众激活为[!DNL List Custom Audiences]，定位您的现有关注者和客户，并创建相关的再营销活动。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的 [!DNL Twitter Ads] 帐户ID。这可在您的[!DNL Twitter Ads]设置中找到。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请阅读[将配置文件和区段激活到流区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

## 数据使用和管理 {#data-usage-governance}

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据管理的详细信息，请参阅[数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

## 其他资源 {#additional-resources}

将受众区段映射到Twitter时，请确保满足以下区段命名要求：

1. 提供人类可读的区段映射名称。 我们建议您使用与Experience Platform区段相同的名称。
2. 请勿使用特殊字符（+和、%）：;@ / = ? $)。 如果您的Experience Platform区段名称包含这些字符，请先删除这些字符，然后再将区段映射到Twitter目标。

有关Twitter中[!DNL List Custom Audiences]的更多信息，请参阅[Twitter文档](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html)。