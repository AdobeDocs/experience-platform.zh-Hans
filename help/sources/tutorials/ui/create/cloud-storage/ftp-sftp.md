---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建FTP或SFTP源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---


# 在UI中创建FTP或SFTP源连接器

>[!NOTE]
>
>FTP和SFTP连接器处于测试阶段。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用户界面创建FTP或SFTP源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的FTP或SFTP连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/batch/cloud-storage.md)。

### 支持的文件格式

[!DNL Experience Platform] 支持从外部源摄取的以下文件格式：

* 分隔符分隔值(DSV):目前，对DSV格式化数据文件的支持仅限于逗号分隔值(CSV)。 DSV格式化文件中字段标题的值只能由字母数字字符和下划线组成。 今后将提供对一般DSV的支持。
* JavaScript对象表示法(JSON):JSON格式数据文件必须符合XDM。
* Apache Parke:必须符合XDM规范，但必须符合XDM格式。

### 收集所需的凭据

要在上访问FTP或SFTP服 [!DNL Platform]务器，必须提供服 **务器的主**&#x200B;机名、 **用户名**&#x200B;和 **密码**。

## 连接到FTP或SFTP服务器

收集所需凭据后，您可以按照以下步骤创建新的FTP或SFTP帐户以连接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建入站帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 **[!UICONTROL 据库]** ”类别下， **[!UICONTROL 选择SFTP]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选 **[!UICONTROL 择“添加]** ”以创建新的FTP或SFTP连接器。

![目录](../../../../images/tutorials/create/sftp/catalog.png)

此时 **[!UICONTROL 将显示“连接到]** SFTP”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明以及FTP或SFTP凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![connect](../../../../images/tutorials/create/sftp/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的FTP或SFTP帐户，然后选择下 **[!UICONTROL 一]** 步以继续。

![现有](../../../../images/tutorials/create/sftp/existing.png)

## 后续步骤

按照本教程，您已建立了与FTP或SFTP帐户的连接。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。