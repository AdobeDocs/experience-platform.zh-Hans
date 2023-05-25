---
keywords: Experience Platform；主页；热门主题；[!DNL PostgreSQL]；[!DNL PostgreSQL]；PostgreSQL
solution: Experience Platform
title: 在UI中创建PostgreSQL源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建PostgreSQL源连接。
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---

# 创建 [!DNL PostgreSQL] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了用于创建 [!DNL PostgreSQL] 源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL PostgreSQL] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

要访问您的 [!DNL PostgreSQL] 帐户于 [!DNL Platform]，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的关联的连接字符串 [!DNL PostgreSQL] 帐户。 此 [!DNL PostgreSQL] 连接字符串模式为： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

有关入门的更多信息，请参阅此 [[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/9.2/app-psql.html).

#### 为连接字符串启用SSL加密

您可以为启用SSL加密 [!DNL PostgreSQL] 连接字符串，方法是：将连接字符串附加到以下属性：

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `EncryptionMethod` | 允许您对启用SSL加密 [!DNL PostgreSQL] 数据。 | <uL><li>`EncryptionMethod=0`(已禁用)</li><li>`EncryptionMethod=1`(已启用)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 验证由您发送的证书 [!DNL PostgreSQL] 数据库时间 `EncryptionMethod` 中所有规则都适用的URL的区域。 | <uL><li>`ValidationServerCertificate=0`(已禁用)</li><li>`ValidationServerCertificate=1`(已启用)</li></ul> |

以下示例为 [!DNL PostgreSQL] 附加了SSL加密的连接字符串： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## 连接您的 [!DNL PostgreSQL] 帐户

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL PostgreSQL] 目标帐户 [!DNL Platform].

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 以访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL PostgreSQL数据库]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 以新建 [!DNL PostgreSQL] 连接器。

![](../../../../images/tutorials/create/postgresql/catalog.png)

此 **[!UICONTROL 连接到[!DNL PostgreSQL]]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL PostgreSQL] 凭据。 完成后，选择 **[!UICONTROL Connect]** 然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/postgresql/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL PostgreSQL] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/postgresql/existing.png)

## 后续步骤

按照本教程，您已建立与的连接 [!DNL PostgreSQL] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md).
