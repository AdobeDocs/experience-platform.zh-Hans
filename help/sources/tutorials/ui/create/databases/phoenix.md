---
keywords: Experience Platform；主页；热门主题；凤凰城；凤凰城
solution: Experience Platform
title: 在UI中创建Phoenix Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Phoenix源连接。
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# 创建 [!DNL Phoenix] UI中的源连接

>[!NOTE]
>
> 此 [!DNL Phoenix] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了用于创建 [!DNL Phoenix] 源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Phoenix] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/databases.md)

### 收集所需的凭据

要访问您的 [!DNL Phoenix] 帐户于 [!DNL Platform]中，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的IP地址或主机名 [!DNL Phoenix] 服务器。 |
| `port` | TCP端口， [!DNL Phoenix] 服务器使用来侦听客户端连接。 如果您连接到 [!DNL Azure HDInsights]，将端口指定为443。 |
| `httpPath` | 与对应的部分URL [!DNL Phoenix] 服务器。 如果您使用 [!DNL Azure HDInsights] 群集。 |
| `username` | 用于访问 [!DNL Phoenix] 服务器。 |
| `password` | 对应于用户的密码。 |
| `enableSsl` | 指定是否使用SSL加密服务器连接的切换开关。 |

有关入门的更多信息，请参阅 [此 [!DNL Phoenix] 文档](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## 连接您的 [!DNL Phoenix] 帐户

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Phoenix] 要连接的帐户 [!DNL Platform].

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 以访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL 凤凰城]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 以新建 [!DNL Phoenix] 帐户。

![目录](../../../../images/tutorials/create/phoenix/catalog.png)

此 **[!UICONTROL 连接到凤凰城]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL Phoenix] 凭据。 完成后，选择 **[!UICONTROL Connect]** 然后留出一些时间来建立新连接。

![connect](../../../../images/tutorials/create/phoenix/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Phoenix] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/phoenix/existing.png)

## 后续步骤

按照本教程，您已建立与的连接 [!DNL Phoenix] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md).
