---
keywords: Experience Platform；主页；热门主题；onetrust；OneTrust
solution: Experience Platform
title: 在UI中创建OneTrust源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建OneTrust源连接。
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# 创建 [!DNL OneTrust Integration] UI中的源连接

>[!NOTE]
>
>此 [!DNL OneTrust Integration] 源仅支持获取同意和偏好设置数据，而不支持Cookie。

本教程提供了用于创建 [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) 源连接，用于通过Platform用户界面将历史同意数据和计划同意数据吸收到Adobe Experience Platform中。

## 先决条件

>[!IMPORTANT]
>
>此 [!DNL OneTrust Integration] 源连接器和文档由创建 [!DNL OneTrust Integration] 团队。 如有任何查询或更新请求，请联系 [[!DNL OneTrust] 团队](https://my.onetrust.com/s/contactsupport?language=en_US) 直接。

连接之前 [!DNL OneTrust Integration] 到Platform，您必须首先检索您的访问令牌。 有关查找访问令牌的详细说明，请参阅 [[!DNL OneTrust Integration] OAuth 2指南](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

访问令牌过期后不会自动刷新，因为系统到系统刷新令牌不受支持 [!DNL OneTrust]. 因此，在访问令牌过期之前，必须确保连接中的访问令牌已更新。 访问令牌的最长可配置生命周期为一年。 要了解有关更新访问令牌的更多信息，请参阅 [[!DNL OneTrust] 有关管理OAuth 2.0客户端凭据的文档](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### 收集所需的凭据

为了连接 [!DNL OneTrust Integration] 对于Platform，您必须提供以下身份验证凭据的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 主机名 | 从中创建 [!DNL OneTrust Integration] 需要从中提取数据。 | `app.onetrust.com` |
| 授权测试URL | （可选）授权测试URL用于在创建基本连接时验证凭据。 如果未提供，则在源连接创建步骤期间将自动检查凭据。 |  |
| 访问令牌 | 与您的对应的访问令牌 [!DNL OneTrust Integration] 帐户。 | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

有关这些凭据的更多信息，请参阅 [[!DNL OneTrust Integration] 身份验证文档](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## 连接您的 [!DNL OneTrust Integration] 帐户

>[!NOTE]
>
>此 [!DNL OneTrust Integration] 正在与Adobe共享API规范以进行数据摄取。

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区中提供的源目录Experience Platform。

使用 *[!UICONTROL 类别]* 菜单，用于按类别筛选源。 或者，在搜索栏中输入源名称，以从目录查找特定源。

转到 [!UICONTROL 同意和偏好设置] 类别 [!DNL OneTrust Integration] 源卡。 要开始，请选择 **[!UICONTROL 添加数据]**.

![Experience PlatformUI源目录。](../../../../images/tutorials/create/onetrust/catalog.png)

此 **[!UICONTROL 连接OneTrust集成帐户]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL OneTrust Integration] 要用于创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![源工作流中的现有帐户身份验证步骤。](../../../../images/tutorials/create/onetrust/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供名称、可选描述和您的凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后留出一些时间来建立新连接。

![源工作流中的新帐户身份验证步骤。](../../../../images/tutorials/create/onetrust/new.png)

## 后续步骤

按照本教程，您已建立与的连接 [!DNL OneTrust Integration] 帐户。 您现在可以继续下一教程和 [配置数据流以将同意数据引入平台](../../dataflow/consent-and-preferences.md).
