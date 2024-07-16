---
keywords: Experience Platform；主页；热门主题；Marketo Engage；marketo engage；marketo
solution: Experience Platform
title: 验证您的Marketo源连接器
description: 本文档提供了有关如何生成Marketo身份验证凭据的信息。
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# 验证您的[!DNL Marketo Engage]源连接器

在创建[!DNL Marketo Engage] （以下简称“[!DNL Marketo]”）源连接器之前，您必须首先通过[!DNL Marketo]界面设置自定义服务，并检索Munchkin ID、客户端ID和客户端密钥的值。

以下文档提供了有关如何获取身份验证凭据以创建[!DNL Marketo]源连接器的步骤。

## 设置新角色

获取身份验证凭据的第一步是通过[[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1)接口设置新角色。

登录到[!DNL Marketo]并从顶部导航栏中选择&#x200B;**[!DNL Admin]**。

新角色的![管理员](../images/marketo/home.png)

*[!DNL Users & Role]s*&#x200B;页面包含有关用户、角色和登录历史记录的信息。 要创建新角色，请从顶部标题中选择&#x200B;**[!DNL Roles]**，然后选择&#x200B;**[!DNL New Role]**。

![新角色](../images/marketo/new-role.png)

出现&#x200B;**[!DNL Create New Role]**&#x200B;对话框。 提供名称和描述，然后选择要为此角色授予的权限。 权限仅限于特定工作区，用户只能在自己具有权限的工作区中执行操作。

选择要授予的权限后，选择&#x200B;**[!DNL Create]**。

![create-new-role](../images/marketo/create-new-role.png)

使用[!DNL Marketo]创建角色时，您可以管理API上受限制的权限。 您无需选择“访问API”，而是可以通过选择以下权限为角色提供最低级别的访问权限：

* [!DNL Read-Only Activity]
* [!DNL Read-Only Assets]
* [!DNL Read-Only Campaign]
* [!DNL Read-Only Company]
* [!DNL Read-Only Custom Object]
* [!DNL Read-Only Custom Object Type]
* [!DNL Read-Only Named Account]
* [!DNL Read-Only Named Account List]
* [!DNL Read-Only Opportunity]
* [!DNL Read-Only Person]
* [!DNL Read-Only Sales Person]

## 设置新用户

与角色类似，您可以从&#x200B;**[!DNL Users & Roles]**&#x200B;页面设置新用户。 **[!DNL Users]**&#x200B;页面提供当前在Marketo中设置的活动用户列表。 选择&#x200B;**[!DNL Invite New User]**&#x200B;以配置新用户。

![邀请 — 新用户](../images/marketo/invite-new-user.png)

弹出对话框菜单出现。 为您的电子邮件、名字、姓氏和原因提供适当的信息。 在此步骤中，您还可以为所邀请的新用户帐户设置访问到期日期。 完成后，选择&#x200B;**[!DNL Next]**。

>[!IMPORTANT]
>
>在设置新用户时，必须向用户分配访问权限，并且该用户严格专为您正在创建的自定义服务。

![用户信息](../images/marketo/new-user-info.png)

在&#x200B;**[!DNL Permissions]**&#x200B;步骤中选择相应的字段，然后选中&#x200B;**[!DNL API Only]**&#x200B;复选框以向新用户提供API角色。 选择&#x200B;**[!DNL Next]**&#x200B;以继续。

![权限](../images/marketo/permissions.png)

要完成该过程，请选择&#x200B;**[!DNL Send]**。

![消息](../images/marketo/message.png)

## 设置自定义服务

建立新用户后，您可以设置自定义服务以检索新凭据。 从管理页面中，选择&#x200B;**[!DNL LaunchPoint]**。

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

**[!DNL Installed services]**&#x200B;页面包含现有服务的列表，要创建新的自定义服务，请选择&#x200B;**[!DNL New]**，然后选择&#x200B;**[!DNL New Service]**。

![新服务](../images/marketo/new-service.png)

为您的新服务提供一个描述性显示名称，然后从&#x200B;**[!DNL Service]**&#x200B;下拉菜单中选择&#x200B;**[!DNL Custom]**。 提供相应的说明，然后从&#x200B;**[!DNL API Only User]**&#x200B;下拉菜单中选择要设置的用户。 填写完必要的详细信息后，选择&#x200B;**[!DNL Create]**&#x200B;以创建新的自定义服务。

![创建](../images/marketo/create.png)

## 获取您的客户端ID和客户端密码

创建新的自定义服务后，您现在可以检索客户端ID和客户端密钥的值。 从&#x200B;**[!DNL Installed Services]**&#x200B;菜单中，找到要访问的自定义服务，然后选择&#x200B;**[!DNL View Details]**。

![查看详细信息](../images/marketo/view-details.png)

此时将显示一个对话框，其中包含您的客户端ID和客户端密码。

![凭据](../images/marketo/credentials.png)

## 获取Munchkin ID

要验证[!DNL Marketo]源连接器，必须完成的最后一个步骤是检索Munchkin ID。 从管理页面中，选择&#x200B;**[!DNL Integration]**&#x200B;面板下的&#x200B;**[!DNL Munchkin]**。

![admin-munchkin](../images/marketo/admin-munchkin.png)

此时会显示&#x200B;*[!DNL Munchkin]*&#x200B;页面，您的唯一Munchkin ID将列在面板顶部。

![munchkin-Id](../images/marketo/munchkin-id.png)

结合客户端ID和客户端密码，您可以使用Munchkin ID配置新帐户并在Experience Platform上[创建新的 [!DNL Marketo] 源连接](../../../tutorials/ui/create/adobe-applications/marketo.md)。
