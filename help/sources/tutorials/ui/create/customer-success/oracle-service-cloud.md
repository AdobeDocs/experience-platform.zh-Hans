---
keywords: Experience Platform；主页；热门主题；Oracle服务云；oracle服务云
title: 在UI中创建Oracle服务云源连接
description: 了解如何使用Adobe Experience Platform UI创建Oracle服务云源连接。
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 在UI中创建Oracle服务云源连接

本教程提供了使用Adobe Experience Platform用户界面创建Oracle服务云源连接的步骤。

## 快速入门

本教程需要对Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的Oracle服务云源连接，则可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/customer-success.md)

### 收集所需的凭据

要访问您的Oracle服务云帐户，请执行以下操作： [!DNL Platform]，则必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| Host | 您的Oracle服务云实例的主机URL。 |
| 用户名 | 您的Oracle服务云用户帐户的用户名。 |
| 密码 | 您的Oracle服务云帐户的密码。 |

有关对Oracle服务云帐户进行身份验证的更多信息，请参阅 [[!DNL Oracle] 认证指南](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## 连接您的Oracle服务云帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕显示可用于创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL 客户成功] 类别，选择 **[!UICONTROL Oracle服务云]** 然后选择 **[!UICONTROL 添加数据]**.

![突出显示Oracle服务云源的源目录。](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

的 **[!UICONTROL 连接到Oracle服务云]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择要连接的Oracle服务云帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有帐户界面。](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述和您的Oracle服务云凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![新帐户与的占位符值的界面。](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## 后续步骤

通过阅读本教程，您已建立与Oracle服务云帐户的连接。 您现在可以继续下一个教程和 [配置数据流以将客户成功数据引入平台](../../dataflow/crm.md).
