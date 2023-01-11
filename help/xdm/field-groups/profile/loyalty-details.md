---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；忠诚度详细信息；架构设计；字段组；字段组；
solution: Experience Platform
title: 忠诚度详细信息架构字段组
description: 本文档概述了忠诚度详细信息架构字段组。
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 3%

---

# [!UICONTROL 忠诚度详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 请参阅 [字段组名称更新](../name-updates.md) 以了解更多信息。

[!UICONTROL 忠诚度详细信息] 是的标准架构字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md). 字段组提供单个对象类型字段， `loyalty`，可捕获与客户忠诚度计划中人员成员资格相关的信息。

![](../../images/field-groups/loyalty-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `pointsExpiration` | 对象数组 | 列出任何即将过期的会员积分（或会员积分组）及其过期日期。 每个数组项目必须是包含以下两个属性的对象： <ul><li>`pointsExpirationDate`:ISO 8601日期时间（时间点将过期）。</li><li>`pointsExpiring`:截止到相关过期日期的点数余额。</li></ul> |
| `joinDate` | DateTime | 人员加入忠诚度计划时的ISO 8601日期时间。 |
| `loyaltyID` | 字符串数组 | 表示与忠诚度计划会员关联的忠诚度计划ID。 |
| `points` | 双精度 | 忠诚会员的当前忠诚点数或奖励余额。 |
| `pointsRedeemed` | 双精度 | 会员已申请购买或已换领的积分金额。 |
| `program` | 字符串 | 注册人员的忠诚度计划的名称。 |
| `status` | 字符串 | 人员的忠诚会员资格的当前状态，如 `active`, `disabled`或 `suspended`. |
| `tier` | 字符串 | 捕获注册人员的忠诚度计划层。 |
| `upgradeDate` | 字符串 | 忠诚度会员升级到其最新层级的日期。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
