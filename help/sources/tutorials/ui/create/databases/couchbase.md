---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Couchbase源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# 在UI [!DNL Couchbase] 中创建源连接器

>[!NOTE]
>
> 连接 [!DNL Couchbase] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

中的源连 [!DNL Adobe Experience Platform] 接器提供按计划接收外部源数据的能力。 本教程提供了使用用户界 [!DNL Couchbase] 面创建源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对以下组件有一个有效的了解 [!DNL Platform]:

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有有效的连 [!DNL Couchbase] 接，您可以跳过此文档的其余部分，继续学习配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要验证源连接器的 [!DNL Couchbase] 身份，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到实例的连接 [!DNL Couchbase] 字符串。 的连接字符串模 [!DNL Couchbase] 式为 `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`。 有关获取连接字符串的详细信息，请参阅有关连接的 [[!DNL Couchbase] 文档](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)。 |

## 连接帐 [!DNL Couchbase] 户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL Couchbase] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 **[!UICONTROL 据库]** ”类别下， **[!UICONTROL 选择Couchbase]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选择 **[!UICONTROL 添加数据]** ，以创建新连 [!DNL Couchbase] 接器。

![目录](../../../../images/tutorials/create/couchbase/catalog.png)

此时 **[!UICONTROL 将显示“连接到]** Couchbase”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭 [!DNL Couchbase] 据。 完成后，选 **[!UICONTROL 择“连接到源]** ”，然后为建立新连接留出一些时间。

![connect](../../../../images/tutorials/create/couchbase/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Couchbase] 要连接的帐户，然后选择右 **[!UICONTROL 上]** 角的“下一步”以继续。

![现有](../../../../images/tutorials/create/couchbase/existing.png)

## 后续步骤

按照本教程，您已建立了与帐户的 [!DNL Couchbase] 连接。 您现在可以继续学习下一个教程， [并配置一个数据流以将数据引入 [!DNL Platform]](../../dataflow/databases.md)。