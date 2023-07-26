---
title: 使用Experience Platform用户界面连接Salesforce帐户
description: 了解如何使用用户界面连接您的Salesforce帐户并将您的CRM数据引入Experience Platform。
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 57cdcbd5018e7f57261f09c6bddf5e2a8dcfd0d5
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# 连接您的 [!DNL Salesforce] 要使用UIExperience Platform的帐户

本教程提供了有关如何连接 [!DNL Salesforce] ，并使用Experience Platform用户界面将您的CRM数据引入Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有经过身份验证的 [!DNL Salesforce] 帐户，您可以跳过本文档的其余部分，并继续阅读上的教程 [为CRM数据配置工作流](../../dataflow/crm.md).

### 收集所需的凭据 {#gather-required-credentials}

为了验证您的 [!DNL Salesforce] Experience Platform account with account时，必须提供对应于以下内容的值 [!DNL Salesforce] 凭据：

| 凭据 | 描述 |
| --- | --- |
| `environmentUrl` | 的URL [!DNL Salesforce] 源实例。 |
| `username` | 的用户名 [!DNL Salesforce] 用户帐户。 |
| `password` | 的密码 [!DNL Salesforce] 用户帐户。 |
| `securityToken` | 的安全令牌 [!DNL Salesforce] 用户帐户。 |
| `apiVersion` | （可选） REST API版本的 [!DNL Salesforce] 您正在使用的实例。 如果此字段留空，则Experience Platform将自动使用最新可用版本。 |

有关身份验证的详细信息，请参阅 [此 [!DNL Salesforce] 身份验证指南](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

收集所需的凭据后，您可以按照以下步骤连接您的 [!DNL Salesforce] 帐户到Experience Platform。

## 连接您的 [!DNL Salesforce] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问“源”工作区。 此 *[!UICONTROL 目录]* 屏幕显示Experience Platform源目录中可用的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找特定源。

选择 **[!UICONTROL CRM]** 从源类别列表中，然后选择 **[!UICONTROL 添加数据]** 从 [!DNL Salesforce] 卡片。

![选择了Salesforce源卡的Experience PlatformUI上的源目录。](../../../../images/tutorials/create/salesforce/catalog.png)

此 **[!UICONTROL 连接到Salesforce]** 页面。 在此页上，您可以使用新凭据或现有凭据。

>[!BEGINTABS]

>[!TAB 使用现有Salesforce帐户]

要使用现有帐户，请选择 **[!UICONTROL 现有帐户]** 然后从显示的列表中选择要使用的帐户。 完成后，选择 **[!UICONTROL 下一个]** 以继续。

![组织中已存在的经过身份验证的Salesforce帐户的列表。](../../../../images/tutorials/create/salesforce/existing.png)

>[!TAB 创建新的Salesforce帐户]

要使用新帐户，请选择 **[!UICONTROL 新帐户]** 并提供名称、描述以及 [!DNL Salesforce] 身份验证凭据。 完成后，选择 **[!UICONTROL 连接到源]** 并等待几秒钟以建立新连接。

![在界面中，通过提供适当的身份验证凭据来创建新的Salesforce帐户。](../../../../images/tutorials/create/salesforce/new.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL Salesforce] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据引入 [!DNL Platform]](../../dataflow/crm.md).
