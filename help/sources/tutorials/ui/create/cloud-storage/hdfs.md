---
keywords: Experience Platform；主页；热门主题；Apache HDFS；HDFS；hdfs
solution: Experience Platform
title: 在UI中创建Apache HDFS源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建ApacheHadoop分布式文件系统源连接。
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# 创建 [!DNL Apache] UI中的HDFS源连接

>[!NOTE]
>
>此 [!DNL Apache] HDFS连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

中的源连接器 [!DNL Adobe Experience Platform] 提供按计划摄取外部源数据的功能。 本教程提供了对进行身份验证的步骤 [!DNL Apache Hadoop Distributed File System] （以下简称“HDFS”）源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对以下组件有一定的了解 [!DNL Platform]：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   - [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的HDFS连接，则可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/batch/cloud-storage.md).

### 收集所需的凭据

要验证HDFS源连接器，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | URL定义了匿名连接到HDFS所需的身份验证参数。 有关如何获取此值的更多信息，请参阅以下文档： [HDFS的HTTPS身份验证](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## 连接您的HDFS帐户

收集所需的凭据后，您可以按照以下步骤将HDFS帐户关联到 [!DNL Platform].

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示了多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 **[!UICONTROL 云存储]** 类别，选择 **[!UICONTROL Apache HDFS]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 创建新的HDFS连接器。

![目录](../../../../images/tutorials/create/hdfs/catalog.png)

此 **[!UICONTROL 连接到HDFS]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入表单上，提供名称、可选描述和您的HDFS凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后等待一段时间以建立新连接。

![connect](../../../../images/tutorials/create/hdfs/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的HDFS帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/hdfs/existing.png)

## 后续步骤

通过学习本教程，您已建立与HDFS帐户的连接。 您现在可以继续下一教程和 [配置数据流以将云存储中的数据引入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
