---
keywords: 身份rtcdp;rtcdp身份；实时cdp身份
title: Real-time Customer Data Platform身份
description: Adobe Experience Platform Identity Service通过跨设备和系统将身份桥接在一起，帮助您更好地了解客户及其行为。
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# 身份概述

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统将身份桥接在一起，帮助您更好地了解客户及其行为。 通常，您的客户会跨多个渠道与您的品牌进行交互，这可能包括在线浏览您的网站、在店内购买、加入忠诚度计划或致电帮助台寻求支持等。 在这些多个系统中，会为该客户创建一个标识， [!DNL Identity Service] 使这些身份合在一起，看到完整的图景。

现在，您可以看到这是同一个客户，而不是通过五个不同的渠道与您的品牌进行交互的五个单独客户，并且您可以确保他们通过每次交互获得一致、个性化、相关的体验。 随着关于客户的更多信息（例如，您网站的匿名浏览器决定注册一个帐户并登录），信息会被拼合在一起，客户的形象也变得越来越清晰。

## 身份命名空间

身份命名空间是 [!DNL Identity Service] 并用作为客户身份提供额外上下文的指标。 常用ID命名空间的示例为“电子邮件”，通过在多个网站中使用相同的电子邮件地址，您可以拼合多个不同的身份（每个身份具有唯一的客户ID），因为实际上属于同一客户。 [!DNL Experience Platform] 允许您使用ID命名空间在用户界面中搜索各个用户档案。 有关查看用户档案的更多信息，请参阅 [配置文件浏览概述](profile-browse.md). 要了解有关身份命名空间的更多信息，请参阅 [身份命名空间概述](../../identity-service/namespaces.md).

## 身份图

身份图是不同身份命名空间之间关系的映射，可直观地表示客户如何跨不同渠道与您的品牌进行交互。 所有客户身份图表都由 [!DNL Identity Service] 以响应客户活动。

[!DNL Identity Service] 管理仅由您的组织查看并基于您的数据构建（称为专用图）的身份图。 [!DNL Identity Service] 当已摄取的数据记录包含多个身份时，通过在找到的身份之间添加关系来增强您的专用图。

## 后续步骤

身份及其之间的关系由 [!DNL Identity Service] 利用 [!DNL Real-Time Customer Profile] 以构建每个客户及其交互的完整图景。 要了解更多信息，请访问 [Identity Service文档](../../identity-service/home.md).
