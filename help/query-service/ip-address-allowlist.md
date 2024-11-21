---
keywords: IP地址， IP范围，允许列表，允许列表，查询服务，网络访问
title: 列入允许列表查询服务的IP地址
description: 本页提供了更新的IP范围，可将其添加到允许列表中以安全访问查询服务。
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: ac29d10d3774a736d1e54255508ba244ff72f278
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# IP地址允许列表 {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe建议您将此页面加入书签，每三个月重新访问一次，以检查最新IP地址。 Adobe不提供新IP范围的通知。
> * 自2024年10月15日起，只有新IP范围才对查询服务访问有效。 过时的IP地址不再有效。 确保您的允许列表仅包含新IP以避免服务中断。

## 概述 {#overview}

您可以通过网络防火墙定义网络访问控制。 通过指定适当的IP范围，您可以允许通信用于查询服务访问。

作为持续改进的一部分，Adobe更新了用于网络访问查询服务的IP范围。 以前的IP地址现已弃用，只有新的IP地址有效。 更新您的IP允许列表以包含以下新IP范围对于保持不间断服务至关重要。

Adobe列入允许列表建议您将以下特定于区域的IP范围添加到，具体取决于您的地区。 未能添加这些特定于区域的IP范围可能会导致错误或服务中断。

## VA7：美国和美国的客户 {#us-americas}

**新IP：** 4.152.211.251

## NLD2：EMEA客户 {#emea}

**新IP：** 108.141.12.47

## AUS5：APAC客户 {#apac}

**新IP：** 40.82.220.111

## CAN2：加拿大客户 {#can2}

**新IP：** 4.172.28.20

## GBR9：英国客户 {#gbr9}

**新IP：** 20.254.80.141

## 设置基于IP的限制 {#set-ip-restrictions}

使用[Data Distiller Authorization API指南](./auth-api/overview.md)设置基于IP的限制。 这些基于IP的限制可确保只有获得批准的网络和客户端计算机才能通过Adobe Experience Platform中的SQL访问数据。 了解如何配置、强制执行并监控IP限制以维护高安全标准，以及提供实时访问跟踪和警报功能。

* [快速入门指南](./auth-api/getting-started.md)
* [IP访问端点指南](./auth-api/ip-access.md)
* [IP验证端点指南](./auth-api/validate.md)
