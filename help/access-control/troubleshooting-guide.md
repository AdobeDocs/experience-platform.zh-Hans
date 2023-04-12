---
keywords: Experience Platform；主页；热门主题；故障诊断；访问控制
solution: Experience Platform
title: 访问控制疑难解答指南
description: 本文档提供了有关Adobe Experience Platform中访问控制的常见问题解答。
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# 访问控制疑难解答指南

本文档提供了有关Adobe Experience Platform中访问控制的常见问题解答。 有关与其他 [!DNL Platform] 服务，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

[!DNL Experience Platform] 利用 [Adobe Admin Console](https://adminconsole.adobe.com) 要提供基于角色的访问控制，请将用户与权限和沙箱关联起来。  请参阅 [访问控制概述](home.md) 以了解更多信息。

## 在哪里可以找到我当前的访问权限？

如果您是您组织的系统管理员、产品管理员或产品配置文件管理员，则可以查看您分配的产品配置文件及其在Adobe Admin Console中提供的权限。 请参阅 [访问控制用户指南](./ui/overview.md) 有关如何导航的说明 [!DNL Admin Console] 查看产品配置文件的权限。

如果您不是管理员，则仍可以通过向 `/acl/effective-policies` 访问控制API中的端点。 请参阅 [访问控制开发人员指南](./api/effective-policies.md) 以了解更多信息。

## 中的一些功能 [!DNL Platform] UI不可用。 权限如何控制对这些功能的访问？

如果您没有特定 [!DNL Platform] 功能，该功能将在 [!DNL Experience Platform] UI。 例如，为了查看[!UICONTROL 用户档案]“ ”选项卡，您必须具有[!UICONTROL 查看配置文件]&quot;或&quot;[!UICONTROL 管理配置文件]“权限”。 如果您需要其他权限，请联系您的管理员 [!DNL Experience Platform] 功能。

## 权限分组方式，以及哪个组包含要使用的权限？

权限按 [!DNL Platform] (例如 [!DNL Data Management] 和 [!DNL Profile Management])。 有关可用权限及其所属群组的完整列表，请参阅 [权限部分](home.md#permissions) 在访问控制概述中。

请参阅 [访问控制概述](home.md) 以了解有关提供基于角色的访问控制的更多信息。

## 从AdobeIO迁移到业务ID后，权限会发生什么情况？

访问控制使用用户ID（分配给用户的内部唯一ID）来授予权限。 将组织从Adobe ID迁移到业务ID后，为其用户设置的所有权限都将丢失，因为用户ID会发生更改，而访问控制将使用新生成的用户ID。 如果贵组织已迁移到业务ID，请联系您的Adobe代表，将您的用户ID从Adobe ID迁移到业务ID。
