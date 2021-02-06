---
keywords: Experience Platform；主页；热门话题；凤凰；凤凰
solution: Experience Platform
title: 在UI中创建Phoenix源连接
topic: overview
type: Tutorial
description: 了解如何使用Adobe Experience PlatformUI创建Phoenix源连接。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# 在UI中创建[!DNL Phoenix]源连接

>[!NOTE]
>
> [!DNL Phoenix]接头为测试版。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用[!DNL Platform]用户界面创建[!DNL Phoenix]源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的[!DNL Phoenix]连接，您可以跳过此文档的其余部分，继续学习有关[配置数据流](../../dataflow/databases.md)的教程

### 收集所需的凭据

要访问[!DNL Platform]上的[!DNL Phoenix]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | [!DNL Phoenix]服务器的IP地址或主机名。 |
| `port` | [!DNL Phoenix]服务器用于侦听客户端连接的TCP端口。 如果连接到[!DNL Azure HDInsights]，请将端口指定为443。 |
| `httpPath` | 与[!DNL Phoenix]服务器对应的部分URL。 如果使用[!DNL Azure HDInsights]群集，请指定/hbasephoenix0。 |
| `username` | 用于访问[!DNL Phoenix]服务器的用户名。 |
| `password` | 与用户对应的口令。 |
| `enableSsl` | 一个切换选项，指定是否使用SSL加密与服务器的连接。 |

有关入门的详细信息，请参阅[this [!DNL Phoenix] 文档](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

## 连接您的[!DNL Phoenix]帐户

收集所需凭据后，您可以按照以下步骤链接[!DNL Phoenix]帐户以连接到[!DNL Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL 目录]**&#x200B;屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Phoenix]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的[!DNL Phoenix]帐户。

![目录](../../../../images/tutorials/create/phoenix/catalog.png)

将显示&#x200B;**[!UICONTROL 连接到Phoenix]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL 新建帐户]**。 在显示的输入表单上，提供名称、可选说明和[!DNL Phoenix]凭据。 完成后，选择&#x200B;**[!UICONTROL Connect]**，然后为新连接建立留出一些时间。

![connect](../../../../images/tutorials/create/phoenix/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL Phoenix]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/phoenix/existing.png)

## 后续步骤

按照本教程，您已建立了与[!DNL Phoenix]帐户的连接。 现在，您可以继续阅读下一个教程，并配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md)。[