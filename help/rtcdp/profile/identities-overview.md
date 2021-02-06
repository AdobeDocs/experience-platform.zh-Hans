---
keywords: 标识rtcdp;rtcdp标识；实时cdp标识
title: 实时客户数据平台中的身份
description: Adobe Experience Platform身份服务通过跨设备和系统连接身份来帮助您更好地视图客户及其行为。
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---


# 实时客户数据平台中的身份

Adobe Experience Platform[!DNL Identity Service]通过跨设备和系统连接身份，帮助您更好地视图客户及其行为。 通常，您的客户会跨多个渠道与您的品牌互动，这可能包括在线浏览您的网站、在店内购买、加入您的忠诚度项目或致电帮助台寻求支持等。 在这些多个系统中，为该客户创建了一个标识，[!DNL Identity Service]使这些标识能够整合在一起，看到完整的图景。

现在，您可以看到这是同一个客户，而不是五个不同渠道中与您的品牌互动的五个不同客户，而且您可以确保他们通过每次互动获得一致、个性化的相关体验。 随着关于客户的更多信息（例如，您网站的匿名浏览器决定注册一个帐户并登录），信息会被拼接在一起，客户的形象也变得越来越清晰。

## 身份命名空间

身份命名空间是[!DNL Identity Service]的一个组件，并作为为客户身份提供附加上下文的指标。 常用ID命名空间的示例为“电子邮件”，在多个网站中使用同一电子邮件地址可以拼接多个不同的身份，每个身份都具有一个唯一的客户ID，实际上属于同一个客户。 [!DNL Experience Platform] 允许您使用ID命名空间在用户界面中搜索单个用户档案。有关查看用户档案的详细信息，请参阅[用户档案查看器概述](/help/rtcdp/profile/profile-viewer.md)。 要进一步了解身份命名空间，请参阅[身份命名空间概述](../../identity-service/namespaces.md)。

## 标识图

标识图是不同标识命名空间之间关系的映射，可直观地展示不同渠道中客户如何与您的品牌互动。 所有客户身份图由[!DNL Identity Service]以接近实时方式集中管理和更新，以响应客户活动。

[!DNL Identity Service] 管理仅由您的组织可见的、基于您的数据（称为私有图）构建的标识图。[!DNL Identity Service] 当所摄取的数据记录包含多个身份时增加您的私人图表，并在找到的身份之间添加关系。

## 后续步骤

身份及其之间的关系由[!DNL Identity Service]定义和维护，并由[!DNL Real-time Customer Profile]利用，以全面了解每位客户及其交互。 要了解更多信息，请访问[Identity Service文档](../../identity-service/home.md)。