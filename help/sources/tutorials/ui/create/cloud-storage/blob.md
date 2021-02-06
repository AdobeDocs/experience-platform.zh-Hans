---
keywords: Experience Platform；主页；热门主题；Azure Blob;azure Blob;Azure Blob连接器
solution: Experience Platform
title: 在UI中创建Azure Blob源连接
topic: overview
type: Tutorial
description: 了解如何使用平台用户界面创建Azure Blob源连接器。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---


# 在UI中创建[!DNL Azure Blob]源连接

本教程提供了使用平台用户界面创建[!DNL Azure Blob]（下称“[!DNL Blob]”）的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的[!DNL Blob]连接，您可以跳过此文档的其余部分，继续学习有关配置数据流](../../dataflow/batch/cloud-storage.md)的教程。[

### 支持的文件格式

[!DNL Experience Platform] 支持从外部存储摄取的以下文件格式：

- 分隔符分隔值(DSV):目前，对DSV格式化数据文件的支持仅限于逗号分隔的值。 DSV格式化文件中字段标题的值只能由字母数字字符和下划线组成。 今后将提供对一般DSV文件的支持。
- JavaScript对象表示法(JSON):JSON格式数据文件必须符合XDM。
- Apache Parke:必须符合XDM规范，但必须符合XDM格式。

### 收集所需的凭据

要访问平台上的[!DNL Blob]存储，您必须为以下凭据提供有效值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 包含验证[!DNL Blob]为Experience Platform所必需的授权信息的字符串。 [!DNL Blob]连接字符串模式为：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 有关连接字符串的详细信息，请参阅[配置连接字符串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)的此[!DNL Blob]文档。 |
| `sasUri` | 可用作连接[!DNL Blob]帐户的替代身份验证类型的共享访问签名URI。 [!DNL Blob] SAS URI模式为：`https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`有关详细信息，请参阅此[!DNL Blob]文档，关于[共享访问签名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)。 |

## 连接您的[!DNL Blob]帐户

收集所需凭据后，您可以按照以下步骤将[!DNL Blob]帐户链接到平台。

在[平台UI](https://platform.adobe.com)中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL 目录]屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在[!UICONTROL 云存储]类别下，选择&#x200B;**[!UICONTROL Azure Blob存储]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/blob/catalog.png)

将显示&#x200B;**[!UICONTROL 连接到Azure Blob存储符]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择要用其创建新数据流的[!DNL Blob]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;继续。

![现有](../../../../images/tutorials/create/blob/existing.png)

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新建帐户]**，然后为新[!DNL Blob]帐户提供名称和选项说明。

**使用连接字符串进行身份验证**

[!DNL Blob]连接器为您提供不同的访问身份验证类型。 在[!UICONTROL 帐户身份验证]下，选择&#x200B;**[!UICONTROL 连接字符串]**&#x200B;以使用基于连接字符串的凭据。

![连接字符串](../../../../images/tutorials/create/blob/connectionstring.png)

**使用共享访问签名URI进行身份验证**

共享访问签名(SAS)URI允许对您的[!DNL Blob]帐户进行安全授权。 您可以使用SAS创建不同访问权限的身份验证凭据，因为基于SAS的身份验证允许您设置权限、开始和到期日期，以及为特定资源提供资源。

选择&#x200B;**[!UICONTROL SasURIAuthentication]**，然后提供您的[!DNL Blob] SAS URI。 选择&#x200B;**[!UICONTROL 连接到源]**&#x200B;以继续。

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## 后续步骤

按照本教程，您已建立了与[!DNL Blob]帐户的连接。 您现在可以继续阅读下一个教程，并[配置数据流，将数据从您的云存储引入平台](../../dataflow/batch/cloud-storage.md)。
