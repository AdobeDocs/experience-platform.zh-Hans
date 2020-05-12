---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Azure文件存储源连接器
topic: overview
translation-type: tm+mt
source-git-commit: aa1c6cb0f5702cfe444cb2046e4460e404f13e57
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# 在UI中创建Azure文件存储源连接器

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了使用平台用户界面验证Azure文件存储源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
- [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有文件存储连接，您可以跳过此文档的其余部分，继续学习配置数据 [流的教程](../../dataflow/batch/cloud-storage.md)。

### 收集所需的凭据

要验证您的Azure文件存储源连接器，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 您正在访问的Azure文件存储实例的端点。 |
| `userId` | 对Azure文件存储端点具有足够访问权限的用户。 |
| `password` | Azure文件存储访问密钥。 |

有关入门的详细信息，请参 [阅此Azure文件存储文档](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)。

## 连接您的Azure文件存储帐户

收集所需凭据后，您可以按照以下步骤创建新的Azure文件存储帐户以连接到平台。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中 *[!UICONTROL 选择“源]* ”以访问“源”工作区。 “ *[!UICONTROL 目录]* ”屏幕显示可为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 *[!UICONTROL 据库]* ”类别下，选 **[!UICONTROL 择“Azure文件]** 存储 **”，单** 击“+”图标(+)以创建新的Azure文件存储连接器。

![目录](../../../../images/tutorials/create/azure-file-storage/catalog.png)

将显 *[!UICONTROL 示“连接到Azure文件存储]* ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供连接的名称、可选说明和文件存储凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新帐户。

![connect](../../../../images/tutorials/create/azure-file-storage/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的Azure文件存储帐户，然后选择下 **[!UICONTROL 一步]** 以继续。

![现有](../../../../images/tutorials/create/azure-file-storage/existing.png)

## 后续步骤

通过遵循本教程，您已建立到Azure文件存储帐户的连接。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入平台](../../dataflow/batch/cloud-storage.md)。