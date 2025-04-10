---
title: 使用UI将PostgreSQL连接到Experience Platform
description: 了解如何使用Experience Platform用户界面中的源工作区将PostgreSQL数据库连接到Experience Platform。
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: 8cabf1cb86993fdde37d0b9d957f6c8ec23bb237
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# 使用UI将[!DNL PostgreSQL]连接到Experience Platform

阅读本指南，了解如何使用Experience Platform用户界面中的源工作区将您的[!DNL PostgreSQL]数据库连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL PostgreSQL]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

有关身份验证的更多信息，请阅读[[!DNL PostgreSQL] 概述](../../../../connectors/databases/postgres.md)。

### 为连接字符串启用SSL加密

您可以为[!DNL PostgreSQL]连接字符串启用SSL加密，方法是使用以下属性附加连接字符串：

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `EncryptionMethod` | 允许您对[!DNL PostgreSQL]数据启用SSL加密。 | <uL><li>`EncryptionMethod=0`（已禁用）</li><li>`EncryptionMethod=1`（已启用）</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 在应用`EncryptionMethod`时验证[!DNL PostgreSQL]数据库发送的证书。 | <uL><li>`ValidationServerCertificate=0`（已禁用）</li><li>`ValidationServerCertificate=1`（已启用）</li></ul> |

以下是附加了SSL加密的[!DNL PostgreSQL]连接字符串的示例： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`。

## 导航源目录 {#navigate}

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;*[!UICONTROL 源]*&#x200B;工作区。 在&#x200B;*[!UICONTROL 类别]*&#x200B;面板中选择相应的类别或者，使用搜索栏导航到要使用的特定源。

若要使用[!DNL PostgreSQL]，请选择&#x200B;*[!UICONTROL 数据库]*&#x200B;下的&#x200B;**[!UICONTROL PostgreSQL]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 设置]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 创建经过身份验证的帐户后，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。



## 使用现有帐户 {#existing}

若要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后选择要使用的[!DNL PostgreSQL]帐户。

![源工作流的现有帐户接口。](../../../../images/tutorials/create/postgresql/catalog.png)

## 创建新帐户 {#create}

如果您没有现有帐户，则必须通过提供与您的源对应的必需身份验证凭据来创建新帐户。

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供名称并选择性地为您的帐户添加描述。

![源工作流中的新帐户接口，提供了帐户名称和可选描述。](../../../../images/tutorials/create/postgresql/existing.png)

### 连接到Azure上的Experience Platform {#azure}

您可以使用帐户密钥或基本身份验证将您的[!DNL PostgreSQL]帐户连接到Azure上的Experience Platform。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

若要使用帐户密钥身份验证，请选择&#x200B;**[!UICONTROL 帐户密钥身份验证]**，提供您的[连接字符串](../../../../connectors/databases/postgres.md#azure)，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![源工作流中的新帐户接口已选择“帐户密钥身份验证”。](../../../../images/tutorials/create/postgresql/account-key.png)

>[!TAB 基本身份验证]

若要使用基本身份验证，请选择&#x200B;**[!UICONTROL 基本身份验证]**，提供[身份验证凭据](../../../../connectors/databases/postgres.md#azure)的值，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![源工作流程中的新帐户接口选择了“基本身份验证”。](../../../../images/tutorials/create/postgresql/basic-auth.png)

>[!ENDTABS]

### 连接到Amazon Web Services上的Experience Platform (AWS) {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

要创建新的[!DNL PostgreSQL]帐户并连接到AWS上的Experience Platform，请确保您处于VA6沙盒中，然后提供身份验证所需的[凭据](../../../../connectors/databases/postgres.md#aws)。

![源工作流中用于连接到AWS的新帐户接口。](../../../../images/tutorials/create/postgresql/basic-auth.png)

## 为您的[!DNL PostgreSQL]数据创建数据流

通过学习本教程，您已建立与[!DNL MariaDB]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Experience Platform](../../dataflow/databases.md)。
