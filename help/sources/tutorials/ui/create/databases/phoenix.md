---
keywords: Experience Platform；主页；热门主题；凤凰；凤凰
solution: Experience Platform
title: 在UI中创建Phoenix源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Phoenix源连接。
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# 创建 [!DNL Phoenix] UI中的源连接

>[!NOTE]
>
> 的 [!DNL Phoenix] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了创建 [!DNL Phoenix] 源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有 [!DNL Phoenix] 连接时，您可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/databases.md)

### 收集所需的凭据

为了访问 [!DNL Phoenix] 帐户 [!DNL Platform]，则必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的IP地址或主机名 [!DNL Phoenix] 服务器。 |
| `port` | TCP端口 [!DNL Phoenix] 服务器使用侦听客户端连接。 如果您连接到 [!DNL Azure HDInsights]，将端口指定为443。 |
| `httpPath` | 与 [!DNL Phoenix] 服务器。 如果使用 [!DNL Azure HDInsights] 群集。 |
| `username` | 用于访问 [!DNL Phoenix] 服务器。 |
| `password` | 与用户对应的密码。 |
| `enableSsl` | 用于指定是否使用SSL加密与服务器的连接的切换开关。 |

有关入门的更多信息，请参阅 [此 [!DNL Phoenix] 文档](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## 连接 [!DNL Phoenix] 帐户

收集所需的凭据后，您可以按照以下步骤链接 [!DNL Phoenix] 连接到的帐户 [!DNL Platform].

登录到 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 的 **[!UICONTROL 目录]** 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL 凤凰城]**. 如果这是您首次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，请选择 **[!UICONTROL 添加数据]** 创建新 [!DNL Phoenix] 帐户。

![目录](../../../../images/tutorials/create/phoenix/catalog.png)

的 **[!UICONTROL 连接到Phoenix]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述以及 [!DNL Phoenix] 凭据。 完成后，选择 **[!UICONTROL 连接]** 然后，再留出一些时间建立新连接。

![connect](../../../../images/tutorials/create/phoenix/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Phoenix] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/phoenix/existing.png)

## 后续步骤

通过阅读本教程，您已经与 [!DNL Phoenix] 帐户。 您现在可以继续下一个教程和 [配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md).
