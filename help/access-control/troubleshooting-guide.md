---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 访问控制疑难解答指南
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa

---


# 访问控制疑难解答指南

本文档为有关Adobe Experience Platform中访问控制的常见问题解答。 有关其他平台服务的问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md)。

Experience Platform利用 [Adobe Admin Console中的产品用户档案](http://adminconsole.adobe.com) ，提供基于角色的 **访问控制**，将用户与权限和沙箱关联起来。  有关详细 [信息，请参阅访问控制](home.md) 概述。

## 在哪里可以找到我的当前访问权限？

如果您是IMS组织的系统管理员、产品管理员或产品用户档案管理员，则可以视图您分配的产品用户档案及其在Adobe Admin Console中提供的权限。 有关如 [何导航Admin Console以访问控制产品用户档案权限的说明](./ui/overview.md) ，请参阅视图用户指南。

如果您不是管理员，您仍可以通过向视图API中的端点发送请求来访问控制当前 `/acl/effective-policies` 的访问权限。 有关详细信息，请参阅视图开发人员指南中 [的“访问控制有效策略](./api/effective-policies.md) ”一节。

## 平台UI中的某些功能不可用。 权限如何控制对这些功能的访问？

如果您没有特定平台功能的访问权限，该功能将在Experience Platform UI中隐藏或灰显。 例如，要视图“用户档案”选项卡，您必须具有“视图用户档案”或“管理用户档案”权限。 如果您需要Experience Platform功能的其他权限，请与管理员联系。

## 如何分组权限，以及哪个组包含要使用的权限？

权限按其适用的平台功能(如数据管理和用户档案管理)进行分组和分类。 有关可用权限及其所属组的完整列表，请参阅访问控制概 [述中的](home.md#permissions) “权限”部分。

有关提供 [基于角色的访问控制](home.md) ，请参阅访问控制概述。