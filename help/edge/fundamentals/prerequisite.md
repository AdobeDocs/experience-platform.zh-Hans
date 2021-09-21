---
title: 使用Adobe Experience Platform Web SDK的先决条件
description: 了解使用Adobe Experience Platform Web SDK的先决条件。
keywords: 第一方域；CNAME；架构；创建架构；启动；aep web sdk扩展；扩展；配置ID；配置工具；数据元素；创建数据元素；XDM对象；sendEvent；发送事件；
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 9d3965be1956de754f0d2a82178bf5dcd871e239
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# 使用Adobe Experience Platform Web SDK的先决条件

要使用Platform Web SDK，您必须首先：

- 已为此功能配置您的组织。 (如果您想要获取访问权限，可免费访问平台Web SDK，请联系您的客户成功经理(CSM)。)
- 建议启用第一方域(CNAME)。 如果您已经拥有Adobe Analytics的CNAME，则应使用该CNAME。 在开发中测试无需CNAME即可运行，但Adobe建议在您投入生产之前先测试一次。 尽管CNAME实施在Cookie生命周期方面不提供任何好处，但它可能会阻止某些广告阻止程序和不太常见的浏览器阻止SDK请求。 在这些情况下，使用CNAME可能会阻止使用这些工具的用户中断您的数据收集。

>[!IMPORTANT]
>
>**请注意，自11/10/20起，第一方CNAME实施在所有Safari浏览器和移动iOS设备上的7天到期。**

- 有权访问Adobe Experience Platform。 如果您尚未购买Adobe Experience Platform,Adobe将为您配置必要的访问权限，以便您在SDK中有限地使用，而无需额外付费。
- 如果您的网站已在您的网站上使用[Experience CloudID服务](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html)(通过Adobe Experience Platform Launch中的访客API或Experience CloudID服务扩展)，并且您希望在迁移到Adobe Experience Platform Web SDK时继续使用它，则您必须使用最新版本的访客API或Experience CloudID服务扩展。 有关更多信息，请参阅[ID迁移](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) 。

## 管理Adobe Experience Platform Web SDK的权限

使用Adobe Experience Platform不需要任何特殊权限，但您需要拥有[权限](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=zh-Hans)才能在Adobe Experience Platform中创建架构。 需要的最低权限可在数据建模和身份类别中找到。

![](../images/AEP-permission-categories.png)

在数据建模类别中，授予用户管理架构和查看架构权限。

![](../images/data-modeling-permissions.png)

在Identity Management类别中，授予用户“管理身份命名空间”和“查看身份命名空间”权限。

![](../images/identity-management-permissions.png)
