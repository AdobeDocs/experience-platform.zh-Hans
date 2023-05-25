---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询；查询编辑器；查询编辑器；
solution: Experience Platform
title: 查询服务凭据指南
description: Adobe Experience Platform查询服务提供了一个用户界面，可用于编写和执行查询、查看以前执行的查询以及访问由您组织内的用户保存的查询。
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 3%

---

# 凭据指南

Adobe Experience Platform查询服务允许您与外部客户端连接。 您可以使用过期凭据或不过期凭据连接到这些外部客户端。

## 过期凭据 {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="客户端的 SSL 模式"
>abstract="必须在连接到查询服务的客户端中启用 SSL。确保 SSL 模式设置为“要求”。"

您可以使用过期凭据快速设置与外部客户端的连接。

![突出显示“即将过期的凭据”部分的“查询仪表板凭据”选项卡。](../images/ui/credentials/expiring-credentials.png)

此 **[!UICONTROL 过期凭据]** 一节提供了以下信息：

- **[!UICONTROL 主机]**：要将客户端连接到的主机名称。 这会合并您的组织名称，如Platform UI顶部功能区中所示。
- **[!UICONTROL 端口]**：要连接的主机端口号。
- **[!UICONTROL 数据库]**：要连接客户端的数据库名称。
- **[!UICONTROL 用户名]**：用于连接到查询服务的用户名。
- **[!UICONTROL 密码]**：用于连接到查询服务的密码。 为了安全起见，UI中的密码进行了哈希处理。 选择复制图标(![复制图标。](../images/ui/credentials/copy-icon.png))以将完整的未哈希凭据复制到剪贴板。
- **[!UICONTROL PSQL命令]**：自动插入所有相关信息的命令，以便在命令行上使用PSQL连接到Query Service。
- **[!UICONTROL 过期]**：过期凭据的过期日期和时间。 令牌的默认有效期为24小时，但可以在Admin Console的高级设置中进行更改。

