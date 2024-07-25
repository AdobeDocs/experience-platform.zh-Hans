---
keywords: 更新目标帐户、目标帐户、如何更新帐户、更新目标
title: 更新目标帐户
type: Tutorial
description: 本教程列出了在Adobe Experience Platform UI中更新目标帐户的步骤
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# 更新目标帐户

## 概述 {#overview}

**[!UICONTROL 帐户]**&#x200B;选项卡显示有关您与各种目标建立的连接的详细信息。 请参阅[帐户概述](../ui/destinations-workspace.md#accounts)，以了解有关每个目标帐户的所有信息。

本教程介绍了使用Experience PlatformUI更新目标帐户详细信息的步骤。

您可以更新目标帐户详细信息，以刷新和重新验证您当前使用的目标的当前帐户或已过期帐户的凭据。 通常，OAuth和持有者令牌的生命周期有限，具体取决于目标平台。 当这些令牌过期时，您可以在下面进一步描述的工作流中刷新它们。 此工作流指导您完成OAuth工作流或重新插入令牌。 同样，如果密码或用户访问权限在下游平台中发生更改，您可以刷新凭据。

对于批处理目标，您可以更新访问密钥或密钥（如果有任何更改的话）。 此外，如果您希望以后加密文件，可以插入RSA公钥，并且导出的文件以后将加密。

![帐户选项卡](../assets/ui/update-accounts/destination-accounts.png)

## 更新帐户 {#update}

请按照以下步骤将连接详细信息更新到现有目标。

1. 登录到[Experience PlatformUI](https://platform.adobe.com/)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 目标]**。 从顶部标题中选择&#x200B;**[!UICONTROL 帐户]**&#x200B;以查看现有帐户。

   ![帐户选项卡](../assets/ui/update-accounts/accounts-tab.png)

2. 选择左上角的过滤器图标![过滤器图标](/help/images/icons/filter.png)以启动排序面板。 排序面板提供所有目标的列表。 您可以从列表中选择多个目标，以查看与所选目标关联的已过滤帐户选择。

   ![筛选目标帐户](../assets/ui/update-accounts/filter-accounts.png)

3. 选择要更新的帐户名称旁边的省略号(`...`)。 此时会显示一个弹出面板，其中提供了&#x200B;**[!UICONTROL 激活受众]**、**[!UICONTROL 编辑详细信息]**&#x200B;和&#x200B;**[!UICONTROL 删除]**&#x200B;帐户的选项。 选择![编辑详细信息按钮](/help/images/icons/edit.png) **[!UICONTROL 编辑详细信息]**&#x200B;按钮以编辑帐户信息。

   ![编辑帐户](../assets/ui/update-accounts/accounts-edit.png)

4. 输入更新后的帐户凭据。

   * 对于使用`OAuth1`或`OAuth2`连接类型的帐户，请选择&#x200B;**[!UICONTROL 重新连接OAuth]**&#x200B;以续订帐户凭据。 您还可以更新帐户的名称和描述。

   ![编辑详细信息OAuth](../assets/ui/update-accounts/edit-details-oauth.png)

   * 对于使用`Access Key`或`ConnectionString`连接类型的帐户，您可以编辑帐户身份验证信息，包括访问ID、密钥或连接字符串等信息。 您还可以更新帐户的名称和描述。

   ![编辑详细信息访问密钥](../assets/ui/update-accounts/edit-details-key.png)

   * 对于使用`Bearer token`连接类型的帐户，您可以根据需要输入新的持有者令牌。 您还可以更新帐户的名称和描述。

   ![编辑详细信息Bearer令牌](../assets/ui/update-accounts/edit-details-bearer.png)

   * 对于使用`Server to server`连接类型的帐户，您可以更新帐户的名称和描述。

   ![编辑服务器到服务器的详细信息](../assets/ui/update-accounts/edit-details-s2s.png)

5. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以完成帐户详细信息更新。

## 后续步骤

通过学习本教程，您已成功使用&#x200B;**[!UICONTROL 目标]**&#x200B;工作区来更新现有帐户。

有关目标的详细信息，请参阅[目标概述](../catalog/overview.md)。