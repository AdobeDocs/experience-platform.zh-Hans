---
title: 配置示例
description: 使用图形模拟工具了解配置的示例。
hide: true
hidefromtoc: true
badge: Beta 版
source-git-commit: ba72abd9febc6d9e6491748519199b54a26ae1c5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 22%

---

# 示例图形配置

>[!NOTE]
>
>“CRM ID”是一个自定义命名空间。 因此，下面的示例要求您创建一个显示名称和身份符号为“CRM ID”的自定义命名空间。

以下部分提供了您在图形模拟中可能遇到的图形场景示例。

## 仅限CRM ID

事件：

* CRM ID：Tom，ECID：111

算法配置：

| 优先级 | 显示名称 | 标识符号 | 标识类型 | 每个图唯一 |
| ---| --- | --- | --- | --- |
| 1 | CRM ID | CRM ID | 跨设备 | 是 |
| 2 | ECID | ECID | COOKIE | 否 |

+++选择以查看模拟图形

+++

## 包含经过哈希处理的电子邮件的CRM ID

在此方案中，CRM ID是摄取的，表示在线（体验事件）和离线（配置文件记录）数据。 此方案还涉及引入哈希电子邮件，该电子邮件表示在CRM记录数据集中与CRM ID一起发送的其他命名空间。

事件：

* CRM ID： Tom， Email_LC_SHA256： tom<span>@acme.com
* CRM ID：Tom，ECID：111
* CRM ID：Summer， Email_LC_SHA256： summer<span>@acme.com
* CRM ID：Summer，ECID：222

算法配置：

| 优先级 | 显示名称 | 标识符号 | 标识类型 | 每个图唯一 |
| ---| --- | --- | --- | --- |
| 1 | CRM ID | CRM ID | 跨设备 | 是 |
| 2 | 电子邮件（SHA256，小写） | Email_LC_SHA256 | 电子邮件 | 否 |
| 3 | ECID | ECID | COOKIE | 否 |

+++选择以查看模拟图形

+++

## 包含哈希电子邮件、哈希手机、GAID和IDFA的CRM ID

事件：

* CRM ID：Tom， Email_LC_SHA256： aabbcc， Phone_SHA256： 123-4567
* CRM ID：Tom，ECID：111
* CRM ID：Tom，ECID：222，IDFA：A-A-A
* CRM ID：Summer，Email_LC_SHA256：deeff，Phone_SHA256:765-4321
* CRM ID：Summer，ECID：333
* CRM ID：Summer，ECID：444，GAID：B-B-B

算法配置：

| 优先级 | 显示名称 | 标识符号 | 标识类型 | 每个图唯一 |
| ---| --- | --- | --- | --- |
| 1 | CRM ID | CRM ID | 跨设备 | 是 |
| 2 | 电子邮件（SHA256，小写） | Email_LC_SHA256 | 电子邮件 | 否 |
| 3 | 手机 (SHA256) | Phone_SHA256 | 电话 | 否 |
| 4 | Google Ad ID (GAID) | GAID | 设备 | 否 |
| 5 | Apple IDFA(Apple的ID) | IDFA | 设备 | 否 |
| 6 | ECID | ECID | COOKIE | 否 |

+++选择以查看模拟图形

+++