>[!TIP]
>
>要更改与查询服务的过期凭据连接的会话生命周期，请导航到 [Admin Console](https://adminconsole.adobe.com/) 并选择以下屏幕选项： **设置** > **隐私和安全性** > **身份验证设置** > **高级设置** > **最长会话时长**.
>
>![“Admin Console设置”选项卡，其中高亮显示了“隐私和安全性”、“身份验证设置”和“最长会话时长”。](../images/ui/credentials/max-session-life.png)
>
>请参阅Adobe帮助文档，以了解有关 [高级设置](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) 管理控制台提供的。

## 未过期的凭据 {#non-expiring-credentials}

您可以使用不会过期的凭据来设置与外部客户端的更永久的连接。

### 先决条件

在生成不会过期的凭据之前，必须在Adobe Admin Console中完成以下步骤：

1. 登录 [Adobe Admin Console](https://adminconsole.adobe.com/) 并从顶部导航栏中选择相关组织。
2. [选择产品配置文件。](../../access-control/ui/browse.md)
3. [配置两者 **沙盒** 和 **管理查询服务集成** 权限](../../access-control/ui/permissions.md) 产品配置文件的。
4. [将新用户添加到产品配置文件](../../access-control/ui/users.md) 因此授予了他们配置的权限。
5. [将用户添加为产品配置文件管理员](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) 允许为任何活动的产品配置文件创建帐户。
6. [将用户添加为产品配置文件开发人员](https://helpx.adobe.com/cn/enterprise/using/manage-developers.html) 以创建集成。

要详细了解如何分配权限，请阅读以下文档： [访问控制](../../access-control/home.md).

现在，已在Adobe Developer Console中配置了用户使用过期凭据功能所需的所有权限。

### 生成凭据

要创建一组不会过期的凭据，请返回平台UI并选择 **[!UICONTROL 查询]** 从左侧导航访问 [!UICONTROL 查询] 工作区。 接下来，选择 **[!UICONTROL 凭据]** 选项卡，后接 **[!UICONTROL 生成凭据]**.

![突出显示“凭据”选项卡和“生成凭据”的“查询”仪表板。](../images/ui/credentials/generate-credentials.png)

此时将显示一个对话框，允许您生成凭据。 要创建不会过期的凭据，必须提供以下详细信息：

- **[!UICONTROL 名称]**：您生成的凭据的名称。
- **[!UICONTROL 描述]**：（可选）对您生成的凭据的描述。
- **[!UICONTROL 分配给]**：凭据将分配到的用户。 此值应为创建凭据的用户的电子邮件地址。
- **[!UICONTROL 密码]** （可选）凭据的可选密码。 如果未设置密码，Adobe将自动为您生成密码。

提供所有必需详细信息后，选择 **[!UICONTROL 生成凭据]** 以生成您的凭据。

![此时将突出显示“生成凭据”对话框。](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>时间 **[!UICONTROL 生成凭据]** ，则会将配置JSON文件下载到您的本地计算机。 因为Adobe会 **非** 记录生成的凭据，您必须安全地存储下载的文件并保留凭据的记录。
>
>此外，如果凭据未使用90天，则将清除凭据。

配置JSON文件包含技术帐户名称、技术帐户ID和凭据等信息。 它采用以下格式提供。

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

保存生成的凭据后，选择 **[!UICONTROL 关闭]**. 您现在可以看到所有不会过期的凭据的列表。

![突出显示“未过期的凭据”部分的“查询仪表板凭据”选项卡。](../images/ui/credentials/list-credentials.png)

您可以编辑或删除不会过期的凭据。 要编辑未过期的凭据，请选择铅笔图标(![铅笔图标。](../images/ui/credentials/edit-icon.png))。要删除未过期的凭据，请选择删除图标(![垃圾桶图标。](../images/ui/credentials/delete-icon.png))。

编辑未过期的凭据时，将显示一个模式窗口。 您可以提供以下详细信息以进行更新：

- **[!UICONTROL 名称]**：您生成的凭据的名称。
- **[!UICONTROL 描述]**：（可选）对您生成的凭据的描述。
- **[!UICONTROL 分配给]**：凭据将分配到的用户。 此值应为创建凭据的用户的电子邮件地址。

![更新帐户对话框。](../images/ui/credentials/update-credentials.png)

提供所有必需详细信息后，选择 **[!UICONTROL 更新帐户]** 以完成凭据的更新。

## 使用凭据连接到外部客户端 {#use-credential-to-connect}

您可以使用过期凭据或不过期凭据与外部客户端(例如Aqua Data Studio、Looker或Power BI)连接。 这些凭据的输入方法因外部客户端而异。 有关使用这些凭据的特定说明，请参阅外部客户端的文档。

该图像指示在UI中找到的每个参数的位置，但不会过期的凭据的密码除外。 虽然过期凭据由其JSON配置文件提供，但您可以在以下位置查看过期凭据： **凭据** 选项卡。

![突出显示“即将过期的凭据”部分的查询工作区凭据选项卡。](../images/ui/credentials/expiring-credentials.png)

下表概述了连接到外部客户端通常所需的参数。

>[!NOTE]
>
>使用未过期的凭据连接到主机时，仍需要使用 [!UICONTROL 过期凭据] 部分（密码和用户名除外）。
>输入用户名和密码的格式使用冒号分隔的值，如本示例所示 `username:{your_username}` 和 `password:{password_string}`.

| 参数 | 描述 | 示例 |
|---|---|---|
| **服务器/主机** | 要连接的服务器/主机的名称。 <ul><li>此值用于即将过期的凭据和非即将过期的凭据，并采用 `server.adobe.io`. 该值位于 **[!UICONTROL 主机]** 在 [!UICONTROL 过期凭据] 部分。</ul></li> | `acme.platform.adobe.io` |
| **端口** | 要连接的服务器/主机的端口。 <ul><li>此值同时用于过期凭据和不过期凭据，并位于 **[!UICONTROL 端口]** 在 [!UICONTROL 过期凭据] 部分。</ul></li> | `80` |
| **数据库** | 要连接的数据库。 <ul><li>此值用于过期凭据和未过期凭据，并位于 **[!UICONTROL 数据库]** 在 [!UICONTROL 过期凭据] 部分。 </ul></li> | `prod:all` |
| **用户名** | 连接到外部客户端的用户名。 <ul><li>此值同时用于过期凭据和非过期凭据。 它以前采用字母数字字符串的形式 `@AdobeOrg`. 此值位于 **[!UICONTROL 用户名]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **密码** | 连接到外部客户端的用户的密码。 <ul><li>如果您使用的是即将过期的凭据，这可以在以下位置找到 **[!UICONTROL 密码]** 在 [!UICONTROL 过期凭据] 部分。</li><li>如果您使用的是不会过期的凭据，此值是来自technicalAccountID的拼接参数和从配置JSON文件获取的凭据。 密码值采用以下形式： `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>即将过期的凭据密码超过一千个字符的字母数字字符串。 不提供示例。</li><li>不会过期的凭据密码如下：<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## 后续步骤

现在，您已了解过期凭据和不过期凭据的工作方式，可以使用这些凭据连接到外部客户端。 有关外部客户端的详细信息，请阅读 [connect clients to Query Service指南](../clients/overview.md).
