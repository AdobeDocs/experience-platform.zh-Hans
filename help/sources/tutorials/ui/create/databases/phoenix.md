---
title: 使用Experience Platform用户界面连接您的Phoenix帐户
description: 了解如何使用用户界面连接您的Phoenix帐户并将数据从Phoenix数据库传送到Experience Platform。
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 1%

---

# 使用UI将您的[!DNL Phoenix]帐户连接到Experience Platform

>[!WARNING]
>
>[!DNL Phoenix]源将于2025年6月底弃用。

本教程提供了有关如何连接[!DNL Phoenix]帐户以及将[!DNL Phoenix]数据库中的数据导入Experience Platform的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有经过身份验证的[!DNL Phoenix]帐户，则可以跳过此文档的其余部分，并转到有关[为数据库配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

要在Experience Platform上访问您的[!DNL Phoenix]帐户，必须提供以下值：

| 凭据 | 描述 |
| --- | --- |
| Host | [!DNL Phoenix]服务器的IP地址或主机名。 |
| 端口 | [!DNL Phoenix]服务器用于侦听客户端连接的TCP端口。 如果您要连接到[!DNL Azure HDInsights]，则将端口指定为443。 如果未提供此参数，则值默认为8765。 |
| HTTP路径 | 与[!DNL Phoenix]服务器对应的部分URL。 如果您使用[!DNL Azure HDInsights]群集，请指定/hbasephoenix0。 |
| 用户名 | 用于访问[!DNL Phoenix]服务器的用户名。 |
| 密码 | 对应于用户的密码。 |
| Enable SSL | 指定是否使用SSL对到服务器的连接进行加密的切换。 |

有关入门的详细信息，请参阅[此 [!DNL Phoenix] 文档](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

收集所需的凭据后，您可以按照以下步骤将您的[!DNL Phoenix]帐户连接到Experience Platform。

## 连接您的[!DNL Phoenix]帐户

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问源工作区。 *[!UICONTROL 目录]*&#x200B;屏幕显示Experience Platform源目录中可用的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找特定源。

从源类别列表中选择&#x200B;**[!UICONTROL 数据库]**，然后从[!DNL Phoenix]信息卡中选择&#x200B;**[!UICONTROL 添加数据]**。

>[!TIP]
>
>源目录中的源可能会根据源的状态显示不同的提示。
> 
>* **[!UICONTROL 添加数据]**&#x200B;表示存在与您所选源关联的已验证帐户。
>
>* **[!UICONTROL 设置]**&#x200B;意味着您必须提供凭据并对新帐户进行身份验证，才能使用您选择的源。

![已选择Phoenix源卡的Experience Platform UI上的源目录。](../../../../images/tutorials/create/phoenix/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到Phoenix]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

>[!BEGINTABS]

>[!TAB 使用现有的Phoenix帐户]

要使用现有帐户，请选择[!UICONTROL 现有帐户]，然后从显示的列表中选择要使用的帐户。 完成后，选择[!UICONTROL 下一步]以继续。

![组织中已存在的经过身份验证的Phoenix数据库帐户的列表。](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB 创建新的Phoenix帐户]

若要使用新帐户，请选择[!UICONTROL 新帐户]，并提供名称、说明和您的[!DNL Phoenix]身份验证凭据。 完成后，选择[!UICONTROL 连接到源]，并等待几秒钟以建立新连接。

![新的帐户界面，您可以在其中提供身份验证凭据并创建Phoenix帐户。](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与[!DNL Phoenix]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Experience Platform](../../dataflow/databases.md)。
