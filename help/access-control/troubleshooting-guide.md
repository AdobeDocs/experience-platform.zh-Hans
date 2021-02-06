---
keywords: Experience Platform；主页；热门主题；疑难解答；访问控制
solution: Experience Platform
title: 访问控制疑难解答指南
topic: troubleshooting guide
description: 本文档提供有关Adobe Experience Platform访问控制的常见问题解答。
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# 访问控制疑难解答指南

本文档提供有关Adobe Experience Platform访问控制的常见问题解答。 有关其他[!DNL Platform]服务的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

[!DNL Experience Platform] 利用用户档案Admin Console中 [的产](http://adminconsole.adobe.com) 品Adobe提供基于角色的访问控制，将用户与权限和沙箱关联起来。有关详细信息，请参阅[访问控制概述](home.md)。

## 在哪里可以找到我当前的访问权限？

如果您是IMS组织的系统管理员、产品管理员或产品用户档案管理员，您可以视图您分配的产品用户档案及其在Adobe Admin Console内提供的权限。 有关如何导航[!DNL Admin Console]访问控制用户档案以视图产品权限的说明，请参阅[用户指南](./ui/overview.md)。

如果您不是管理员，您仍可以通过向访问控制API中的`/acl/effective-policies`端点发送请求来视图当前访问权限。 有关详细信息，请参阅[视图开发人员指南](./api/effective-policies.md)中的“访问控制有效策略”部分。

## [!DNL Platform] UI中的某些功能不可用。 权限如何控制对这些功能的访问？

如果您没有特定[!DNL Platform]功能的访问权限，该功能将在[!DNL Experience Platform] UI中隐藏或灰显。 例如，要视图“[!UICONTROL 用户档案]”选项卡，您必须具有“[!UICONTROL 视图用户档案]”或“[!UICONTROL 管理用户档案]”权限。 如果您需要对[!DNL Experience Platform]功能具有其他权限，请与管理员联系。

## 权限分组方式，以及哪个组包含要使用的权限？

权限按其应用的[!DNL Platform]功能（如[!DNL Data Management]和[!DNL Profile Management]）进行分组和分类。 有关可用权限及其所属组的完整列表，请参阅访问控制概述中的[权限部分](home.md#permissions)。

有关提供基于角色的访问控制的详细信息，请参阅[访问控制概述](home.md)。