---
keywords: Experience Platform；主页；热门主题；Azure文件存储；Azure文件存储连接器
solution: Experience Platform
title: 在UI中创建Azure文件存储源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Azure文件存储源连接。
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 创建 [!DNL Azure File Storage] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了验证 [!DNL Azure File Storage] 源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   - [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Azure File Storage] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/batch/cloud-storage.md).

### 收集所需的凭据

为了验证您的 [!DNL Azure File Storage] 源连接器中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的端点 [!DNL Azure File Storage] 您正在访问的实例。 |
| `userId` | 具有足够访问权限的用户 [!DNL Azure File Storage] 端点。 |
| `password` | 此 [!DNL Azure File Storage] 访问密钥。 |

有关入门指南的更多信息，请参阅 [此 [!DNL Azure File Storage] 文档](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## 连接您的 [!DNL Azure File Storage] 帐户

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Azure File Storage] 目标帐户 [!DNL Platform].

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 以访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL Azure文件存储]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 以新建 [!DNL Azure File Storage] 连接器。

![目录](../../../../images/tutorials/create/azure-file-storage/catalog.png)

此 **[!UICONTROL 连接到Azure文件存储]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL Azure File Storage] 凭据。 完成后，选择 **[!UICONTROL Connect]** 然后留出一些时间来建立新连接。

![connect](../../../../images/tutorials/create/azure-file-storage/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Azure File Storage] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/azure-file-storage/existing.png)

## 后续步骤

按照本教程，您已建立与的连接 [!DNL Azure File Storage] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据从云存储引入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
