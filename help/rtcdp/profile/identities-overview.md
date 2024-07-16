---
keywords: 身份rtcdp；rtcdp身份；real-time cdp身份
title: Real-time Customer Data Platform中的身份
description: Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，帮助您更好地了解客户及其行为。
feature: Get Started, Identities
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# 身份概述

Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统桥接身份，帮助您更好地了解客户及其行为。 通常，您的客户会通过多个渠道与您的品牌互动，这可能包括在线浏览您的网站、在店内购买、加入您的忠诚度计划或致电技术支持等等。 在这些多个系统中，有一个为该客户创建的标识，[!DNL Identity Service]允许将这些标识集合起来以查看完整图片。

现在，不再是五个单独的客户通过五个不同的渠道与您的品牌互动，而是您可以看到这是同一个客户，您可以确保他们通过每次互动获得一致、个性化的相关体验。 随着有关您客户的更多信息逐渐为人所知（例如，您网站的匿名浏览器决定注册一个帐户并登录），该信息将拼合在一起，您客户的形象将变得越来越清晰。

## 身份命名空间

身份命名空间是[!DNL Identity Service]的组件，用作为客户身份提供额外上下文的指示器。 例如，“电子邮件”就是常用ID命名空间的例子，通过跨多个网站使用相同的电子邮件地址，您可以将多个不同的身份（每个身份具有唯一的客户ID）拼接在一起，因为实际上属于同一个客户。 [!DNL Experience Platform]允许您使用ID命名空间在用户界面中搜索各个配置文件。 有关查看配置文件的详细信息，请参阅[配置文件浏览概述](profile-browse.md)。 若要了解有关身份命名空间的更多信息，请参阅[身份命名空间概述](../../identity-service/features/namespaces.md)。

## 身份图

身份图是不同身份之间关系的映射，它为您提供了客户如何跨不同渠道与您的品牌互动的可视表示形式。 所有客户身份图由Identity Service集体管理和更新，以响应客户活动。

[!DNL Identity Service]管理仅对您的组织可见的基于您的数据的身份图。 当摄取的数据记录包含多个标识时，[!DNL Identity Service]会增强您的图形，从而添加找到的标识之间的关系。

## 后续步骤

标识以及它们之间的关系，由[!DNL Identity Service]定义和维护，并由[!DNL Real-Time Customer Profile]用来构建每个客户及其交互的完整图景。 若要了解详细信息，请访问[Identity Service文档](../../identity-service/home.md)。
