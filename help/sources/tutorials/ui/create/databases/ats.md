---
keywords: Experience Platform；主页；热门主题；Azure表存储；Azure表存储；ATS;ATS
solution: Experience Platform
title: 在UI中创建Azure表存储源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Azure表存储源连接。
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: 7af79b9e0d6ed29b796ac7c98b4df1dda09f3513
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 在UI中创建[!DNL Azure Table Storage]源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了使用[!DNL Platform]用户界面创建[!DNL Azure Table Storage]（以下称为“ATS”）源连接器的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):用于组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的ATS连接，则可以跳过本文档的其余部分，并继续阅读有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

要在[!DNL Platform]上访问您的ATS帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 连接到[!DNL Azure Table Storage]实例的连接字符串。 要连接到ATS实例的连接字符串。 ATS的连接字符串模式为`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |

有关入门的更多信息，请参阅[this [!DNL Azure Table Storage] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)。

## 连接[!DNL Azure Table Storage]帐户

收集所需凭据后，您可以按照以下步骤将ATS帐户关联到[!DNL Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在&#x200B;**[!UICONTROL 数据库]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Azure表存储]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL Add data]**&#x200B;以创建新的ATS连接器。

![目录](../../../../images/tutorials/create/ats/catalog.png)

出现&#x200B;**[!UICONTROL 连接到Azure表存储]**&#x200B;页。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入窗体中，提供名称、可选描述和您的ATS凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后允许一些时间建立新连接。

![connect](../../../../images/tutorials/create/ats/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的ATS帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/ats/existing.png)

## 后续步骤

通过阅读本教程，您已建立与ATS帐户的连接。 您现在可以继续阅读下一个教程，并[配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md)。
