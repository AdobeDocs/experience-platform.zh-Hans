---
title: 使用Adobe Experience PlatformWeb SDK的先决条件
seo-title: 使用Adobe Experience PlatformWeb SDK的先决条件
description: 使用Adobe Experience PlatformWeb SDK的先决条件
seo-description: 使用Adobe Experience PlatformWeb SDK的先决条件
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: 94b3faf3157f4e1f4e46b6055914a04883dc44fa
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# 使用Adobe Experience PlatformWeb SDK的先决条件

要使用此SDK，您必须首先：

- 为组织配置此功能。 (如果您希望进入等待列表，请联系您的客户成功经理(CSM)。)
- 启用第一方域(CNAME)。 如果您已经有Adobe Analytics的CNAME，您应该使用它。 在开发中进行测试没有CNAME，但您在开始生产之前需要一个CNAME。

>[!IMPORTANT]
>
>**请注意，自2020年11月10日起，第一方CNAME实施在所有Safari浏览器和移动iOS设备上都有7天的期限。**

- 有权获得Adobe Experience Platform。 如果您尚未购买Adobe Experience Platform,Adobe将为您提供Experience Platform数据服务基金会，以便在SDK中以有限方式使用，而不收取额外费用。
- 如果您的网站已在您的网站上使用[Experience CloudID服务](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html)(通过访客API或Adobe Experience Platform Launch的Experience CloudID服务扩展)，并且您希望在迁移到Adobe Experience PlatformWeb SDK时继续使用它，您必须使用最新版访客API或Experience CloudID服务扩展。 有关详细信息，请参阅[ID迁移](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity)。
