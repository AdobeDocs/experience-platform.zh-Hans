---
keywords: Experience Platform；主页；热门主题；onetrust；OneTrust
solution: Experience Platform
title: 在UI中创建OneTrust Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建OneTrust源连接。
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 2%

---

# 在用户界面中创建[!DNL OneTrust Integration]源连接

>[!NOTE]
>
>[!DNL OneTrust Integration]源仅支持获取同意和偏好设置数据，而不支持Cookie。

本教程提供了一些步骤，介绍如何使用Experience Platform用户界面创建[[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US)源连接以将历史同意数据和计划同意数据吸收到Adobe Experience Platform中。

## 先决条件

>[!IMPORTANT]
>
>[!DNL OneTrust Integration]源连接器和文档由[!DNL OneTrust Integration]团队创建。 如有任何查询或更新请求，请直接联系[[!DNL OneTrust] 团队](https://my.onetrust.com/s/contactsupport?language=en_US)。

在将[!DNL OneTrust Integration]连接到Experience Platform之前，必须首先检索您的访问令牌。 有关查找访问令牌的详细说明，请参阅[[!DNL OneTrust Integration] OAuth 2指南](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token)。

访问令牌过期后不会自动刷新，因为[!DNL OneTrust]不支持系统到系统刷新令牌。 因此，在访问令牌过期之前，必须确保连接中的访问令牌已更新。 访问令牌的最大可配置生命周期为一年。 要了解有关更新访问令牌的更多信息，请参阅有关管理OAuth 2.0客户端凭据的[[!DNL OneTrust] 文档](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials)。

### 收集所需的凭据

为了将[!DNL OneTrust Integration]连接到Experience Platform，您必须提供以下身份验证凭据的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 主机名称 | 需要从中提取[!DNL OneTrust Integration]数据的环境。 | `app.onetrust.com` |
| 授权测试URL | （可选）创建基本连接时，授权测试URL用于验证凭据。 如果未提供，则会在源连接创建步骤中自动检查凭据。 | |
| 访问令牌 | 与您的[!DNL OneTrust Integration]帐户对应的访问令牌。 | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

有关这些凭据的详细信息，请参阅[[!DNL OneTrust Integration] 身份验证文档](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token)。

## 连接您的[!DNL OneTrust Integration]帐户

>[!NOTE]
>
>正在与Adobe共享[!DNL OneTrust Integration] API规范以进行数据摄取。

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问Experience Platform中可用源目录的[!UICONTROL 源]工作区。

使用&#x200B;*[!UICONTROL 类别]*&#x200B;菜单按类别筛选源。 或者，在搜索栏中输入源名称，以从目录查找特定源。

转到[!DNL OneTrust Integration]源卡的[!UICONTROL 同意和偏好设置]类别。 要开始，请选择&#x200B;**[!UICONTROL 添加数据]**。

![Experience Platform UI源目录。](../../../../images/tutorials/create/onetrust/catalog.png)

出现&#x200B;**[!UICONTROL Connect OneTrust集成帐户]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

要使用现有帐户，请选择要用于创建新数据流的[!DNL OneTrust Integration]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![源工作流中的现有帐户身份验证步骤。](../../../../images/tutorials/create/onetrust/existing.png)

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新建帐户]**，然后提供名称、可选描述和凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![源工作流中的新帐户身份验证步骤。](../../../../images/tutorials/create/onetrust/new.png)

## 后续步骤

通过学习本教程，您已建立与[!DNL OneTrust Integration]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将同意数据导入Experience Platform](../../dataflow/consent-and-preferences.md)。
