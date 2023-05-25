---
keywords: 身份rtcdp；rtcdp身份；real-time cdp身份
title: Real-time Customer Data Platform中的身份
description: Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，帮助您更好地了解客户及其行为。
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# 身份概述

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统桥接身份，帮助您更好地了解客户及其行为。 通常，您的客户会通过多个渠道与您的品牌互动，这可以包括在线浏览您的网站、在店内购买商品、加入您的忠诚度计划或致电技术支持等。 在这些多个系统中，会为该客户创建一个标识，并且 [!DNL Identity Service] 使将这些标识集合在一起看完整情况成为可能。

现在，您可以看到这是同一客户，而不是五个单独的客户通过五个不同的渠道与您的品牌进行交互，并且您可以确保他们通过每次交互获得一致、个性化的相关体验。 随着有关您客户的更多信息逐渐为人所知（例如，您网站的匿名浏览器决定注册一个帐户并登录），该信息将拼合在一起，而您客户的照片将变得越来越清晰。

## 身份命名空间

身份命名空间是的组件 [!DNL Identity Service] 和用作为客户身份提供额外上下文的指示器。 例如，常见的ID命名空间是“电子邮件”，其中在多个网站中使用相同的电子邮件地址，使您能够拼合多个不同的身份，每个身份具有唯一的客户ID，并且实际上属于同一个客户。 [!DNL Experience Platform] 允许您使用ID命名空间在用户界面中搜索各个配置文件。 有关查看用户档案的更多信息，请参阅 [配置文件浏览概述](profile-browse.md). 要了解有关身份命名空间的更多信息，请参阅 [身份命名空间概述](../../identity-service/namespaces.md).

## 身份图

身份图是不同身份命名空间之间关系的映射，为您提供客户如何通过不同渠道与您的品牌进行交互的可视表示形式。 所有客户标识图都由进行统一管理和更新 [!DNL Identity Service] 近乎实时地，响应客户活动。

[!DNL Identity Service] 管理仅对您的组织可见并且基于您的数据构建的标识图，称为专用图。 [!DNL Identity Service] 当摄取的数据记录包含多个标识时，可增强专用图，从而添加找到的标识之间的关系。

## 后续步骤

身份以及它们之间的关系，由来定义和维护 [!DNL Identity Service] 利用者 [!DNL Real-Time Customer Profile] 以全面了解每个客户及其交互。 欲了解更多信息，请访问 [Identity Service文档](../../identity-service/home.md).
