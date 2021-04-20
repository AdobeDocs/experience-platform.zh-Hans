---
keywords: 更新目标帐户；目标帐户；如何更新帐户
title: 更新目标帐户
type: Tutorial
description: 本教程列表了在Adobe Experience Platform UI中更新目标帐户的步骤
exl-id: afb41878-4205-4c64-af4d-e2740f852785
translation-type: tm+mt
source-git-commit: e436d7147c613dad5b2ff596a412759fd60d228c
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 1%

---

# 更新目标帐户

## 概述 {#overview}

**[!UICONTROL Accounts]**&#x200B;选项卡显示您已与各种目标建立的连接的详细信息。 有关您可以获取的每个目标上的所有信息，请参阅下表：

![“帐户”选项卡](../assets/ui/update-accounts/destination-accounts.png)

| 元素 | 描述 |
|---|---|
| [!UICONTROL Platform] | 您为其设置连接的目标。 |
| [!UICONTROL Connection Type] | 表示到存储存储段或目标的连接类型。 <ul><li>对于电子邮件营销目标：可以是S3或FTP。</li><li>对于实时广告目标：服务器到服务器</li><li>对于Amazon S3云存储目标：访问密钥 </li><li>对于SFTP云存储目标：SFTP的基本身份验证</li></ul> |
| [!UICONTROL Username] | 您在[连接目标向导](../catalog/email-marketing/overview.md#connect-destination)中选择的用户名。 |
| [!UICONTROL Destinations] | 表示与为目标创建的基本信息连接的唯一成功目标流的数量。 |
| [!UICONTROL Authorized] | 到此目标的连接被授权的日期。 |

## 更新帐户{#update}

请按照以下步骤将连接详细信息更新到现有目标。

1. 登录到[Experience PlatformUI](https://platform.adobe.com/)并从左侧导航栏中选择&#x200B;**[!UICONTROL Destinations]**。 从顶部标题中选择&#x200B;**[!UICONTROL Accounts]**&#x200B;以视图现有帐户。

   ![“帐户”选项卡](../assets/ui/update-accounts/accounts-tab.png)

2. 选择左上角的过滤器图标![过滤器图标](../assets/ui/update-accounts/filter.png)以启动排序面板。 排序面板提供所有目标的列表。 您可以从列表中选择多个目标，以查看与所选目标关联的帐户的筛选选择。

   ![筛选目标](../assets/ui/update-accounts/filter-accounts.png)

3. 在&#x200B;**[!UICONTROL Platform]**&#x200B;列中选择![编辑帐户按钮](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Edit]**&#x200B;按钮，以编辑帐户信息。

   ![“帐户”选项卡](../assets/ui/update-accounts/accounts-edit.png)

4. 输入您更新的帐户凭据。

   * 对于使用`OAuth2`连接类型的帐户，请选择&#x200B;**[!UICONTROL Reconnect OAuth]**&#x200B;以续订您的帐户凭据。

      ![编辑详细信息OAuth](../assets/ui/update-accounts/edit-details-oauth.png)


   * 对于使用`Access Key`或`ConnectionString`连接类型的帐户，您可以编辑帐户身份验证信息，包括访问ID、密钥或连接字符串等信息。

      ![编辑详细信息访问密钥](../assets/ui/update-accounts/edit-details-key.png)

5. 选择&#x200B;**[!UICONTROL Save]**&#x200B;以完成凭据更新。
