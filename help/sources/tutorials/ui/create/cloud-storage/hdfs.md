---
keywords: Experience Platform；主页；热门主题；Apache HDFS;HDFS;HDFS
solution: Experience Platform
title: 在UI中创建Apache HDFS源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建ApacheHadoop分布式文件系统源连接。
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# 创建 [!DNL Apache] UI中的HDFS源连接

>[!NOTE]
>
>的 [!DNL Apache] HDFS连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

源连接器 [!DNL Adobe Experience Platform] 提供按计划摄取外部来源数据的功能。 本教程提供了验证 [!DNL Apache Hadoop Distributed File System] （以下简称HDFS）源连接器，使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对的以下组件有一定的了解 [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   - [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的HDFS连接，则可以跳过本文档的其余部分，继续阅读上的教程 [配置数据流](../../dataflow/batch/cloud-storage.md).

### 收集所需的凭据

要验证HDFS源连接器，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | URL可以匿名定义连接到HDFS所需的身份验证参数。 有关如何获取此值的更多信息，请参阅 [HDFS的HTTPS身份验证](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## 连接HDFS帐户

收集所需凭据后，您可以按照以下步骤将HDFS帐户关联到 [!DNL Platform].

登录到 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 的 **[!UICONTROL 目录]** 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 **[!UICONTROL 云存储]** 类别，选择 **[!UICONTROL Apache HDFS]**. 如果这是您首次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，请选择 **[!UICONTROL 添加数据]** 创建新的HDFS连接器。

![目录](../../../../images/tutorials/create/hdfs/catalog.png)

的 **[!UICONTROL 连接到HDFS]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述和HDFS凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![connect](../../../../images/tutorials/create/hdfs/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的HDFS帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/hdfs/existing.png)

## 后续步骤

通过阅读本教程，您已建立与HDFS帐户的连接。 您现在可以继续下一个教程和 [配置数据流，将云存储中的数据引入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
