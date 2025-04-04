---
keywords: Experience Platform；主页；热门主题；[!DNL PostgreSQL]；[!DNL PostgreSQL]；PostgreSQL
solution: Experience Platform
title: 在UI中创建PostgreSQL Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建PostgreSQL源连接。
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 2%

---

# 在用户界面中创建[!DNL PostgreSQL]源连接

Adobe Experience Platform中的Source连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用[!DNL Experience Platform]用户界面创建[!DNL PostgreSQL]源连接器的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL PostgreSQL]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

要在[!DNL Experience Platform]上访问您的[!DNL PostgreSQL]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的[!DNL PostgreSQL]帐户关联的连接字符串。 [!DNL PostgreSQL]连接字符串模式为： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |

有关入门的详细信息，请参阅此[[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/9.2/app-psql.html)。

#### 为连接字符串启用SSL加密

您可以为[!DNL PostgreSQL]连接字符串启用SSL加密，方法是使用以下属性附加连接字符串：

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `EncryptionMethod` | 允许您对[!DNL PostgreSQL]数据启用SSL加密。 | <uL><li>`EncryptionMethod=0`（已禁用）</li><li>`EncryptionMethod=1`（已启用）</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 在应用`EncryptionMethod`时验证[!DNL PostgreSQL]数据库发送的证书。 | <uL><li>`ValidationServerCertificate=0`（已禁用）</li><li>`ValidationServerCertificate=1`（已启用）</li></ul> |

以下是附加了SSL加密的[!DNL PostgreSQL]连接字符串的示例： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`。

## 连接您的[!DNL PostgreSQL]帐户

收集所需的凭据后，您可以按照以下步骤将您的[!DNL PostgreSQL]帐户关联到[!DNL Experience Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!UICONTROL 数据库]**&#x200B;类别下，选择&#x200B;**[!UICONTROL PostgreSQL DB]**。 如果这是您第一次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的[!DNL PostgreSQL]连接器。

![](../../../../images/tutorials/create/postgresql/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到[!DNL PostgreSQL]]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL PostgreSQL]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/postgresql/new.png)

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL PostgreSQL]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/postgresql/existing.png)

## 后续步骤

通过学习本教程，您已建立与[!DNL PostgreSQL]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入 [!DNL Experience Platform]](../../dataflow/databases.md)。
