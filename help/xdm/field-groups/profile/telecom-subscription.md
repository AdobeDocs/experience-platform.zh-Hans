---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；电信；订阅；电信；架构设计；字段组；字段组；
solution: Experience Platform
title: 电信订阅架构字段组
description: 本文档概述了Telecom Subscription模式字段组。
exl-id: 00c20081-09d0-425c-9894-0f957558bd43
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 4%

---

# [!UICONTROL 电信订阅] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 查看文档 [字段组名称更新](../name-updates.md) 了解更多信息。

[!UICONTROL 电信订阅] 是的标准架构字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md) 其中描述了客户的电信订阅计划，包括定价、产品包和单个产品订阅。

字段组提供单个对象类型字段， `telecomSubscription`，其属性如下所述。

![电信订阅结构](../../images/field-groups/telecom-subscription/structure.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `internetSubscription` | 对象数组 | 描述Internet订阅计划详细信息，如数据限制、连接类型和速度详细信息。 请参阅 [以下部分](#internetSubscription) 了解更多信息。 |
| `landlineSubscription` | 对象数组 | 描述固定电话订阅计划详细信息，包括选定的功能、分钟数和拨号计划。 请参阅 [以下部分](#landlineSubscription) 了解更多信息。 |
| `mediaSubscription` | 对象数组 | 描述媒体订阅计划详细信息，包括频道数量和包含的流媒体服务。 请参阅 [以下部分](#mediaSubscription) 了解更多信息。 |
| `mobileSubscription` | 对象数组 | 描述移动订阅计划详细信息，包括线路数、数据速率、成本等。 请参阅 [以下部分](#mobileSubscription) 了解更多信息。 |
| `primarySubscriber` | [[!UICONTROL 人员]](../../data-types/person.md) | 描述订阅的所有者。 |
| `bundleName` | 字符串 | 捕获客户注册的任何类型的订阅包的名称，例如 `Internet + Media`. |
| `primaryPartyID` | 字符串 | 负责订阅的主要人员的标识符，通常可能是他们的设备电话号码。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` 以对象数组形式提供。 每个对象的结构如下所述。

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL 电信订阅]](../../data-types/telecom-subscription.md) | 描述有关订阅的一般详细信息，包括订阅时长、费用、状态等。 描述有关订阅的一般详细信息，包括订阅时长、费用、状态等。 |
| `connectionType` | 字符串 | 订阅的连接类型。 |
| `dataCap` | 整数 | 帐户的数据上限，以兆字节(MB)为单位。 |
| `downloadSpeed` | 整数 | 订阅可用的最大下载速度（以MB为单位）。 |
| `selfSetup` | 布尔值 | 指示客户是否有资格在没有技术人员帮助的情况下进行Internet设置。 |
| `uploadSpeed` | 整数 | 订阅可用的最大上传速度（以MB为单位）。 |

{style="table-layout:auto"}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` 以对象数组形式提供。 每个对象的结构如下所述。

![固定电话订阅](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL 电话号码]](../../data-types/telecom-subscription.md) | 分配给此订阅的电话号码。 |
| `subscriptionDetails` | [[!UICONTROL 电信订阅]](../../data-types/telecom-subscription.md) | 描述有关订阅的一般详细信息，包括订阅时长、费用、状态等。 |
| `callBlocking` | 布尔值 | 指示固定电话订阅功能是否包括呼叫阻止。 |
| `callForwarding` | 布尔值 | 指示固定电话订阅功能是否包括呼叫转移。 |
| `callWaiting` | 布尔值 | 指示固定电话订阅功能是否包括呼叫等待。 |
| `callerID` | 布尔值 | 指示固定电话订阅功能是否包括来电显示。 |
| `internationalCalling` | 布尔值 | 指示固定电话订阅功能是否包括国际呼叫。 |
| `minutes` | 整数 | 订阅中每月可用的分钟数。 |
| `threeWayCalling` | 布尔值 | 指示固定电话订阅功能是否包括三方呼叫。 |
| `unlimitedDomesticLongDistance` | 布尔值 | 指示固定电话订阅功能是否包括无限国内长途呼叫。 |
| `unlimitedLocalCalling` | 布尔值 | 指示固定电话订阅功能是否包括无限制的本地呼叫。 |
| `voicemail` | 布尔值 | 指示固定电话订阅功能是否包括语音邮件。 |

{style="table-layout:auto"}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` 以对象数组形式提供。 每个对象的结构如下所述。

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `streamingServices` | 对象数组 | 订阅中包含的所有流媒体服务的列表。 每个数组项都包含以下属性： <ul><li>`promotionLength`：促销的时长，以月为单位（如果将流服务作为促销的一部分添加）。</li><li>`promotionalAddition`：指示是否将流服务作为促销的一部分添加。</li><li>`serviceName`：流服务的名称。</li></ul> |
| `subscriptionDetails` | [[!UICONTROL 电信订阅]](../../data-types/telecom-subscription.md) | 描述有关订阅的一般详细信息，包括订阅时长、费用、状态等。 |
| `channels` | 整数 | 媒体订阅中包含的频道数。 |

{style="table-layout:auto"}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` 以对象数组形式提供。 每个对象的结构如下所述。

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL 电话号码]](../../data-types/telecom-subscription.md) | 分配给此订阅的电话号码。 |
| `subscriptionDetails` | [[!UICONTROL 电信订阅]](../../data-types/telecom-subscription.md) | 描述有关订阅的一般详细信息，包括订阅时长、费用、状态等。 |
| `earlyUpgradeEnrollment` | 布尔值 | 指示客户是否选择提前升级。 |
| `planLevel` | 字符串 | 分配给此订阅的移动计划的名称。 |
| `portedNumber` | 布尔值 | 指示客户是否从其他运营商移植其号码。 |

{style="table-layout:auto"}
