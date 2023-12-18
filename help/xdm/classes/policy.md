---
title: 策略类
description: 了解Experience Data Model (XDM)中的“策略”类。
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 4%

---

# [!UICONTROL 策略] 类

在Experience Data Model (XDM)中， [!UICONTROL 策略] class捕获定义保险单的最小属性集。

![](../images/classes/policy.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `assignedBeneficiary` | 数组 [[!UICONTROL 人员]](../data-types/person.md) 数据类型 | 捕获分配给保单的受益人（或受益人）。 |
| `benefitAmount` | [[!UICONTROL 货币]](../data-types/currency.md) | 根据保险单条款支付的金额。 |
| `location` | [[!UICONTROL 邮政地址]](../data-types/postal-address.md) | 保险单签发地点。 |
| `owner` | [!UICONTROL 对象] | 捕获投保人的个人资料信息。 |
| `owner.faxPhone` | [[!UICONTROL 电话号码]](../data-types/phone-number.md) | 所有者的传真电话号码。 |
| `owner.homeAddress` | [[!UICONTROL 邮政地址]](../data-types/postal-address.md) | 所有者家庭地址。 |
| `owner.homePhone` | [[!UICONTROL 电话号码]](../data-types/phone-number.md) | 业主的家庭电话号码。 |
| `owner.mobilePhone` | [[!UICONTROL 电话号码]](../data-types/phone-number.md) | 所有者的手机号码。 |
| `owner.personalEmail` | [[!UICONTROL 电子邮件地址]](../data-types/email-address.md) | 所有者的个人电子邮件地址。 |
| `ID` | [!UICONTROL 字符串] | 保险单的标识符。 |
| `_id` | [!UICONTROL 字符串] | 系统为记录生成的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会向其提供显式值。 但是，如果您愿意，仍然可以选择提供自己的唯一ID值。 |
| `endDate` | [!UICONTROL 日期时间] | 保险单承保结束（或结束）的日期。 |
| `hasAssignedBeneficiary` | [!UICONTROL 布尔型] | 指示是否已为政策分配受益人。 |
| `name` | [!UICONTROL 字符串] | 保险单的名称。 |
| `startDate` | [!UICONTROL 日期时间] | 保险单承保开始（或开始）的日期。 |
| `type` | [!UICONTROL 字符串] | 保险单的类型，如房屋、汽车、出租人或船。 |

{style="table-layout:auto"}
