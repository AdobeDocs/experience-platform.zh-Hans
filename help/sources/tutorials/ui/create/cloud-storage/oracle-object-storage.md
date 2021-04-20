---
keywords: Experience Platform；主页；热门主题；Oracle对象存储;oracle对象存储
solution: Experience Platform
title: 在UI中创建Oracle对象存储源连接
topic: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Oracle对象存储源连接。
translation-type: tm+mt
source-git-commit: c1453a9f0be42f834d35af871051324df8dadf80
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# 在UI中创建[!DNL Oracle Object Storage]源连接

本教程提供了使用Adobe Experience Platform UI创建[!DNL Oracle Object Storage]源连接的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

### 收集所需凭据

要连接到[!DNL Oracle Object Storage]，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUrl` | 身份验证所需的[!DNL Oracle Object Storage]端点。 端点格式为：`https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 身份验证所需的[!DNL Oracle Object Storage]访问密钥ID。 |
| `secretKey` | 身份验证所需的[!DNL Oracle Object Storage]密码。 |
| `bucketName` | 如果用户具有受限访问权限，则需要允许的存储段名称。 存储段名称必须长度在3到63个字符之间，必须以字母或数字开头和结尾，并且只能包含小写字母、数字或连字符(`-`)。 存储段名称的格式不能与IP地址相同。 |
| `folderPath` | 如果用户具有受限访问权限，则需要允许的文件夹路径。 |

有关如何获取这些值的详细信息，请参阅[Oracle对象存储身份验证指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)。

收集所需凭据后，您可以按照以下步骤创建新的Oracle对象存储帐户以连接到平台。

## 连接到Oracle对象存储

在平台UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL 目录]屏幕显示了可创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索栏找到要处理的特定源。

在[!UICONTROL 云存储]类别下，选择&#x200B;**[!UICONTROL Oracle对象存储]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 现有帐户

要使用现有帐户，请选择要用来创建新数据流的[!DNL Oracle Object Storage]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新建帐户]**，然后提供名称、可选说明和[!DNL Oracle Object Storage]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后为建立新连接留出一些时间。

![新](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 后续步骤

按照本教程，您已建立了与[!DNL Oracle Object Storage]帐户的连接。 现在，您可以继续下一个教程，内容是[配置数据流以将来自云存储的数据引入Platform](../../dataflow/batch/cloud-storage.md)。
