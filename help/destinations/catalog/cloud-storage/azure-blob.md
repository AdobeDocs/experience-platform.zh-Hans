---
keywords: Azure Blob;Blob目标；s3;Azure Blob目标
title: Azure Blob连接
description: 创建到Azure Blob存储的实时出站连接，以定期从Adobe Experience Platform导出制表符分隔或CSV数据文件。
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 1%

---


# [!DNL Azure Blob] 连接

## 概述 {#overview}

[!DNL Azure Blob] (以下简称“[!DNL Blob]”)是微软的云对象存储解决方案。本教程提供了使用[!DNL Platform]用户界面创建[!DNL Blob]目标的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   - [模式合成的基础](../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已经有一个有效的Blob目标，则可以跳过此文档的其余部分，继续学习有关[将区段激活到目标](../../ui/activate-destinations.md)的教程。

## 支持的文件格式 {#file-formats}

[!DNL Experience Platform] 支持以下要导出到的文件格式 [!DNL Blob]:

- 分隔符分隔值(DSV):目前，对DSV格式化数据文件的支持仅限于逗号分隔值。 将来将提供对一般DSV文件的支持。 有关受支持文件的详细信息，请阅读教程中[激活目标](../../ui/activate-destinations.md#esp-and-cloud-storage)的云存储部分。

## 连接您的Blob帐户{#connect-destination}

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL Destinations]**&#x200B;以访问&#x200B;**[!UICONTROL Destinations]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示了您可以为其创建帐户的各种目标。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定目标。

在&#x200B;**[!UICONTROL Cloud Storage]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Azure Blob Storage]**，后跟&#x200B;**[!UICONTROL Configure]**。

![Catalog](../../assets/catalog/cloud-storage/blob/catalog.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[目录](../../ui/destinations-workspace.md#catalog)部分。

将显示&#x200B;**[!UICONTROL Connect to Azure Blob Storage]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

## 新帐户{#new-account}

如果您使用新凭据，请选择&#x200B;**[!UICONTROL New account]**。 在显示的输入表单上，提供连接字符串。 访问Blob存储中的数据需要连接字符串。 [!DNL Blob]连接字符串模式开始:`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。

有关配置[!DNL Blob]连接字符串的详细信息，请参阅Microsoft文档中的[配置Azure存储帐户的连接字符串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account)。

或者，您可以附加RSA格式的公钥，以向导出的文件添加加密。 请注意，此公钥&#x200B;**必须**&#x200B;写入为Base64编码字符串。

![新帐户](../../assets/catalog/cloud-storage/blob/new.png)

## 现有帐户{#existing-account}

要连接现有帐户，请选择要连接的[!DNL Blob]帐户，然后选择&#x200B;**下一步**&#x200B;以继续。

![现有帐户](../../assets/catalog/cloud-storage/blob/existing.png)

## 身份验证{#authentication}

将显示&#x200B;**身份验证**&#x200B;页。 在显示的输入表单上，提供文件的名称、可选说明、文件夹路径和容器。

在此步骤中，您还可以选择应用于此目标的任何&#x200B;**[!UICONTROL Marketing actions]**。 营销活动指示要将数据导出到目标的目的。 您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

完成后，选择&#x200B;**[!UICONTROL Create destination]**。

![身份验证](../../assets/catalog/cloud-storage/blob/authentication.png)

## 后续步骤 {#activate-segments}

按照本教程，您已建立了与[!DNL Blob]帐户的连接。 现在，您可以继续阅读下一个教程，并[将区段激活到目标](../../ui/activate-destinations.md)。
