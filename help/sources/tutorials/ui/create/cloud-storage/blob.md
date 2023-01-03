---
keywords: Experience Platform；主页；热门主题；Azure Blob;Azure Blob连接器
solution: Experience Platform
title: 在UI中创建Azure Blob源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用平台用户界面创建Azure Blob源连接器。
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---

# 创建 [!DNL Azure Blob] UI中的源连接

本教程提供了创建 [!DNL Azure Blob] (以下简称“[!DNL Blob]“”)。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   - [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有 [!DNL Blob] 连接时，您可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/batch/cloud-storage.md).

### 支持的文件格式

[!DNL Experience Platform] 支持从外部存储摄取以下文件格式：

- 分隔符分隔值(DSV):目前，对DSV格式化数据文件的支持仅限于逗号分隔值。 DSV格式文件中字段标题的值只能由字母数字字符和下划线组成。 将来将提供对一般DSV文件的支持。
- JavaScript对象表示法(JSON):JSON格式的数据文件必须符合XDM。
- Apache Parquet:必须符合XDM规范，但必须使用Parquet格式的数据文件。

### 收集所需的凭据

为了访问 [!DNL Blob] 存储时，必须为以下凭据提供有效值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 一个字符串，其中包含进行身份验证所需的授权信息 [!DNL Blob] Experience Platform。 的 [!DNL Blob] 连接字符串模式为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. 有关连接字符串的更多信息，请参阅此 [!DNL Blob] 文档 [配置连接字符串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | 共享访问签名URI，可用作连接您的 [!DNL Blob] 帐户。 的 [!DNL Blob] SAS URI模式为： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 有关更多信息，请参阅此 [!DNL Blob] 文档 [共享访问签名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## 连接 [!DNL Blob] 帐户

收集所需的凭据后，您可以按照以下步骤链接 [!DNL Blob] 帐户到平台。

在 [平台UI](https://platform.adobe.com)，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL Azure Blob存储]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/blob/catalog.png)

的 **[!UICONTROL 连接到Azure Blob Storage]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Blob] 创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/blob/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为新用户提供名称和选项描述 [!DNL Blob] 帐户。

**使用连接字符串进行身份验证**

的 [!DNL Blob] 连接器为您提供不同的访问身份验证类型。 在 [!UICONTROL 帐户身份验证] 选择 **[!UICONTROL ConnectionString]** 使用基于连接字符串的凭据。

![连接字符串](../../../../images/tutorials/create/blob/connectionstring.png)

**使用共享访问签名URI进行身份验证**

共享访问签名(SAS)URI允许对您的 [!DNL Blob] 帐户。 您可以使用SAS创建不同访问度的身份验证凭据，因为基于SAS的身份验证允许您设置权限、开始和到期日期以及对特定资源的配置。

选择 **[!UICONTROL SasURIAuthentication]** 然后提供 [!DNL Blob] SAS URI。 选择 **[!UICONTROL 连接到源]** 以继续。

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## 后续步骤

通过阅读本教程，您已经与 [!DNL Blob] 帐户。 您现在可以继续下一个教程和 [配置数据流，以将云存储中的数据引入平台](../../dataflow/batch/cloud-storage.md).
