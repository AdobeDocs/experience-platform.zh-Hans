---
keywords: Experience Platform;home;popular topics;mysql;MySQL
solution: Experience Platform
title: 在UI中创建MySQL源连接器
topic: overview
type: Tutorial
description: 本教程提供了使用平台用户界面创建MySQL源连接器的步骤。
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---


# 在UI [!DNL MySQL] 中创建源连接器

>[!NOTE]
>
> 连接 [!DNL MySQL] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用平台用 [!DNL MySQL] 户界面创建源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有连接， [!DNL MySQL] 您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要访问您的帐 [!DNL MySQL] 户， [!DNL Platform]您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您 [!DNL MySQL] 的帐户关联的连接字符串。 连接 [!DNL MySQL] 字符串模式为： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. 您可以通过阅读文档进一步了解连接字符串以及如何获取它 [[!DNL MySQL] 们](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)。 |

## 连接帐 [!DNL MySQL] 户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL MySQL] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

在“数 **[!UICONTROL 据库]** ”类别下， **[!UICONTROL 选择MySQL]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选择 **[!UICONTROL 添加数据]** ，以创建新连 [!DNL MySQL] 接器。

![](../../../../images/tutorials/create/my-sql/catalog.png)

将显 **[!UICONTROL 示“连接到MySQL]** ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭 [!DNL MySQL] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![](../../../../images/tutorials/create/my-sql/new.png)

### 现有帐户

要连接现有帐户，请选 [!DNL MySQL] 择要连接的帐户，然后选择 **[!UICONTROL 下一]** 步以继续。

![](../../../../images/tutorials/create/my-sql/existing.png)

## 后续步骤

通过本教程，您已建立了与MySQL帐户的连接。 您现在可以继续学习下一个教程， [并配置一个数据流以将数据引入 [!DNL Platform]](../../dataflow/databases.md)。