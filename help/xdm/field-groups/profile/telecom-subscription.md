---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；电信；订阅；电信；架构设计；字段组；字段组；
solution: Experience Platform
title: 电信订阅模式字段组
topic-legacy: overview
description: 本文档概述了电信订阅架构字段组。
source-git-commit: 19675e4042c28061a4b2ed4e68374d5e09216ba1
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 5%

---

# [!UICONTROL 电信] 订阅模式字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL 电信] 订阅是类的标准架构字段组， [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 用于描述客户的电信订阅计划，包括定价、软件包和单个产品订阅。

字段组提供了一个对象类型字段`telecomSubscription`，其属性如下所述。

![电信订购结构](../../images/field-groups/telecom-subscription/structure.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `internetSubscription` | 对象数组 | 介绍Internet订阅计划详细信息，如数据上限、连接类型和速度详细信息。 有关更多信息，请参阅下面的[部分](#internetSubscription)。 |
| `landlineSubscription` | 对象数组 | 介绍固定电话订阅计划详细信息，包括选定功能、分钟数和拨号计划。 有关更多信息，请参阅下面的[部分](#landlineSubscription)。 |
| `mediaSubscription` | 对象数组 | 介绍媒体订阅计划详细信息，包括渠道数量和包含的流服务。 有关更多信息，请参阅下面的[部分](#mediaSubscription)。 |
| `mobileSubscription` | 对象数组 | 介绍移动订阅计划详细信息，包括行数、数据费率、成本等。 有关更多信息，请参阅下面的[部分](#mobileSubscription)。 |
| `primarySubscriber` | [[!UICONTROL 人员]](../../data-types/person.md) | 描述订阅的所有者。 |
| `bundleName` | 字符串 | 捕获客户在其中注册的任何类型订阅包的名称，如`Internet + Media`。 |
| `primaryPartyID` | 字符串 | 负责订阅的主要人员的标识符，通常可能是其设备电话号码。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` 提供了对象数组。每个对象的结构如下所述。

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL 电信订购]](../../data-types/telecom-subscription.md) | 介绍有关订阅的一般详细信息，包括订阅时长、费用、状态等。 介绍有关订阅的一般详细信息，包括订阅时长、费用、状态等。 |
| `connectionType` | 字符串 | 订阅的连接类型。 |
| `dataCap` | 整数 | 帐户的数据上限限制（以MB为单位）。 |
| `downloadSpeed` | 整数 | 订阅可用的最大下载速度，以MB(MB)为单位。 |
| `selfSetup` | 布尔值 | 指示客户是否有资格进行Internet设置，而无需技术人员的访问。 |
| `uploadSpeed` | 整数 | 订阅可用的最大上传速度，以MB(MB)为单位。 |

{style=&quot;table-layout:auto&quot;}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` 提供了对象数组。每个对象的结构如下所述。

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL 电话号码]](../../data-types/telecom-subscription.md) | 分配给此订阅的电话号码。 |
| `subscriptionDetails` | [[!UICONTROL 电信订购]](../../data-types/telecom-subscription.md) | 介绍有关订阅的一般详细信息，包括订阅时长、费用、状态等。 |
| `callBlocking` | 布尔值 | 指示固定电话订阅功能是否包括呼叫阻止。 |
| `callForwarding` | 布尔值 | 指示固定电话订阅功能是否包括呼叫转发。 |
| `callWaiting` | 布尔值 | 指示固定电话订阅功能是否包括等待呼叫。 |
| `callerID` | 布尔值 | 指示固定电话订阅功能是否包括来电者ID。 |
| `internationalCalling` | 布尔值 | 指示固定电话订购功能是否包括国际电话。 |
| `minutes` | 整数 | 订阅内每月可用的分钟数。 |
| `threeWayCalling` | 布尔值 | 指示固定电话订阅功能是否包含三向调用。 |
| `unlimitedDomesticLongDistance` | 布尔值 | 指示固定电话订购功能是否包括无限制的国内长途呼叫。 |
| `unlimitedLocalCalling` | 布尔值 | 指示固定电话订阅功能是否包括无限制的本地呼叫。 |
| `voicemail` | 布尔值 | 指示固定电话订阅功能是否包含语音邮件。 |

{style=&quot;table-layout:auto&quot;}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` 提供了对象数组。每个对象的结构如下所述。

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `streamingServices` | 对象数组 | 订阅中包含的所有流服务的列表。 每个数组项目包含以下属性： <ul><li>`promotionLength`:如果作为促销活动的一部分添加了流服务，则促销活动的时长（以月为单位）。</li><li>`promotionalAddition`:指示流服务是否已添加为促销活动的一部分。</li><li>`serviceName`:流服务的名称。</li></ul> |
| `subscriptionDetails` | [[!UICONTROL 电信订购]](../../data-types/telecom-subscription.md) | 介绍有关订阅的一般详细信息，包括订阅时长、费用、状态等。 |
| `channels` | 整数 | 媒体订阅中包含的频道数。 |

{style=&quot;table-layout:auto&quot;}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` 提供了对象数组。每个对象的结构如下所述。

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL 电话号码]](../../data-types/telecom-subscription.md) | 分配给此订阅的电话号码。 |
| `subscriptionDetails` | [[!UICONTROL 电信订购]](../../data-types/telecom-subscription.md) | 介绍有关订阅的一般详细信息，包括订阅时长、费用、状态等。 |
| `earlyUpgradeEnrollment` | 布尔值 | 指示客户是否选择提前升级。 |
| `planLevel` | 字符串 | 分配给此订阅的移动计划的名称。 |
| `portedNumber` | 布尔值 | 指示客户是否从其他运营商端口其号码。 |

{style=&quot;table-layout:auto&quot;}

