---
keywords: Experience Platform；主页；热门主题；Azure Data Lake Storage Gen2；ADLS Gen2；adls gen2；adls连接器
solution: Experience Platform
title: 在UI中创建Azure Data Lake Storage Gen2源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Azure Data Lake Storage Gen2源连接。
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# 创建 [!DNL Azure Data Lake Storage Gen2] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了验证 [!DNL Azure Data Lake Storage Gen2] (以下简称“ ”[!DNL ADLS Gen2]&quot;)源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   - [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的ADLS Gen2连接，则可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/batch/cloud-storage.md).

### 收集所需的凭据

为了验证您的 [!DNL ADLS Gen2] 源连接器中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | 的端点 [!DNL ADLS Gen2]. |
| `servicePrincipalId` | 应用程序的客户端ID。 |
| `servicePrincipalKey` | 应用程序的密钥。 |
| `tenant` | 包含您的应用程序的租户信息。 |

有关这些值的更多信息，请参阅 [此 [!DNL ADLS Gen2] 文档](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## 连接您的 [!DNL ADLS Gen2] 帐户

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL ADLS Gen2] 要连接的帐户 [!DNL Platform].

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 以访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL Azure Data Lake Gen2]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 创建新的ADLS Gen2连接器。

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

此 **[!UICONTROL 连接到Azure Data Lake Gen2]** 对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新建帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL ADLS Gen2] 凭据。 完成后，选择 **[!UICONTROL Connect]** 然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL ADLS Gen2] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 后续步骤

按照本教程，您已建立与的连接 [!DNL ADLS Gen2] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据从云存储引入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
