---
title: 使用Experience Platform用户界面连接您的Phoenix帐户
description: 了解如何使用用户界面连接您的Phoenix帐户，并将来自Phoenix数据库的数据引入Experience Platform。
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: b7e42eb180b8f16344afedadf763c33bcf22fa35
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# 连接您的 [!DNL Phoenix] 要使用UIExperience Platform的帐户

本教程提供了有关如何连接 [!DNL Phoenix] 帐户并从以下位置获取数据： [!DNL Phoenix] Experience Platform数据库。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有经过身份验证的 [!DNL Phoenix] 之后，您可以跳过本文档的其余部分并继续阅读上的教程 [为数据库配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

要访问 [!DNL Phoenix] account on account(Experience Platform帐户)，您必须提供以下值：

| 凭据 | 描述 |
| --- | --- |
| Host | 的IP地址或主机名 [!DNL Phoenix] 服务器。 |
| 端口 | TCP端口 [!DNL Phoenix] 服务器使用来侦听客户端连接。 如果您要连接到 [!DNL Azure HDInsights]，然后将端口指定为443。 如果未提供此参数，则值默认为8765。 |
| HTTP路径 | 与对应的部分URL [!DNL Phoenix] 服务器。 如果您使用 [!DNL Azure HDInsights] 群集。 |
| 用户名 | 您用于访问 [!DNL Phoenix] 服务器。 |
| 密码 | 对应于用户的密码。 |
| Enable SSL | 指定是否使用SSL对到服务器的连接进行加密的切换。 |

有关入门的更多信息，请参阅 [此 [!DNL Phoenix] 文档](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

收集所需的凭据后，您可以按照以下步骤连接您的 [!DNL Phoenix] 帐户到Experience Platform。

## 连接您的 [!DNL Phoenix] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问“源”工作区。 此 *[!UICONTROL 目录]* 屏幕显示Experience Platform源目录中可用的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找特定源。

选择 **[!UICONTROL 数据库]** 从源类别列表中，然后选择 **[!UICONTROL 添加数据]** 从 [!DNL Phoenix] 卡片。

>[!TIP]
>
>源目录中的源可能会根据源的状态显示不同的提示。
> 
>* **[!UICONTROL 添加数据]** 表示存在与您选择的源关联的已验证帐户。
>
>* **[!UICONTROL 设置]** 这意味着您必须提供凭据并对新帐户进行身份验证，才能使用您选择的源。

![选择了Phoenix源卡的Experience PlatformUI上的源目录。](../../../../images/tutorials/create/phoenix/catalog.png)

此 **[!UICONTROL 连接到凤凰城]** 页面。 在此页上，您可以使用新凭据或现有凭据。

>[!BEGINTABS]

>[!TAB 使用现有的Phoenix帐户]

要使用现有帐户，请选择 [!UICONTROL 现有帐户] 然后从显示的列表中选择要使用的帐户。 完成后，选择 [!UICONTROL 下一个] 以继续。

![组织中已存在的经过身份验证的Phoenix数据库帐户的列表。](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB 创建新的Phoenix帐户]

要使用新帐户，请选择 [!UICONTROL 新帐户] 并提供名称、描述以及 [!DNL Phoenix] 身份验证凭据。 完成后，选择 [!UICONTROL 连接到源] 并等待几秒钟以建立新连接。

![新的帐户界面，您可以在其中提供身份验证凭据并创建Phoenix帐户。](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL Phoenix] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据引入Experience Platform](../../dataflow/databases.md).
