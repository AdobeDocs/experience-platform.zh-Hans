---
keywords: Azure Blob;Blob目标；s3;Azure Blob目标
title: Azure Blob连接
description: 创建到Azure Blob存储的实时出站连接，以定期从Adobe Experience Platform导出制表符分隔或CSV数据文件。
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# [!DNL Azure Blob] 连接

## 概述 {#overview}

[!DNL Azure Blob] （以下简称）是微 [!DNL Blob]软的云对象存储解决方案。本教程提供了使用[!DNL Platform]用户界面创建[!DNL Blob]目标的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的[!DNL Blob]目标，则可以跳过本文档的其余部分，并继续阅读有关[将区段激活到目标](../../ui/activate-batch-profile-destinations.md)的教程。

## 支持的文件格式 {#file-formats}

[!DNL Experience Platform] 支持以下要导出到的文件格式 [!DNL Blob]:

* 分隔符分隔值(DSV):目前，对DSV格式化数据文件的支持仅限于逗号分隔值。 将来将提供对一般DSV文件的支持。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 连接字符串]**:访问Blob存储中的数据时需要使用连接字符串。[!DNL Blob]连接字符串模式的开头为：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。
   * 有关配置[!DNL Blob]连接字符串的更多信息，请参阅Microsoft文档中的[配置Azure存储帐户的连接字符串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account)。

* 或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为[!DNL Base64]编码字符串。
* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 文件夹路径]**:输入将托管导出文件的目标文件夹的路径。
* **[!UICONTROL 容器]**:输入要由此目 [!DNL Azure Blob Storage] 标使用的容器的名称。

或者，您也可以附加RSA格式的公钥，以向导出的文件添加加密。 您的公钥必须写为[!DNL Base64]编码字符串。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请参阅[将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)。
