---
keywords: Experience Platform；主页；热门主题；Couchbase;Couchbase
solution: Experience Platform
title: 在UI中创建Couchbase源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Couchbase源连接。
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# 在UI中创建[!DNL Couchbase]源连接

>[!NOTE]
>
> [!DNL Couchbase]连接器处于测试状态。 有关使用测试版标记的连接器的详细信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

[!DNL Adobe Experience Platform]中的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用[!DNL Platform]用户界面创建[!DNL Couchbase]源连接器的步骤。

## 入门指南

本教程需要对[!DNL Platform]的以下组件有充分的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成的基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已有有效的[!DNL Couchbase]连接，则可以跳过此文档的其余部分，继续学习有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需凭据

要验证[!DNL Couchbase]源连接器，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到[!DNL Couchbase]实例的连接字符串。 [!DNL Couchbase]的连接字符串模式为`Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`。 有关获取连接字符串的详细信息，请参阅[[!DNL Couchbase] connection](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)上的文档。 |

## 连接您的[!DNL Couchbase]帐户

收集所需凭据后，您可以按照以下步骤将您的[!DNL Couchbase]帐户链接到[!DNL Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问&#x200B;**[!UICONTROL Sources]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示了可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Couchbase]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL Configure]**。 否则，选择&#x200B;**[!UICONTROL Add data]**&#x200B;以创建新[!DNL Couchbase]连接器。

![目录](../../../../images/tutorials/create/couchbase/catalog.png)

将显示&#x200B;**[!UICONTROL Connect to Couchbase]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL New account]**。 在显示的输入表单上，提供名称、可选说明和[!DNL Couchbase]凭据。 完成后，选择&#x200B;**[!UICONTROL Connect to source]**，然后为新连接建立留出一些时间。

![connect](../../../../images/tutorials/create/couchbase/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL Couchbase]帐户，然后选择右上角的&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/couchbase/existing.png)

## 后续步骤

按照本教程，您已建立了与[!DNL Couchbase]帐户的连接。 您现在可以继续下一个教程，并[配置一个数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md)。
