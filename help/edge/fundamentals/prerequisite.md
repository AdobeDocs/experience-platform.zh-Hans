---
title: 使用Adobe Experience Platform Web SDK的先决条件
description: 了解使用Adobe Experience Platform Web SDK的先决条件。
keywords: 第一方域；CNAME；架构；创建架构；启动；aep web sdk扩展；扩展；配置ID；配置工具；数据元素；创建数据元素；XDM对象；sendEvent；发送事件；
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 6a9882224cba08718c81a3aead237107b3e47726
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 使用Adobe Experience Platform Web SDK的先决条件

要使用Adobe Experience Platform Web SDK，您必须先：

- 为组织中的用户配置了正确的权限。 所有Experience Cloud客户都有权访问数据收集工具，您组织中的每个用户只需要拥有架构、身份和数据流的权限。 要阅读有关如何设置这些权限的更多信息，请参阅 [数据收集权限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
- 建议启用第一方域(CNAME)。 如果您已经拥有Adobe Analytics的CNAME，则应使用该CNAME。 在开发中测试无需CNAME即可运行，但Adobe建议在您投入生产之前先测试一次。 尽管CNAME实施在Cookie生命周期方面不提供任何好处，但它可能会阻止某些广告阻止程序和不太常见的浏览器阻止SDK请求。 在这些情况下，使用CNAME可能会阻止使用这些工具的用户中断您的数据收集。

>[!IMPORTANT]
>
>**请注意，自11/10/20起，第一方CNAME实施在所有Safari浏览器和移动iOS设备上的7天到期。**

- 如果您的网站已在使用 [Experience CloudID服务](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) 在您的网站上(通过Adobe Experience Platform Launch中的访客API或Experience CloudID服务扩展)，并且您希望在迁移到Adobe Experience Platform Web SDK时继续使用它，您必须使用最新版本的访客API或Experience CloudID服务扩展。 请参阅 [ID迁移](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) 以了解更多信息。
