---
title: Facebook目标
seo-title: Facebook目标
description: 根据散列电子邮件激活Facebook活动的用户档案，进行受众定位、个性化和抑制。
seo-description: 根据散列电子邮件激活Facebook活动的用户档案，进行受众定位、个性化和抑制。
translation-type: tm+mt
source-git-commit: 522014f8e5f3de0f553a69763d3a37482953b7c4
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---


# Facebook目标

## 概述 {#overview}

根据散列电子邮件激活Facebook活动的用户档案，进行受众定位、个性化和抑制。

![实时CDP UI中的Facebook目标](/help/rtcdp/destinations/assets/facebook-destination.png)

## 用例

为了帮助您更好地了解Facebook目标的使用方式和时间，以下是Adobe实时客户数据平台客户可以通过此功能解决的两个示例使用案例。


### 用例#1


一家在线零售商希望通过社交平台接触现有客户，并根据先前的订单向他们展示个性化的优惠。 这家在线零售商可以将电子邮件地址从自己的CRM采集到Adobe实时CDP，根据自己的线下数据构建细分，并将这些细分发送到Facebook社交平台，从而优化其广告支出。


### 用例#2


航空公司拥有不同的客户层（铜牌、银牌和金牌），希望通过社交平台为每层提供个性化优惠。 然而，并非所有客户都使用航空公司的移动应用程序，其中一些客户还没有登录该公司的网站。 公司有关这些客户的唯一标识符是会员ID和电子邮件地址。
要跨社交媒体进行目标，他们可以将散列电子邮件地址作为标识符，将客户数据从CRM载入Adobe实时CDP。
接下来，他们可以将线下活动数据与现有在线受众数据相结合，以建立新的细分，并通过Facebook目标进行目标。

## 目标特定信息 {#destination-specs}

### Facebook目标的数据管理 {#data-governance}

>[!IMPORTANT]
>
>发送到Facebook的数据不应包括拼合身份。 您有责任履行此义务，并可确保为激活选择的区段在其合并策略中不使用拼接选项来执行此操作。 进一步了 [解合并策略](/help/profile/ui/merge-policies.md)。

### 激活类型 {#activation-type}

**区段导出** -您正在导出包含标识符（名称、电话号码等）的区段(受众)的所有成员。 在Facebook目标中使用。

### Facebook帐户先决条件 {#facebook-account-prerequisites}

在将受众区段发送到之 [!DNL Facebook]前，请确保满足以下要求：

1. 您 [!DNL Facebook] 的用户帐户必须为 **[!DNL Manage campaigns]** 您计划使用的广告帐户启用权限。
2. 将Adobe Experience **Cloud商业帐户** （作为广告合作伙伴）添加到您的 [!DNL Facebook Ad Account]中。 使用 `business ID=206617933627973`. 有关详 [细信息，请参阅Facebook文档](https://www.facebook.com/business/help/1717412048538897) 中的将合作伙伴添加到您的业务经理。
   >[!IMPORTANT]
   > 配置Adobe Experience Cloud的权限时，必须启用“管理 **活动** ”权限。 这是集成所必需 [!DNL Adobe Real-time CDP] 的。
3. 阅读并签署 [!DNL Facebook Custom Audiences] 服务条款。 为此，请转 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`到您 `accountID` 的位 [!DNL Facebook Ad Account ID]置。

### 电子邮件散列要求 {#email-hashing-requirements}

Facebook要求不明确发送任何个人可识别信息(PII)。 因此，激活到Facebook的受众必须锁定散列 *电子邮件* 地址。 您可以在将电子邮件地址引入Adobe Experience Platform之前选择对其进行散列处理，也可以选择在Experience Platform中清晰地处理电子邮件地址，并在激活上使用我们的算法对它们进行散列处理。

要了解如何在Experience Platform中摄取电子邮件地址，请参 [阅批量摄取概述](/help/ingestion/batch-ingestion/overview.md) 和快速 [摄取概述](/help/ingestion/streaming-ingestion/overview.md)。

如果您选择自行对电子邮件地址进行哈希处理，请确保符合以下要求：

* 修剪电子邮件字符串中的所有前导和尾随空格； 示例： `johndoe@example.com`，不是 `<space>johndoe@example.com<space>`;
* 散列电子邮件字符串时，请确保散列小写字符串；
   * 示例： `example@email.com`，不是 `EXAMPLE@EMAIL.COM`;
* 确保哈希字符串全为小写
   * 示例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，不是 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 不要把绳子盐掉。


>[!IMPORTANT]
>
>如果您选择不对电子邮件地址进行哈希处理，则在将区段激活到Facebook时，Adobe实时CDP会为您执行此操作。 在激活 [工作流](/help/rtcdp/destinations/activate-destinations.md#activate-data) （请参阅步骤5）中，选择以 `Email` 下原始电子邮件地址选 *项和散列式电子邮* 件地址选 `Email_LC_SHA256` 项(如 **&#x200B;下所示)。


![散列激活](/help/rtcdp/destinations/assets/identity-mapping.png)

## 连接到目标 {#connect-destination}

要连接到Facebook目标，请参阅社交 [网络目标身份验证工作流](/help/rtcdp/destinations/social-network-destinations-workflow.md)。


## 将区段激活到Facebook {#activate-segments}

有关如何将区段激活到Facebook的说明，请参阅将 [数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。