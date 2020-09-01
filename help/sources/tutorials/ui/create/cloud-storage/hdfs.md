---
keywords: Experience Platform;home;popular topics;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: 在UI中创建Apache HDFS源连接器
topic: overview
description: 本教程提供使用平台用户界面验证Apache Hadoop分布式文件系统（以下称“HDFS”）源连接器的步骤。
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---


# 在UI [!DNL Apache] 中创建HDFS源连接器

>[!NOTE]
>
>HDFS [!DNL Apache] 接口为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

中的源连 [!DNL Adobe Experience Platform] 接器提供按计划接收外部源数据的能力。 本教程提供了使用用 [!DNL Apache Hadoop Distributed File System] 户界面验证源连接器（以下称“HDFS”）的 [!DNL Platform] 步骤。

## 入门指南

本教程需要对以下组件有一个有效的了解 [!DNL Platform]:

- [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有有效的HDFS连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/batch/cloud-storage.md)。

### 收集所需的凭据

要验证HDFS源连接器，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | URL定义匿名连接到HDFS所需的身份验证参数。 有关如何获取此值的详细信息，请参阅以下HDFS HTTPS身 [份验证文档](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)。 |

## 连接您的HDFS帐户

收集所需凭据后，您可以按照以下步骤将HDFS帐户链接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“云 **[!UICONTROL 存储]** ”类别 **[!UICONTROL 下，选择Apache]** HDFS。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选 **[!UICONTROL 择“添加数]** 据”创建新的HDFS连接器。

![目录](../../../../images/tutorials/create/hdfs/catalog.png)

将显 **[!UICONTROL 示“连接到HDFS]** ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和HDFS凭据。 完成后，选 **[!UICONTROL 择“连接到源]** ”，然后为建立新连接留出一些时间。

![connect](../../../../images/tutorials/create/hdfs/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的HDFS帐户，然后选择“下 **[!UICONTROL 一步]** ”继续。

![现有](../../../../images/tutorials/create/hdfs/existing.png)

## 后续步骤

按照本教程，您已建立了与HDFS帐户的连接。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。