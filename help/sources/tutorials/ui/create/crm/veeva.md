---
keywords: Experience Platform；主页；热门主题；Veeva CRM;Veeva
solution: Experience Platform
title: 在UI中创建Veeva CRM源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Veeva CRM源连接。
exl-id: 4ef76c28-9bd2-4e54-a3d6-dceb89162337
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 1%

---

# 创建 [!DNL Veeva CRM] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源CRM数据的功能。 本教程提供了创建 [!DNL Veeva CRM] 源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有 [!DNL Veeva CRM] 帐户，您可以跳过本文档的其余部分，并继续阅读本教程 [配置数据流](../../dataflow/crm.md).

### 收集所需的凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | 的URL [!DNL Veeva CRM] 源实例。 |
| `username` | 的用户名 [!DNL Veeva CRM] 用户帐户。 |
| `password` | 的密码 [!DNL Veeva CRM] 用户帐户。 |
| `securityToken` | 的安全令牌 [!DNL Veeva CRM] 用户帐户。 |

有关入门的更多信息，请参阅此 [[!DNL Veeva CRM] 文档](https://developer.veevacrm.com/doc/Content/rest-api.htm).

## 连接 [!DNL Veeva CRM] 帐户

收集所需的凭据后，您可以按照以下步骤链接 [!DNL Veeva CRM] 帐户 [!DNL Platform].

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 [!UICONTROL CRM] 类别，选择 **[!UICONTROL Veeva CRM]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/veeva/catalog.png)

的 **[!UICONTROL 连接Veeva CRM帐户]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Veeva CRM] 创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/veeva/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供名称、可选描述以及 [!DNL Veeva CRM] 凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![新建](../../../../images/tutorials/create/veeva/new.png)

## 后续步骤

通过阅读本教程，您已经与 [!DNL Veeva CRM] 帐户。 您现在可以继续下一个教程和 [配置数据流以将数据导入平台](../../dataflow/crm.md).
