---
title: 在UI中创建Azure Blob源连接
description: 了解如何使用Platform用户界面创建Azure Blob源连接器。
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---

# 创建 [!DNL Azure Blob] UI中的源连接

本教程提供了创建 [!DNL Azure Blob] (以下简称“[!DNL Blob]“)使用Platform用户界面进行源连接。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于在Experience Platform中整理客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Blob] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/batch/cloud-storage.md).

### 支持的文件格式

Experience Platform支持从外部存储摄取的以下文件格式：

* 分隔符分隔值(DSV)：可使用任何单列分隔符（如制表符、逗号、竖线、分号或哈希）收集任何格式的平面文件。
* JavaScript对象表示法(JSON)： JSON格式的数据文件必须符合XDM。
* Apache Parquet： Parquet格式的数据文件必须符合XDM。

### 收集所需的凭据

要访问 [!DNL Blob] 存储Experience Platform时，必须为以下凭据提供有效值：

>[!BEGINTABS]

>[!TAB 连接字符串验证]

| 凭据 | 描述 |
| --- | --- |
| 连接字符串 | 一个字符串，其中包含进行身份验证所需的授权信息 [!DNL Blob] Experience Platform。 此 [!DNL Blob] 连接字符串模式为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. 有关连接字符串的详细信息，请参阅此 [!DNL Blob] 文档 [配置连接字符串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |

>[!TAB SAS URI身份验证]

| 凭据 | 描述 |
| --- | --- |
| SAS URI | 共享访问签名URI，您可以将其用作连接您的主机和计算机的 [!DNL Blob] 帐户。 此 [!DNL Blob] SAS URI模式为： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 有关更多信息，请参阅此 [!DNL Blob] 文档 [共享访问签名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| 容器 | 要为其指定访问权限的容器的名称。 使用创建新帐户时 [!DNL Blob] 源，您可以提供容器名称以指定用户对所选子文件夹的访问权限。 |
| 文件夹路径 | 要提供访问权限的文件夹的路径。 |

>[!ENDTABS]

收集所需的凭据后，您可以按照以下步骤连接您的 [!DNL Blob] 存储到Experience Platform

## 连接您的 [!DNL Blob] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示了多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL Azure Blob存储]**，然后选择 **[!UICONTROL 添加数据]**.

![已选择Azure BlobExperience Platform源的存储源目录。](../../../../images/tutorials/create/blob/catalog.png)

此 **[!UICONTROL 连接到Azure Blob存储]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Blob] 要用于创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/blob/existing.png)

### 新帐户

>[!TIP]
>
>创建后，便无法更改的身份验证类型 [!DNL Blob] 基本连接。 要更改身份验证类型，必须创建新的基本连接。

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为新页面提供名称和可选描述 [!DNL Blob] 帐户。

![Azure Blob存储源的新帐户屏幕。](../../../../images/tutorials/create/blob/new.png)

此 [!DNL Blob] 源支持帐户密钥身份验证和共享访问签名(SAS)身份验证。 基于帐户密钥的身份验证需要使用连接字符串进行验证，而SAS身份验证使用允许对帐户进行安全委托授权的URI。

在此步骤中，您还可以通过定义容器名称和子文件夹的路径来指定帐户将有权访问的子文件夹。

>[!BEGINTABS]

>[!TAB 连接字符串]

要使用帐户密钥进行身份验证，请选择 **[!UICONTROL 帐户密钥身份验证]** 并提供连接字符串。 在此步骤中，您还可以指定容器名称和要访问的子文件夹的路径。 完成后，选择 **[!UICONTROL 连接到源]**.

![连接字符串](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB SAS URI]

您可以使用SAS创建具有不同访问级别的身份验证凭据，因为基于SAS的身份验证允许您设置权限、开始和到期日期，以及配置给特定资源。

要使用共享访问签名进行身份验证，请选择 **[!UICONTROL 共享访问签名身份验证]** 然后提供您的SAS URI。 在此步骤中，您还可以指定容器名称和要访问的子文件夹的路径。 完成后，选择 **[!UICONTROL 连接到源]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL Blob] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据从云存储引入Platform](../../dataflow/batch/cloud-storage.md).
