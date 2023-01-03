---
keywords: Experience Platform；主页；热门主题；Greenplum;Greenplum
solution: Experience Platform
title: 在UI中创建GreenPlum源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建GreenPlum源连接。
exl-id: e6c6a495-25ce-4497-b20e-91374c7bb548
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# 创建 [!DNL GreenPlum] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了创建 [!DNL GreenPlum] 源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有 [!DNL GreenPlum] 连接时，您可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

以下部分提供了成功连接到所需了解的其他信息 [!DNL GreenPlum] 使用 [!DNL Flow Service] API。

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到的连接字符串 [!DNL GreenPlum] 实例。 的连接字符串模式 [!DNL GreenPlum] is `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

有关入门的更多信息，请参阅 [这份绿李文件](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

## 连接 [!DNL GreenPlum] 帐户

收集所需的凭据后，您可以按照以下步骤链接 [!DNL GreenPlum] 帐户 [!DNL Platform].

登录到 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 的 **[!UICONTROL 目录]** 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL 绿梅]**. 如果这是您首次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，请选择 **[!UICONTROL 添加数据]** 创建新 [!DNL GreenPlum] 连接器。

![目录](../../../../images/tutorials/create/greenplum/catalog.png)

的 **[!UICONTROL 连接到GreenPlum]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述以及 [!DNL GreenPlum] 凭据。 完成后，选择 **[!UICONTROL 连接]** 然后，再留出一些时间建立新连接。

![connect](../../../../images/tutorials/create/greenplum/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL GreenPlum] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 的问题。

![现有](../../../../images/tutorials/create/greenplum/existing.png)

## 后续步骤

通过阅读本教程，您已经与 [!DNL GreenPlum] 帐户。 您现在可以继续下一个教程和 [配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md).
