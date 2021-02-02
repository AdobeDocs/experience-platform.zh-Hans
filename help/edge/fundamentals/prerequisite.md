---
title: 使用Adobe Experience PlatformWeb SDK的先决条件
seo-title: 使用Adobe Experience PlatformWeb SDK的先决条件
description: 使用Adobe Experience PlatformWeb SDK的先决条件
seo-description: 使用Adobe Experience PlatformWeb SDK的先决条件
keywords: 第一方域；CNAME;模式；创建模式；启动；aep web sdk扩展；扩展；配置id；配置工具；数据元素；创建数据元素；XDM对象；sendEvent；发送事件;
translation-type: tm+mt
source-git-commit: a19b4384e2ea64eb9ab5f0f5443fd329ec44a2a0
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# 使用Adobe Experience PlatformWeb SDK的先决条件

要使用Platform Web SDK，您必须首先：

- 让您的组织配置此功能。 (如果您想要访问平台Web SDK，可免费访问平台Web SDK，请联系您的客户成功经理(CSM)。
- 启用第一方域(CNAME)。 如果您已经有Adobe Analytics的CNAME，您应该使用它。 在开发中进行测试没有CNAME，但您在开始生产之前需要一个CNAME。

>[!IMPORTANT]
>
>**请注意，自2020年11月10日起，第一方CNAME实施在所有Safari浏览器和移动iOS设备上都有7天的期限。**

- 有权获得Adobe Experience Platform。 如果您尚未购买Adobe Experience Platform,Adobe将为您提供必要的访问权，以在SDK中有限地使用，而无需额外付费。
- 如果您的网站已在您的网站上使用[Experience CloudID服务](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html)(通过访客API或Adobe Experience Platform Launch的Experience CloudID服务扩展)，并且您希望在迁移到Adobe Experience PlatformWeb SDK时继续使用它，您必须使用最新版访客API或Experience CloudID服务扩展。 有关详细信息，请参阅[ID迁移](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity)。
