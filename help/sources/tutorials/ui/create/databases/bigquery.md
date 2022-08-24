---
keywords: Experience Platform；主页；热门主题；Google Big Query;google big query;GBQ;gbq
solution: Experience Platform
title: 在UI中创建Google大查询源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Google UI创建Adobe Experience Platform大查询源连接。
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 015a4fa06fc2157bb8374228380bb31826add37e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 创建 [!DNL Google Big Query] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了创建 [!DNL Google Big Query] 源连接。

## 快速入门

本教程需要对Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有 [!DNL Google BigQuery] 连接时，您可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

为了访问 [!DNL Google BigQuery] 帐户，您必须提供以下OAuth 2.0身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `project` | 默认项目ID [!DNL Google BigQuery] 要查询的项目。 |
| `clientID` | 用于生成刷新令牌的ID值。 |
| `clientSecret` | 用于生成刷新令牌的密钥值。 |
| `refreshToken` | 从获取的刷新令牌 [!DNL Google] 用于授权访问 [!DNL Google BigQuery]. |

有关这些值的更多信息，请参阅 [此 [!DNL Google BigQuery] 文档](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## 连接您的Google BigQuery帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以为其创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL 数据库] 类别，选择 **[!UICONTROL Google BigQuery]** 然后选择 **[!UICONTROL 添加数据]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

的 **[!UICONTROL 连接到Google Big Query]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择 [!DNL Google BigQuery] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/google-big-query/existing.png)

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述以及 [!DNL Google BigQuery] 凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![](../../../../images/tutorials/create/google-big-query/new.png)

## 后续步骤

通过阅读本教程，您已经与 [!DNL Google BigQuery] 帐户。 您现在可以继续下一个教程和 [配置数据流以将数据导入平台](../../dataflow/databases.md).
