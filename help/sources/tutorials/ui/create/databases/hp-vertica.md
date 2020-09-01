---
keywords: Experience Platform;home;popular topics;HP Vertica
solution: Experience Platform
title: 在UI中创建HP Vertica源连接器
topic: overview
description: 本教程提供了使用平台用户界面创建HP Vertica源连接器的步骤。
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---


# 在UI中创 [!DNL Vertica] 建HP源连接器

>[!NOTE]
>
> HP接 [!DNL Vertica] 口为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用户界面创 [!DNL Vertica] 建HP源连接 [!DNL Platform] 器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的HP [!DNL Vertica] 连接，您可以跳过本文档的其余部分，继续学习配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

以下各节提供您需要了解的其他信息，以便使用API成 [!DNL Vertica] 功连接到 [!DNL Flow Service] HP。

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到HP实例的连接 [!DNL Vertica] 字符串。 HP的连接字符串模式 [!DNL Vertica] 是 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

有关快速入门的详细信息，请参 [阅此 [!DNL Vertica] HP文档](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)。

## 连接您的HP帐 [!DNL Vertica] 户

收集所需凭据后，您可以按照以下步骤将HP帐户链 [!DNL Vertica] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 **[!UICONTROL 据库]** ”类别 **[!UICONTROL 下，选择HP Vertica]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选 **[!UICONTROL 择“添加]** ”以创建新的HP连 [!DNL Vertica] 接器。

![目录](../../../../images/tutorials/create/hp-vertica/catalog.png)

将显 **[!UICONTROL 示“Connect to HP Vertica]** ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和您的HP凭 [!DNL Vertica] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### 现有帐户

要连接现有帐户，请选 [!DNL Vertica] 择要连接的HP帐户，然 **[!UICONTROL 后]** 选择右上角的“下一步”以继续。

![现有](../../../../images/tutorials/create/hp-vertica/existing.png)

## 后续步骤

按照本教程，您已建立了与HP帐户的 [!DNL Vertica] 连接。 您现在可以继续学习下一个教程， [并配置一个数据流以将数据引入 [!DNL Platform]](../../dataflow/databases.md)。