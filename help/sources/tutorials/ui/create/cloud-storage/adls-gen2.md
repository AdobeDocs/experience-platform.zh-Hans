---
keywords: Experience Platform；主页；热门主题；Azure Data Lake Storage Gen2；ADLS Gen2；adls gen2；adls连接器
solution: Experience Platform
title: 在UI中创建Azure Data Lake Storage Gen2 Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Azure Data Lake Storage Gen2源连接。
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 2%

---

# 在用户界面中创建[!DNL Azure Data Lake Storage Gen2]源连接

Adobe Experience Platform中的Source连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用[!DNL Experience Platform]用户界面验证[!DNL Azure Data Lake Storage Gen2]（以下称为“[!DNL ADLS Gen2]”）源连接器的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   - [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的ADLS Gen2连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集所需的凭据

为了验证您的[!DNL ADLS Gen2]源连接器，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | [!DNL ADLS Gen2]的终结点。 |
| `servicePrincipalId` | 应用程序的客户端ID。 |
| `servicePrincipalKey` | 应用程序的密钥。 |
| `tenant` | 包含您的应用程序的租户信息。 |

有关这些值的详细信息，请参阅[此 [!DNL ADLS Gen2] 文档](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

## 连接您的[!DNL ADLS Gen2]帐户

收集所需的凭据后，您可以按照以下步骤链接您的[!DNL ADLS Gen2]帐户以连接到[!DNL Experience Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!UICONTROL 数据库]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Azure Data Lake Gen2]**。 如果这是您第一次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的ADLS Gen2连接器。

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

将显示&#x200B;**[!UICONTROL 连接到Azure Data Lake Gen2]**&#x200B;对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL ADLS Gen2]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL ADLS Gen2]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 后续步骤

通过学习本教程，您已建立与[!DNL ADLS Gen2]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将云存储中的数据引入 [!DNL Experience Platform]](../../dataflow/batch/cloud-storage.md)。
