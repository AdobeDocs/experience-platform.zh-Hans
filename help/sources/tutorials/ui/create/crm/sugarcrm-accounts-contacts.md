---
title: 在UI中创建SugarCRM帐户和联系人源连接
description: 了解如何使用Adobe Experience Platform UI创建SugarCRM帐户和联系人源连接。
exl-id: 45840d7e-4c19-4720-8629-be446347862d
source-git-commit: 0de4b32ac2ddc90dabefd469b6658388a4532e0d
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 2%

---

# 创建 [!DNL SugarCRM Accounts & Contacts] UI中的源连接

本教程提供了用于创建 [!DNL SugarCRM Accounts & Contacts] 源连接，使用Adobe Experience Platform用户界面。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL SugarCRM] 帐户，您可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/crm.md).

### 收集所需的凭据

为了连接 [!DNL SugarCRM Accounts & Contacts] 到Platform时，必须提供以下连接属性的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `Host` | 源连接到的SugarCRM API端点。 | `developer.salesfusion.com` |
| `Username` | 您的SugarCRM开发人员帐户用户名。 | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | 您的SugarCRM开发人员帐户密码。 | `123456789` |

### 创建Platform架构

创建之前 [!DNL SugarCRM] 源连接时，还必须确保首先创建用于源的Platform架构。 请参阅上的教程 [创建平台架构](../../../../../xdm/schema/composition.md) 以了解有关如何创建模式的完整步骤。

此 [!DNL SugarCRM Accounts & Contacts] 支持多个API。 这意味着您必须根据所使用的对象类型创建单独的架构。 有关accounts和contacts架构，请参阅以下示例：

>[!BEGINTABS]

>[!TAB 帐户]

![显示帐户模式示例的平台UI屏幕截图](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB 联系人]

![显示联系人的示例架构的平台UI屏幕截图](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## 连接您的 [!DNL SugarCRM Accounts & Contacts] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示了多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 *CRM* 类别，选择 **[!UICONTROL SugarCRM帐户和联系人]**，然后选择 **[!UICONTROL 添加数据]**.

![带有SugarCRM帐户和联系人卡片的目录的Platform UI屏幕截图](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

此 **[!UICONTROL 连接SugarCRM帐户和联系人帐户]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL SugarCRM Accounts & Contacts] 要用于创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![将SugarCRM帐户和联系人帐户与现有帐户连接的Platform UI屏幕截图](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供名称、可选描述和您的凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后等待一段时间以建立新连接。

![将SugarCRM帐户和联系人帐户与新帐户连接的Platform UI屏幕截图](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### 选择数据

最后，必须选择要摄取到Platform的对象类型。

| 对象类型 | 描述 |
| --- | --- |
| `Accounts` | 与您的组织有关系的公司。 |
| `Contacts` | 与您的组织建立关系的个人。 |

>[!BEGINTABS]

>[!TAB 帐户]

![显示选中了“帐户”选项的配置的SugarCRM帐户和联系人的Platform UI屏幕截图](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB 联系人]

![显示选中了“联系人”选项的配置的SugarCRM帐户和联系人的Platform UI屏幕截图](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL SugarCRM Accounts & Contacts] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据引入Platform](../../dataflow/crm.md).

## 其他资源

以下各节提供了在使用时，您可以参考的其他资源 [!DNL SugarCRM] 源。

### 护栏 {#guardrails}

此 [!DNL SugarCRM] API限制速率为每分钟90次调用或每天2000次调用，以先发生者为准。 但是，通过在连接规范中添加参数来绕过此限制，该参数将延迟请求时间，从而永远不会达到速率限制。

### 验证 {#validation}

验证是否已正确设置源和 [!DNL SugarCRM Accounts & Contacts] 正在摄取数据，请执行以下步骤：

* 在Platform UI中，选择 **[!UICONTROL 查看数据流]** 在 [!DNL SugarCRM Accounts & Contacts] 源目录上的卡菜单。 接下来，选择 **[!UICONTROL 预览数据集]** 以验证已摄取的数据。

* 根据您所使用的对象类型，您可以根据 [!DNL SugarMarket] 下面的“帐户”或“联系人”页：

>[!BEGINTABS]

>[!TAB 帐户]

![SugarMarket帐户页面屏幕截图显示帐户列表](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB 联系人]

![SugarMarket Contacts页面的屏幕截图显示联系人列表](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>此 [!DNL SugarMarket] 页面不包含已删除的对象计数。 但是，通过此源检索的数据也将包含已删除的计数，这些计数将标有已删除的标志。
