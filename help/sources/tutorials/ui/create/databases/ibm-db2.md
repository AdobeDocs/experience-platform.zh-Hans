---
keywords: Experience Platform;home;popular topics;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: 在UI中创建IBM DB2源连接器
topic: overview
description: 本教程提供了使用平台用户界面创建IBM DB2（以下简称“DB2”）源连接器的步骤。
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---



# 在UI中创建IBM DB2源连接器

>[!NOTE]
>
> IBM DB2连接器处于测试阶段。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用户界面创建IBM DB2（以下称“DB2”）源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的DB2连接，您可以跳过此文档的其余部分，继续学习配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

以下各节提供了使用API成功连接到DB2所需了解的其他信 [!DNL Flow Service] 息。

| 凭据 | 描述 |
| ---------- | ----------- |
| `server` | DB2服务器的名称。 可以指定服务器名称后用冒号分隔的端口号。 例如：服务器：端口。 |
| `database` | DB2数据库的名称。 |
| `username` | 用于连接DB2数据库的用户名。 |
| `password` | 您为用户名指定的用户帐户的口令。 |

有关快速入门的详细信息，请参 [阅此DB2文档](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html)。

## 连接您的IBM DB2帐户

收集所需凭据后，您可以按照以下步骤将DB2帐户链接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 **[!UICONTROL 据库]** ”类别 **[!UICONTROL 下，选择IBM DB2]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选 **[!UICONTROL 择“添加]** 数据”以创建新的DB2连接器。

![目录](../../../../images/tutorials/create/ibm-db2/catalog.png)

出 **[!UICONTROL 现“Connect to IBM DB2]** ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和DB2凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的DB2帐户，然后选择“下 **[!UICONTROL 一步]** ”继续。

![现有](../../../../images/tutorials/create/ibm-db2/existing.png)

## 后续步骤

按照本教程，您已建立了与DB2帐户的连接。 您现在可以继续学习下一个教程， [并配置一个数据流以将数据引入 [!DNL Platform]](../../dataflow/databases.md)。