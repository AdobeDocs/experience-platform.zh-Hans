---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Couchbase源连接器
topic: overview
translation-type: tm+mt
source-git-commit: adb9c46e7337897e2336971e58ebc90b0e497ea0
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# 在UI中创建Couchbase源连接器

> [!NOTE]
> Couchbase连接器为测试版。 功能和文档可能会发生更改。

中的源连 [!DNL Adobe Experience Platform] 接器提供按计划接收外部源数据的能力。 本教程提供了使用用户界面创建Couchbase源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对以下组件有一个有效的了解 [!DNL Platform]:

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): 组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的Couchbase连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要验证Couchbase源连接器，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到Couchbase实例的连接字符串。 Couchbase的连接字符串模式为 `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`。 有关获取连接字符串的详细信息，请参阅Couchbase连接上 [的文档](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)。 |

## 连接您的Couchbase帐户

收集所需凭据后，您可以按照以下步骤创建新的Couchbase帐户以连接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中 *[!UICONTROL 选择“源]* ”以访问“源”工作区。 “目 *[!UICONTROL 录]* ”屏幕显示可为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 *[!UICONTROL 据库]* ”类别 **[!UICONTROL 下]** ，选择Couchbase **单** 击+图标(+)以创建新的Couchbase连接器。

![目录](../../../../images/tutorials/create/couchbase/catalog.png)

此时 *[!UICONTROL 将显示“连接到]* Couchbase”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供连接的名称、可选说明和您的Couchbase凭据。 完成后，选 **[!UICONTROL 择“连接到源]** ”，然后为新帐户建立留出一些时间。

![connect](../../../../images/tutorials/create/couchbase/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的Couchbase帐户，然后选 **[!UICONTROL 择]** 右上角的“下一步”以继续。

![现有](../../../../images/tutorials/create/couchbase/existing.png)

## 后续步骤

通过遵循本教程，您已建立了与Couchbase帐户的连接。 您现在可以继续阅读下一个教程， [并配置数据流以将数据引入平台](../../dataflow/databases.md)。