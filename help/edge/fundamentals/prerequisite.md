---
title: 使用Adobe Experience Platform Web SDK的先决条件
description: 了解使用Adobe Experience Platform Web SDK的先决条件。
keywords: 第一方域；CNAME;模式；创建模式；启动；aep web sdk扩展；扩展；配置id；配置工具；数据元素；创建数据元素；XDM对象；sendEvent；发送事件;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# 使用Adobe Experience Platform Web SDK的先决条件

要使用Platform Web SDK，您必须首先：

- 让您的组织配置此功能。 (如果您希望访问Platform Web SDK，可免费访问Platform Web SDK，请联系您的客户成功经理(CSM)。
- 启用第一方域(CNAME)。 如果您已经有Adobe Analytics的CNAME，则应使用该CNAME。 在开发中测试无需CNAME即可工作，但在开始生产之前您需要测试。

>[!IMPORTANT]
>
>**请注意，截至11/10/20，第1方CNAME实施在所有Safari浏览器和移动iOS设备上具有7天的期限。**

- 有权访问Adobe Experience Platform。 如果您尚未购买Adobe Experience Platform,Adobe将为您提供使用SDK以有限方式使用的必要访问权，而不收取任何额外费用。
- 如果您的网站已在您的网站上使用[Experience CloudID服务](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html)(通过访客 API或Adobe Experience Platform Launch中的Experience CloudID服务扩展)，并且您希望在迁移到Adobe Experience Platform Web SDK时继续使用它，则您必须使用最新版本的访客API或Experience CloudID服务扩展。 有关详细信息，请参阅[ID迁移](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity)。
