---
keywords: Experience Platform；主页；热门主题；疑难解答；访问控制
solution: Experience Platform
title: 访问控制疑难解答指南
description: 本文档提供有关Adobe Experience Platform中访问控制的常见问题解答。
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 访问控制疑难解答指南

本文档提供有关Adobe Experience Platform中访问控制的常见问题解答。 有关其他[!DNL Experience Platform]服务的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

[!DNL Experience Platform]利用[Adobe Admin Console](https://adminconsole.adobe.com)中的产品配置文件来提供基于角色的访问控制，从而将用户与权限和沙盒关联起来。  有关详细信息，请参阅[访问控制概述](home.md)。

## 在哪里可以找到我当前的访问权限？

如果您是组织的系统管理员、产品管理员或产品配置文件管理员，则可以在Adobe Admin Console中查看分配的产品配置文件及其提供的权限。 有关如何导航[!DNL Admin Console]以查看产品配置文件的权限的说明，请参阅[访问控制用户指南](./ui/overview.md)。

如果您不是管理员，则仍可以通过向访问控制API中的`/acl/effective-policies`端点发送请求来查看您当前的访问权限。 有关详细信息，请参阅[访问控制开发人员指南](./api/effective-policies.md)中的“查看有效策略”部分。

## [!DNL Experience Platform] UI中的某些功能不可用。 对这些功能的访问如何受权限控制？

如果您没有特定[!DNL Experience Platform]功能的访问权限，则该功能将在[!DNL Experience Platform] UI中隐藏或灰显。 例如，要查看“[!UICONTROL 配置文件]”选项卡，您必须具有“[!UICONTROL 查看配置文件]”或“[!UICONTROL 管理配置文件]”权限。 如果您需要[!DNL Experience Platform]功能的附加权限，请联系您的管理员。

## 权限如何分组，哪个组包含我想使用的权限？

权限按其应用的[!DNL Experience Platform]功能（如[!DNL Data Management]和[!DNL Profile Management]）进行分组和分类。 有关可用权限及其所属组的完整列表，请参阅访问控制概述中的[权限部分](home.md#permissions)。

有关提供基于角色的访问控制的详细信息，请参阅[访问控制概述](home.md)。

## 从Adobe IO迁移到Business ID后，权限会发生什么情况？

访问控制使用用户ID（分配给用户的内部唯一ID）来授予权限。 当组织从Adobe ID迁移到Business ID时，为其用户设置的所有权限将丢失，因为用户ID发生更改，访问控制将使用新生成的用户ID。 如果贵组织迁移到Business ID，请联系Adobe代表以将用户ID从Adobe ID迁移到Business ID。
