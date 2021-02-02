---
keywords: Azure Blob;Blob目标；s3;azure Blob目标
title: Azure Blob目标
seo-title: Azure Blob目标
description: 创建到Azure Blob存储的实时出站连接，定期从Adobe Experience Platform导出制表符分隔或CSV数据文件。
seo-description: 创建到Azure Blob存储的实时出站连接，定期从Adobe Experience Platform导出制表符分隔或CSV数据文件。
translation-type: tm+mt
source-git-commit: 739c7cb55f943675d5ee63d81bba58a2b250c814
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---


# 在UI中创建[!DNL Azure Blob]目标

[!DNL Azure Blob] (以下简称“[!DNL Blob]”)是微软的云对象存储解决方案。本教程提供了使用[!DNL Platform]用户界面创建[!DNL Blob]目标的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   - [模式合成基础](../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的Blob目标，您可以跳过此文档的其余部分，继续学习有关将区段激活到目标](../../ui/activate-destinations.md)的教程。[

### 支持的文件格式

[!DNL Experience Platform] 支持以下要导出到的文件格式 [!DNL Blob]:

- 分隔符分隔值(DSV):目前，对DSV格式化数据文件的支持仅限于逗号分隔的值。 今后将提供对一般DSV文件的支持。 有关受支持文件的详细信息，请阅读教程中有关[激活目标](../../ui/activate-destinations.md#esp-and-cloud-storage)的云存储部分

## 连接您的Blob帐户{#connect-destination}

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 目标]**&#x200B;以访问&#x200B;**[!UICONTROL 目标]**&#x200B;工作区。 **[!UICONTROL 目录]**&#x200B;屏幕显示您可以为其创建帐户的各种目标。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定目标。

在&#x200B;**[!UICONTROL 云存储]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Azure Blob存储]**，然后选择&#x200B;**[!UICONTROL 激活]**。

![Catalog](../../assets/catalog/cloud-storage/blob/catalog.png)

将显示&#x200B;**[!UICONTROL 连接到Azure Blob存储符]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户{#new-account}

如果您使用新凭据，请选择&#x200B;**[!UICONTROL 新建帐户]**。 在显示的输入表单上，提供连接字符串。 访问Blob存储中的数据所需的连接字符串。 [!DNL Blob]连接字符串模式开始有：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。

或者，您可以附加RSA格式的公钥，以向导出的文件添加加密。 请注意，此公钥&#x200B;**必须**&#x200B;写成Base64编码字符串。

![新帐户](../../assets/catalog/cloud-storage/blob/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL Blob]帐户，然后选择&#x200B;**下一步**&#x200B;以继续。

![现有帐户](../../assets/catalog/cloud-storage/blob/existing.png)

## 身份验证{#authentication}

将显示&#x200B;**身份验证**&#x200B;页。 在显示的输入表单上，提供文件的名称、可选说明、文件夹路径和容器。 完成后，选择&#x200B;**[!UICONTROL 创建目标]**。

![身份验证](../../assets/catalog/cloud-storage/blob/authentication.png)

## 后续步骤 {#activate-segments}

按照本教程，您已建立了与[!DNL Blob]帐户的连接。 您现在可以继续阅读下一个教程，并[将区段激活到目标](../../ui/activate-destinations.md)。
