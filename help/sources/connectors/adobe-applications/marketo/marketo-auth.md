---
keywords: Experience Platform；主页；热门主题；Marketo Engage；营销参与；营销
solution: Experience Platform
title: 验证Marketo源连接器
topic: 概述
description: 此文档提供有关如何生成Marketo身份验证凭据的信息。
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# （测试版）验证[!DNL Marketo Engage]源连接器

>[!IMPORTANT]
>
>[!DNL Marketo Engage]源当前处于测试状态。 其功能和文档可能会发生更改。

在创建[!DNL Marketo Engage]（以下称为“[!DNL Marketo]”）源连接器之前，必须首先通过[!DNL Marketo]接口设置自定义服务，并检索Munchkin ID、客户端ID和客户端机密的值。

以下文档提供了如何获取身份验证凭据以创建[!DNL Marketo]源连接器的步骤。

## 设置新角色

获取身份验证凭据的第一步是通过[[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1)接口设置新角色。

登录[!DNL Marketo]并从顶部导航栏中选择&#x200B;**[!DNL Admin]**。

![管理新角色](../images/marketo/home.png)

*[!DNL Users & Role]s*&#x200B;页面包含有关用户、角色和登录历史记录的信息。 要创建新角色，请从顶部标题中选择&#x200B;**[!DNL Roles]**，然后选择&#x200B;**[!DNL New Role]**。

![新角色](../images/marketo/new-role.png)

出现&#x200B;**[!DNL Create New Role]**&#x200B;对话框。 提供名称和说明，然后选择您要授予此角色的权限。 权限仅限于特定工作区，用户只能在具有权限的工作区中执行操作。

选择要授予的权限后，选择&#x200B;**[!DNL Create]**。

![create-new-role](../images/marketo/create-new-role.png)

使用[!DNL Marketo]创建角色时，可以管理API上的受限权限。 您可以通过选择以下权限，为角色提供最低访问级别的权限，而不是选择“访问API”：

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

与角色类似，您可以从&#x200B;**[!DNL Users & Roles]**&#x200B;页面设置新用户。 **[!DNL Users]**&#x200B;页面提供当前在Marketo中设置的活动用户的列表。 选择&#x200B;**[!DNL Invite New User]**&#x200B;以设置新用户。

![invite-new-user](../images/marketo/invite-new-user.png)

将出现一个跨窗对话框菜单。 请为您的电子邮件、名字、姓氏和原因提供适当的信息。 在此步骤中，您还可以为要邀请的新用户帐户的访问权限建立到期日期。 完成后，选择&#x200B;**[!DNL Next]**。

>[!IMPORTANT]
>
>设置新用户时，您必须将访问权限分配给严格专用于您创建的自定义服务的用户。

![user-info](../images/marketo/new-user-info.png)

在&#x200B;**[!DNL Permissions]**&#x200B;步骤中选择相应的字段，然后选中&#x200B;**[!DNL API Only]**&#x200B;复选框，为新用户提供API角色。 选择&#x200B;**[!DNL Next]**&#x200B;以继续。

![权限](../images/marketo/permissions.png)

要完成该过程，请选择&#x200B;**[!DNL Send]**。

![消息](../images/marketo/message.png)

## 设置自定义服务

建立新用户后，可以设置自定义服务以检索新凭据。 从管理页面中，选择&#x200B;**[!DNL LaunchPoint]**。

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

**[!DNL Installed services]**&#x200B;页面包含现有服务的列表，若要创建新的自定义服务，请选择&#x200B;**[!DNL New]**，然后选择&#x200B;**[!DNL New Service]**。

![新服务](../images/marketo/new-service.png)

为新服务提供描述性显示名称，然后从&#x200B;**[!DNL Service]**&#x200B;下拉菜单中选择&#x200B;**[!DNL Custom]**。 提供相应的描述，然后从&#x200B;**[!DNL API Only User]**&#x200B;下拉菜单中选择要预配的用户。 填写必要的详细信息后，选择&#x200B;**[!DNL Create]**&#x200B;以创建新的自定义服务。

![create](../images/marketo/create.png)

## 获取您的客户端ID和客户端机密

创建新的自定义服务后，您现在可以检索客户端ID和客户端密码的值。 从&#x200B;**[!DNL Installed Services]**&#x200B;菜单中，找到要访问的自定义服务，然后选择&#x200B;**[!DNL View Details]**。

![视图详细信息](../images/marketo/view-details.png)

将显示一个对话框，其中包含您的客户端ID和客户端机密。

![凭据](../images/marketo/credentials.png)

## 获取您的Munchkin ID

要验证[!DNL Marketo]源连接器，您必须完成的最后一步是检索您的Munchkin ID。 在管理页面的&#x200B;**[!DNL Integration]**&#x200B;面板下选择&#x200B;**[!DNL Munchkin]**。

![admin-munchkin](../images/marketo/admin-munchkin.png)

将显示&#x200B;*[!DNL Munchkin]*&#x200B;页面，面板顶部列出了您唯一的Munchkin ID。

![蒙奇金](../images/marketo/munchkin-id.png)

结合您的客户端ID和客户端机密，您可以使用Munchkin ID配置新帐户，并在Experience Platform上[创建新的 [!DNL Marketo] 源连接](../../../tutorials/ui/create/adobe-applications/marketo.md)。
