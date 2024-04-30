---
title: 在UI中创建Azure事件中心源连接
description: 了解如何使用Adobe Experience Platform UI创建Azure事件中心源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: e4ea21af3f0d9e810959330488dc06bc559cf72c
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 1%

---

# 创建 [!DNL Azure Event Hubs] UI中的源连接

>[!IMPORTANT]
>
>此 [!DNL Azure Event Hubs] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

本教程提供了创建 [!DNL Azure Event Hubs] 使用Adobe Experience Platform用户界面创建的帐户。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Event Hubs] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/streaming/cloud-storage-streaming.md).

### 收集所需的凭据

为了验证您的 [!DNL Event Hubs] 源连接器中，必须提供以下连接属性的值：

>[!BEGINTABS]

>[!TAB 标准身份验证]

| 凭据 | 描述 |
| --- | --- |
| SAS密钥名称 | 授权规则的名称，也称为SAS密钥名称。 |
| SAS键 | 的主键 [!DNL Event Hubs] 命名空间。 此 `sasPolicy` 该 `sasKey` 对应于必须具有 `manage` 权限已配置，用于 [!DNL Event Hubs] 要填充的列表。 |
| 命名空间 | 的命名空间 [!DNL Event Hubs] 您正在访问。 An [!DNL Event Hubs] namespace提供了一个唯一的范围容器，您可以在其中创建一个或多个 [!DNL Event Hubs]. |

>[!TAB SAS身份验证]

| 凭据 | 描述 |
| --- | --- |
| SAS密钥名称 | 授权规则的名称，也称为SAS密钥名称。 |
| SAS键 | 的主键 [!DNL Event Hubs] 命名空间。 此 `sasPolicy` 该 `sasKey` 对应于必须具有 `manage` 权限已配置，用于 [!DNL Event Hubs] 要填充的列表。 |
| 命名空间 | 的命名空间 [!DNL Event Hubs] 您正在访问。 An [!DNL Event Hubs] namespace提供了一个唯一的范围容器，您可以在其中创建一个或多个 [!DNL Event Hubs]. |
| 事件中心名称 | 您的名称 [!DNL Event Hubs] 源。 |

有关共享访问签名(SAS)身份验证的详细信息 [!DNL Event Hubs]，阅读 [[!DNL Azure] 使用SAS指南](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB 事件中心Azure Active Directory身份验证]

| 凭据 | 描述 |
| --- | --- |
| 租户ID | 要从中请求权限的租户ID。 可以将您的租户ID格式化为GUID或友好名称。 **注意**：租户ID在中称为“目录ID” [!DNL Microsoft Azure] 界面。 |
| 客户端ID | 分配给您应用程序的应用程序ID。 您可以从以下位置检索此ID [!DNL Microsoft Entra ID] 门户，您可在其中注册 [!DNL Azure Active Directory]. |
| 客户端密钥值 | 与客户端ID一起用于对应用程序进行身份验证的客户端密码。 您可以从以下位置检索您的客户端密钥： [!DNL Microsoft Entra ID] 门户，您可在其中注册 [!DNL Azure Active Directory]. |
| 命名空间 | 的命名空间 [!DNL Event Hubs] 您正在访问。 An [!DNL Event Hubs] namespace提供了一个唯一的范围容器，您可以在其中创建一个或多个 [!DNL Event Hubs]. |

有关的详细信息 [!DNL Azure Active Directory]，阅读 [关于使用Microsoft Entra ID的Azure指南](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB 事件中心范围的Azure Active Directory身份验证]

