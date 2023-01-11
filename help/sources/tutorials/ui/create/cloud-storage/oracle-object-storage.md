---
keywords: Experience Platform；主页；热门主题；Oracle对象存储；oracle对象存储
solution: Experience Platform
title: 在UI中创建Oracle对象存储源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Oracle对象存储源连接。
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# 创建 [!DNL Oracle Object Storage] UI中的源连接

本教程提供了创建 [!DNL Oracle Object Storage] 源连接。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

连接到 [!DNL Oracle Object Storage]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUrl` | 的 [!DNL Oracle Object Storage] 身份验证所需的端点。 端点格式为： `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 的 [!DNL Oracle Object Storage] 访问密钥ID，这是进行身份验证所需的。 |
| `secretKey` | 的 [!DNL Oracle Object Storage] 验证所需的密码。 |
| `bucketName` | 如果用户具有受限访问权限，则需要允许的存储段名称。 存储段名称必须介于3到63个字符之间，且必须以字母或数字开头和结尾，并且只能包含小写字母、数字或连字符(`-`)。 存储段名称的格式不能与IP地址类似。 |
| `folderPath` | 用户具有受限访问权限时需要的允许文件夹路径。 |

有关如何获取这些值的更多信息，请参阅 [Oracle对象存储身份验证指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

收集所需的凭据后，您可以按照以下步骤创建新的Oracle对象存储帐户以连接到平台。

## 连接到Oracle对象存储

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以为其创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL Oracle对象存储]** 然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 现有帐户

要使用现有帐户，请选择 [!DNL Oracle Object Storage] 创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供名称、可选描述以及 [!DNL Oracle Object Storage] 凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![新建](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 后续步骤

通过阅读本教程，您已经与 [!DNL Oracle Object Storage] 帐户。 您现在可以继续阅读下一个教程： [配置数据流以将数据从云存储引入平台](../../dataflow/batch/cloud-storage.md).
