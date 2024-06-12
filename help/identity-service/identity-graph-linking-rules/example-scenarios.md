---
title: 配置身份设置的示例方案
description: 了解配置身份设置的示例场景。
badge: Beta 版
exl-id: bccd5b7a-3836-47d8-b976-51747b9c1803
source-git-commit: f1779ee75c877649a69f9fa99f3872aea861beca
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# 配置身份图链接规则的示例场景

>[!AVAILABILITY]
>
>此功能尚不可用；标识图链接规则的测试版计划预计于7月在开发沙盒上开始。 有关参与标准的信息，请与您的Adobe客户团队联系。

本文档概述了配置身份图形链接规则时可以考虑的示例场景。

## 共享设备

在某些情况下，单个设备可能会发生多次登录：

| 共享设备 | 描述 |
| --- | --- |
| 家用计算机和平板电脑 | 丈夫和妻子均登录各自的银行账户。 |
| 公共信息亭 | 在机场登机的旅客使用他们的忠诚身份证登记签到行李并打印登机牌。 |
| 呼叫中心 | 呼叫中心人员代表致电客户支持以解决问题的客户在单个设备上登录。 |

![共享设备](../images/identity-settings/shared-devices.png)

在这些情况下，从图表角度看，如果不启用任何限制，单个ECID将链接到多个CRM ID。

利用身份图链接规则，您可以：

* 配置用于作为唯一标识符登录的ID。 例如，您可以将图表限制为仅存储一个具有CRM ID命名空间的身份，从而将CRM ID定义为共享设备的唯一标识符。
   * 通过这样做，您可以确保CRM ID不会被ECID合并。

## 电子邮件/电话方案无效

还有一些用户在注册时提供虚假值作为电话号码和/或电子邮件地址的实例。 在这些情况下，如果未启用限制，则电话/电子邮件相关的身份最终会链接到多个不同的CRM ID。

![invalid-email-phone](../images/identity-settings/invalid-email-phone.png)

利用身份图链接规则，您可以：

* 将CRM ID、电话号码或电子邮件地址配置为唯一标识符，从而将一个人限制为只能有一个与其帐户关联的CRM ID、电话号码和/或电子邮件地址。

## 标识值错误或错误

在某些情况下，会在系统中摄取非唯一、错误的标识值，而不管命名空间如何。 示例包括：

* 标识值为“user_null”的IDFA命名空间。
   * IDFA标识值应包含36个字符：32个字母数字字符和4个连字符。
* 标识值为“未指定”的电话号码命名空间。
   * 电话号码不应包含任何字母字符。

这些标识可能会导致以下图表，其中多个CRM ID与“坏”标识合并在一起：

![坏数据](../images/identity-settings/bad-data.png)

通过身份图链接规则，您可以将CRM ID配置为唯一标识符，以防止由于此类数据而造成不需要的用户档案折叠。

## 后续步骤

有关身份图链接规则的更多信息，请阅读以下文档：

* [身份图链接规则概述](./overview.md)
* [身份优化算法](./identity-optimization-algorithm.md)
* [Identity Service和实时客户资料](../identity-and-profile.md)
* [身份链接逻辑](../features/identity-linking-logic.md)
