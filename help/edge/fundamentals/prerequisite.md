---
title: 使用Adobe Experience Platform Web SDK的先决条件
description: 了解使用Adobe Experience Platform Web SDK的先决条件。
keywords: 第一方域；CNAME；架构；创建架构；启动项；aep web sdk扩展；扩展；配置ID；配置工具；数据元素；创建数据元素；XDM对象；sendEvent；发送事件；
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 使用Adobe Experience Platform Web SDK的先决条件

要使用Adobe Experience Platform Web SDK，您必须首先：

- 为您的组织中的用户配置了正确的权限。 所有Experience Cloud客户都可以访问数据收集工具，贵组织中的每位用户只需要架构、身份和数据流的权限。 要阅读有关如何设置这些权限的更多信息，请参阅我们的文档，其网址为 [数据收集权限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).
- 建议启用第一方域(CNAME)。 如果您已拥有Adobe Analytics的CNAME，则应该使用该CNAME。 开发中的测试无需使用CNAME即可运行，但Adobe建议在进入生产阶段之前使用一个CNAME。 尽管CNAME实施在Cookie生命周期方面没有任何好处，但它可以阻止某些广告阻止程序和不太常见的浏览器阻止SDK请求。 在这些情况下，使用CNAME可以在对使用这些工具的用户进行数据收集时防止中断。

>[!IMPORTANT]
>
>**请注意，自2020年11月10日起，所有Safari浏览器和移动iOS设备上的第一方CNAME实施都将维持7天的有效期。**

- 如果您的网站已经在使用 [Experience CloudID服务](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) 在您的网站上(通过访客API或Adobe Experience Platform Launch中的Experience CloudID服务扩展)，如果您希望在迁移到Adobe Experience Platform Web SDK时继续使用它，则必须使用最新版本的访客API或Experience CloudID服务扩展。 请参阅 [ID迁移](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#identity) 以了解更多信息。
