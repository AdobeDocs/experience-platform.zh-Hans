---
keywords: Experience Platform；主页；热门主题；Google云存储；Google云存储；GCS;GCS
solution: Experience Platform
title: 在UI中创建Google云存储源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Google UI创建Adobe Experience Platform云存储源连接。
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---

# 创建 [!DNL Google Cloud Storage] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了创建 [!DNL Google Cloud Storage] （以下简称GCS）源连接器，使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的GCS连接，则可以跳过本文档的其余部分，继续阅读上的教程 [配置数据流](../../dataflow/batch/cloud-storage.md).

### 支持的文件格式

[!DNL Experience Platform] 支持从外部存储摄取以下文件格式：

* 分隔符分隔值(DSV):目前，对DSV格式化数据文件的支持仅限于逗号分隔值。 DSV格式文件中字段标题的值只能由字母数字字符和下划线组成。 将来将提供对一般DSV文件的支持。
* JavaScript对象表示法(JSON):JSON格式的数据文件必须符合XDM。
* Apache Parquet:必须符合XDM规范，但必须使用Parquet格式的数据文件。

### 收集所需的凭据

要在 [!DNL Platform]，则必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 访问密钥ID | 由61个字符组成的字母数字字符串，用于验证您的 [!DNL Google Cloud Storage] 帐户到平台。 |
| 密钥访问密钥 | 一个40个字符、基于64编码的字符串，用于验证您的 [!DNL Google Cloud Storage] 帐户到平台。 |

有关这些值的更多信息，请参阅 [Google云存储HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 的双曲余切值。 有关如何生成您自己的访问密钥ID和密钥的步骤，请参阅 [[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md).

## 连接 [!DNL Google Cloud Storage] 帐户

收集所需凭据后，您可以按照以下步骤将GCS帐户关联到 [!DNL Platform].

登录到 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 的 **[!UICONTROL 目录]** 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL Google云存储]**. 如果这是您首次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，请选择 **[!UICONTROL 添加数据]** 创建新的GCS连接器。

![目录](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

的 **[!UICONTROL 连接到Google云存储]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述和您的GCS凭据。 完成后，选择 **[!UICONTROL 连接]** 然后，再留出一些时间建立新连接。

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的GCS帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## 后续步骤

通过阅读本教程，您已建立与GCS帐户的连接。 您现在可以继续下一个教程和 [配置数据流，将云存储中的数据引入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
