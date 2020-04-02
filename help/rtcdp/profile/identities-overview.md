---
title: 身份与身份命名空间
seo-title: Adobe Experience Platform Identity Service
description: 描述
seo-description: seo描述
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# 实时CDP中的身份

Adobe Experience Platform Identity Service通过跨设备和系统连接身份，帮助您更好地视图客户及其行为。 通常，您的客户在多个渠道中与您的品牌互动，这包括在线浏览您的网站、在店内购买、加入您的忠诚度项目或致电技术支持等。 在这些多个系统中，为该客户创建了一个标识，而Identity Service使这些标识能够整合在一起，从而看到完整的图景。

现在，您可以看到，这是同一个客户，而不是五个不同渠道中与您的品牌互动的五个单独客户，并且您可以确保他们通过每次互动获得一致、个性化的相关体验。 随着更多关于客户的信息（例如，您网站的匿名浏览器决定注册一个帐户并登录），信息会被拼接在一起，客户的形象也变得越来越清晰。

## 身份命名空间

身份命名空间是身份服务的一个组成部分，并作为为客户身份提供附加上下文的指标。 通常使用的ID命名空间的示例为“电子邮件”，在多个网站中使用相同的电子邮件地址可以将多个不同的身份拼合在一起，每个身份都具有一个唯一的客户ID，实际上属于同一客户。 Experience Platform允许您使用ID命名空间在用户界面中搜索各个用户档案。 有关查看用户档案的详细信息，请参阅 [用户档案查看器概述](/help/rtcdp/profile/profile-viewer.md)。 要进一步了解身份命名空间，请参阅身份 [命名空间概述](../../identity-service/namespaces.md)。

## 标识图

标识图是不同标识命名空间之间关系的映射，可直观地呈现客户如何跨不同渠道与品牌互动。 所有客户标识图由Identity Service以近乎实时的方式统一管理和更新，以响应客户活动。

Identity Service管理仅由您的组织可见并基于您的数据（称为专用图）构建的标识图。 当所摄取的数据记录包含多个标识时，Identity Service会增强您的专用图形，从而在找到的标识之间添加关系。

## 后续步骤

身份及其间的关系由Identity Service定义和维护，并由实时客户用户档案利用，以全面了解每位客户及其交互。 要了解更多信息，请访问 [Identity Service文档](../../identity-service/home.md)。