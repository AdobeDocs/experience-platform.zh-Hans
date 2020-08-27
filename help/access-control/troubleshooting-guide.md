---
keywords: Experience Platform;home;popular topics;troubleshooting;access control
solution: Experience Platform
title: 访问控制疑难解答指南
topic: troubleshooting guide
description: 本文档提供有关Adobe Experience Platform访问控制的常见问题解答。
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# 访问控制疑难解答指南

本文档提供有关Adobe Experience Platform访问控制的常见问题解答。 有关其他服务的问题和疑 [!DNL Platform] 难解答，请参阅Experience Platform [疑难解答指南](../landing/troubleshooting.md)。

[!DNL Experience Platform] 利用Adobe Admin Console的产品 [用户档案](http://adminconsole.adobe.com) ，提供基于角色 **的访问控制**，将用户与权限和沙箱关联起来。  有关更多 [信息](home.md) ，请参阅访问控制概述。

## 在哪里可以找到我当前的访问权限？

如果您是IMS组织的系统管理员、产品管理员或产品用户档案管理员，您可以视图您分配的产品用户档案及其在Adobe Admin Console内提供的权限。 有关如何 [导航到访问控制](./ui/overview.md) ，请参阅用户指南 [!DNL Admin Console] ，以获取有关如何导航到视图产品用户档案权限的说明。

如果您不是管理员，您仍可以通过向视图API中的端点发送请求来访问控制您 `/acl/effective-policies` 当前的访问权限。 有关详细信息，请参阅视图开发人 [员指南中的](./api/effective-policies.md) “访问控制有效策略”部分。

## UI中的某些 [!DNL Platform] 功能不可用。 权限如何控制对这些功能的访问？

如果您对特定功能没有访问权限， [!DNL Platform] 则该功能将在UI中被隐藏或灰显 [!DNL Experience Platform] 。 例如，要视图“[!UICONTROL 用户档案]”选项卡，您必须具有“[!UICONTROL 视图用户档案]”或“管[!UICONTROL 理用户档案]”权限。 如果您需要其他权限才能使用功能，请与您的管 [!DNL Experience Platform] 理员联系。

## 权限分组方式，以及哪个组包含要使用的权限？

权限按权限所应用的 [!DNL Platform] 功能（如和）进行分 [!DNL Data Management] 组和 [!DNL Profile Management]分类。 有关可用权限及其所属组的完整列表，请参阅 [访问控制概述](home.md#permissions) 中的权限部分。

有关提供 [基于角色的访问控制](home.md) ，请参阅访问控制概述。