---
keywords: 更新目标帐户、目标帐户、如何更新帐户、更新目标
title: 更新目标帐户
type: Tutorial
description: 本教程列出了在Adobe Experience Platform UI中更新目标帐户的步骤
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# 更新目标帐户

## 概述 {#overview}

的 **[!UICONTROL 帐户]** 选项卡会显示有关您已与各种目标建立的连接的详细信息。 请参阅 [帐户概述](../ui/destinations-workspace.md#accounts) 您可以获取每个目标帐户的所有信息。

本教程介绍了使用Experience PlatformUI更新目标帐户详细信息的步骤。

您可以更新目标帐户详细信息，以刷新和重新验证当前或过期帐户的凭据，以获取您当前使用的目标。 通常，OAuth和载体令牌的生命周期有限，具体取决于目标平台。 当这些令牌过期时，您可以在下面进一步描述的工作流中刷新它们。 此工作流将指导您完成OAuth工作流或重新插入令牌。 同样，如果下游平台中的密码或用户访问权限发生更改，则可以刷新凭据。

对于批处理目标，您可以更新访问密钥或密钥（如果其中任何目标已更改）。 此外，如果您希望加密文件，则可以插入RSA公钥，导出的文件将随后进行加密。

![“帐户”选项卡](../assets/ui/update-accounts/destination-accounts.png)

## 更新帐户 {#update}

请按照以下步骤将连接详细信息更新到现有目标。

1. 登录到 [Experience PlatformUI](https://platform.adobe.com/) 选择 **[!UICONTROL 目标]** 中。 选择 **[!UICONTROL 帐户]** 来查看您的现有帐户。

   ![“帐户”选项卡](../assets/ui/update-accounts/accounts-tab.png)

2. 选择过滤器图标 ![过滤器图标](../assets/ui/update-accounts/filter.png) 来启动排序面板。 排序面板提供了所有目标的列表。 您可以从列表中选择多个目标，以查看与选定目标关联的已筛选帐户选择。

   ![筛选目标帐户](../assets/ui/update-accounts/filter-accounts.png)

3. 选择省略号(`...`)。 此时会出现一个弹出面板，其中提供了 **[!UICONTROL 激活区段]**, **[!UICONTROL 编辑详细信息]**&#x200B;和 **[!UICONTROL 删除]** 帐户。 选择 ![“编辑详细信息”按钮](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL 编辑详细信息]** 按钮以编辑帐户信息。

   ![编辑帐户](../assets/ui/update-accounts/accounts-edit.png)

4. 输入更新的帐户凭据。

   * 对于使用 `OAuth1` 或 `OAuth2` 连接类型，选择 **[!UICONTROL 重新连接OAuth]** 续订帐户凭据。 您还可以更新帐户的名称和描述。

   ![编辑详细信息OAuth](../assets/ui/update-accounts/edit-details-oauth.png)

   * 对于使用 `Access Key` 或 `ConnectionString` 连接类型，则可以编辑帐户身份验证信息，包括访问ID、密钥或连接字符串等信息。 您还可以更新帐户的名称和描述。

   ![编辑详细信息访问密钥](../assets/ui/update-accounts/edit-details-key.png)

   * 对于使用 `Bearer token` 连接类型，则可以根据需要输入新的载体令牌。 您还可以更新帐户的名称和描述。

   ![编辑详细信息载体令牌](../assets/ui/update-accounts/edit-details-bearer.png)

   * 对于使用 `Server to server` 连接类型，则可以更新帐户的名称和说明。

   ![编辑详细信息服务器到服务器](../assets/ui/update-accounts/edit-details-s2s.png)

5. 选择 **[!UICONTROL 保存]** 完成帐户详细信息更新。

## 后续步骤

通过阅读本教程，您已成功使用 **[!UICONTROL 目标]** 工作区以更新现有帐户。

有关目标的更多信息，请参阅 [目标概述](../catalog/overview.md).