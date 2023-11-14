---
title: 通过UI将您的SalesforceMarketing Cloud帐户连接到Experience Platform
description: 了解如何通过UI将您的SalesforceMarketing Cloud帐户连接到Experience Platform。
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 1%

---

# 连接您的 [!DNL Salesforce Marketing Cloud] 要通过UIExperience Platform的帐户

>[!IMPORTANT]
>
>当前不支持自定义对象摄取 [!DNL Salesforce Marketing Cloud] 源集成。


本教程提供了有关如何连接 [!DNL Salesforce Marketing Cloud] 帐户通过UI访问Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有 [!DNL Salesforce Marketing Cloud] 帐户，您可以跳过本文档的其余部分，并继续阅读上的教程 [使用UI将营销自动化数据引入Experience Platform](../../dataflow/marketing-automation.md).

### 收集所需的凭据

要访问 [!DNL Salesforce Marketing Cloud] 帐户，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| Host | 应用程序的主机服务器。 这通常是您的子域。 **注意：** 输入时 `host` 值，您只需指定子域，而无需指定整个URL。 例如，如果您的主机URL为 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，则只需输入 `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 作为主机值。 |
| 客户端ID | 与您的关联的客户端ID [!DNL Salesforce Marketing Cloud] 应用程序。 |
| 客户端密码 | 与您的关联的客户端密钥 [!DNL Salesforce Marketing Cloud] 应用程序。 |

有关身份验证的详细信息 [!DNL Salesforce Marketing Cloud]，请访问 [[!DNL Salesforce] 身份验证文档](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## 连接您的 [!DNL Salesforce Marketing Cloud] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 显示Experience Platform支持的各种源。

您可以从类别列表中选择相应的类别。 您还可以使用搜索栏筛选特定源。

在 [!UICONTROL 营销自动化] 类别，选择 **[!UICONTROL SalesforceMarketing Cloud]** 然后选择 **[!UICONTROL 设置]**.

![已选择SalesforceMarketing Cloud源的源目录。](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

此 **[!UICONTROL 连接到SalesforceMarketing Cloud]** 页面。 在此页上，您可以创建新帐户或使用现有帐户。

### 新帐户

要创建新帐户，请选择 **[!UICONTROL 新帐户]** 并提供帐户名称、可选描述以及与您的帐户对应的身份验证凭据。 [!DNL Salesforce Marketing Cloud] 帐户。

完成后，选择 **[!UICONTROL 连接到源]** 然后等待一段时间以建立新连接。

![新的帐户界面，您可以在其中验证SalesforceMarketing Cloud的新帐户。](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 现有帐户

如果您已经拥有现有帐户，请选择 **[!UICONTROL 现有帐户]** 然后从显示的列表中选择要使用的帐户。

![可以从现有Salesforce帐户列表中选择的现有Marketing Cloud界面。](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 后续步骤

通过学习本教程，您已在 [!DNL Salesforce Marketing Cloud] 帐户和Experience Platform。 您现在可以继续下一教程和 [创建数据流以将您的营销自动化数据引入Experience Platform](../../dataflow/marketing-automation.md).
