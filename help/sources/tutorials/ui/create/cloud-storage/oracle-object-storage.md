---
keywords: Experience Platform；主页；热门主题；Oracle对象存储；oracle对象存储
solution: Experience Platform
title: 在UI中创建Oracle对象存储Source连接
type: Tutorial
description: 了解如何使用Oracle UI创建Adobe Experience Platform对象存储源连接。
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# 在UI中创建[!DNL Oracle Object Storage] Source连接

本教程提供了使用Adobe Experience Platform UI创建[!DNL Oracle Object Storage]源连接的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

在中，要连接到[!DNL Oracle Object Storage]，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUrl` | 身份验证所需的[!DNL Oracle Object Storage]终结点。 终结点格式为： `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 身份验证所需的[!DNL Oracle Object Storage]访问密钥ID。 |
| `secretKey` | 身份验证所需的[!DNL Oracle Object Storage]密码。 |
| `bucketName` | 如果用户具有受限访问权限，则需要允许的分段名称。 存储段名称的长度必须介于3到63个字符之间，必须以字母或数字开头和结尾，并且只能包含小写字母、数字或连字符(`-`)。 存储段名称的格式不得类似于IP地址。 |
| `folderPath` | 如果用户具有受限访问权限，则需要允许的文件夹路径。 |

有关如何获取这些值的详细信息，请参阅[Oracle Object Storage身份验证指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)。

收集完所需的凭据后，您可以按照以下步骤创建新的Oracle对象存储帐户以连接到Experience Platform。

## 连接到Oracle对象存储

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在[!UICONTROL 云存储]类别下，选择&#x200B;**[!UICONTROL Oracle对象存储]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 现有账户

要使用现有帐户，请选择要用于创建新数据流的[!DNL Oracle Object Storage]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 新帐户

如果您正在创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供名称、可选描述和您的[!DNL Oracle Object Storage]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![新](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 后续步骤

通过学习本教程，您已建立与[!DNL Oracle Object Storage]帐户的连接。 您现在可以继续有关[配置数据流以将数据从云存储引入Experience Platform](../../dataflow/batch/cloud-storage.md)的下一个教程。