| 凭据 | 描述 |
| --- | --- |
| 租户ID | 要从中请求权限的租户ID。 可以将您的租户ID格式化为GUID或友好名称。 **注意**：租户ID在中称为“目录ID” [!DNL Microsoft Azure] 界面。 |
| 客户端ID | 分配给您应用程序的应用程序ID。 您可以从以下位置检索此ID [!DNL Microsoft Entra ID] 门户，您可在其中注册 [!DNL Azure Active Directory]. |
| 客户端密钥值 | 与客户端ID一起用于对应用程序进行身份验证的客户端密码。 您可以从以下位置检索您的客户端密钥： [!DNL Microsoft Entra ID] 门户，您可在其中注册 [!DNL Azure Active Directory]. |
| 命名空间 | 的命名空间 [!DNL Event Hubs] 您正在访问。 An [!DNL Event Hubs] namespace提供了一个唯一的范围容器，您可以在其中创建一个或多个 [!DNL Event Hubs]. |
| 事件中心名称 | 您的名称 [!DNL Event Hubs] 源。 |

有关的详细信息 [!DNL Azure Active Directory]，阅读 [关于使用Microsoft Entra ID的Azure指南](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Event Hubs] 帐户到Experience Platform。

## 连接您的 [!DNL Event Hubs] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示了您可以用来创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL Azure事件中心]**，然后选择 **[!UICONTROL 添加数据]**.

![已选择Azure事件中心的源目录。](../../../../images/tutorials/create/eventhub/catalog.png)

此 **[!UICONTROL 连接到Azure事件中心]** 出现对话框。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Event Hubs] 要使用的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有Azure事件中心源帐户的列表。](../../../../images/tutorials/create/eventhub/existing.png)

### 新帐户

>[!TIP]
>
>创建后，便无法更改的身份验证类型 [!DNL Event Hubs] 基本连接。 要更改身份验证类型，必须创建新的基本连接。

要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为新页面提供名称和可选描述 [!DNL Event Hubs] 帐户。

![Azure事件中心的新帐户创建界面。](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB 标准身份验证]

创建 [!DNL Event Hubs] 使用标准身份验证的帐户，使用 [!UICONTROL 帐户身份验证] 下拉菜单，然后选择 **[!UICONTROL 标准身份验证]**. 接下来，为提供以下各项的值： [!UICONTROL SAS密钥名称]， [!UICONTROL SAS键]、和 [!UICONTROL 命名空间].

输入身份验证凭据后，选择 **[!UICONTROL 连接到源]**.

![Azure事件中心的标准身份验证接口。](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB SAS身份验证]

创建 [!DNL Event Hubs] 使用SAS身份验证的帐户，使用 [!UICONTROL 帐户身份验证] 下拉菜单，然后选择 **[!UICONTROL SAS身份验证]**. 接下来，为提供以下各项的值： [!UICONTROL SAS密钥名称]， [!UICONTROL SAS键]， [!UICONTROL 命名空间]、和 [!UICONTROL 事件中心名称].

输入身份验证凭据后，选择 **[!UICONTROL 连接到源]**.

![Azure事件中心的SAS身份验证接口。](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB 事件中心Azure Active Directory身份验证]

创建 [!DNL Event Hubs] 具有事件中心Azure Active Directory身份验证的帐户，使用 [!UICONTROL 帐户身份验证] 下拉菜单，然后选择 **[!UICONTROL 事件中心Azure Active Directory]**. 接下来，为提供以下各项的值： [!UICONTROL 租户ID]， [!UICONTROL 客户端ID]， [!UICONTROL 客户端密钥值]、和 [!UICONTROL 命名空间].

![Azure事件中心Azure Active Directory身份验证](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB 事件中心范围的Azure Active Directory身份验证]

创建 [!DNL Event Hubs] 具有事件中心范围的Azure Active Directory身份验证的帐户，使用 [!UICONTROL 帐户身份验证] 下拉菜单，然后选择 **[!UICONTROL 事件中心范围的Azure Active Directory]**. 接下来，为提供以下各项的值： [!UICONTROL 租户ID]， [!UICONTROL 客户端ID]， [!UICONTROL 客户端密钥值]， [!UICONTROL 命名空间]、和 [!UICONTROL 事件中心名称].

![Azure事件中心范围的Azure活动目录身份验证](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## 后续步骤

按照本教程，您已连接 [!DNL Event Hubs] 帐户到Experience Platform。 您现在可以继续下一教程和 [配置数据流以将数据从云存储引入Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).
