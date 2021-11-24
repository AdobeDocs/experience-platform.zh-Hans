---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询编辑器；查询编辑器；查询编辑器；查询编辑器；
solution: Experience Platform
title: 查询服务UI指南
topic-legacy: guide
description: Adobe Experience Platform查询服务提供了一个用户界面，可用于编写和执行查询、查看以前执行的查询，以及访问由IMS组织内的用户保存的查询。
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 87ec2ab37105aefc52abe102d45fd124492ac79f
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 1%

---

# 凭据指南

Adobe Experience Platform查询服务允许您与外部客户端连接。 您可以使用过期凭据或未过期的凭据连接到这些外部客户端。

## 过期凭据

您可以使用过期凭据快速设置与外部客户端的连接。

![](../images/ui/credentials/expiring-credentials.png)

的 **[!UICONTROL 过期凭据]** 部分提供了以下信息：

- **[!UICONTROL 主机]**:要连接到的主机的名称。 要连接到查询服务，这将包括您当前使用的IMS组织的名称。
- **[!UICONTROL 端口]**:要连接到的主机的端口号。
- **[!UICONTROL 数据库]**:要连接到的数据库的名称。
- **[!UICONTROL 用户名]**:用于连接到查询服务的用户名。
- **[!UICONTROL 密码]**:用于连接到查询服务的密码。
- **[!UICONTROL PSQL命令]**:命令自动插入所有相关信息，以便您使用命令行上的PSQL连接到查询服务。
- **[!UICONTROL 过期]**:过期凭据的到期日期。 凭据在生成后24小时过期。

## 未过期的凭据

您可以使用未过期的凭据来设置与外部客户端的更永久连接。

### 先决条件

在生成未过期的凭据之前，您必须在Adobe Admin Console中完成以下步骤：

1. 登录 [Adobe Admin Console](https://adminconsole.adobe.com/) ，然后从顶部导航栏中选择相关组织。
2. [选择产品配置文件。](../../access-control/ui/browse.md)
3. [配置 **沙箱** 和 **管理查询服务集成** 权限](../../access-control/ui/permissions.md) ，以获取产品配置文件。
4. [将新用户添加到产品配置文件](../../access-control/ui/users.md) 这样，他们就可以获得其配置的权限。
5. [将用户添加为产品配置文件管理员](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) 以允许为任何活动的产品用户档案创建帐户。
6. [将用户添加为产品配置文件开发人员](https://helpx.adobe.com/cn/enterprise/using/manage-developers.html) 以创建集成。

要了解有关如何分配权限的更多信息，请阅读 [访问控制](../../access-control/home.md).

现在，在Adobe开发人员控制台中配置了所有所需的权限，以便用户使用过期的凭据功能。

### 生成凭据

要创建一组未过期的凭据，请返回到Platform UI并选择 **[!UICONTROL 查询]** 从左侧导航访问 [!UICONTROL 查询] 工作区。 接下来，选择 **[!UICONTROL 凭据]** 选项卡，后跟 **[!UICONTROL 生成凭据]**.

![](../images/ui/credentials/generate-credentials.png)

此时会显示一个对话框，用于生成凭据。 要创建未过期的凭据，您必须提供以下详细信息：

- **[!UICONTROL 名称]**:要生成的凭据的名称。
- **[!UICONTROL 描述]**:（可选）对要生成的凭据的描述。
- **[!UICONTROL 已分配给]**:将向其分配凭据的用户。 此值应为创建凭据的用户的电子邮件地址。
- **[!UICONTROL 密码]** （可选）凭据的可选密码。 如果未设置密码，Adobe将自动为您生成密码。

提供所有必需的详细信息后，请选择 **[!UICONTROL 生成凭据]** 以生成您的凭据。

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>一旦 **[!UICONTROL 生成凭据]** 按钮时，会将配置JSON文件下载到本地计算机。 因为Adobe **not** 记录生成的凭据，您必须安全地存储下载的文件并保留凭据记录。
>
>此外，如果凭据90天内未使用，则凭据将被删除。

配置JSON文件包含技术帐户名称、技术帐户ID和凭据等信息。 它以以下格式提供。

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

保存生成的凭据后，选择 **[!UICONTROL 关闭]**. 您现在可以看到所有未过期凭据的列表。

![](../images/ui/credentials/list-credentials.png)

您可以编辑或删除未过期的凭据。 要编辑未过期的凭据，请选择铅笔图标(![](../images/ui/credentials/edit-icon.png))。 要删除未过期的凭据，请选择删除图标(![](../images/ui/credentials/delete-icon.png))。

编辑未过期的凭据时，会显示一个模式窗口。 您可以提供以下详细信息以进行更新：

- **[!UICONTROL 名称]**:要生成的凭据的名称。
- **[!UICONTROL 描述]**:（可选）对要生成的凭据的描述。
- **[!UICONTROL 已分配给]**:将向其分配凭据的用户。 此值应为创建凭据的用户的电子邮件地址。

![](../images/ui/credentials/update-credentials.png)

提供所有必需的详细信息后，请选择 **[!UICONTROL 更新帐户]** 以完成凭据更新。

## 使用凭据连接到外部客户端

您可以使用过期或未过期的凭据与外部客户端(如Aqua Data Studio、Looker或Power BI)进行连接。 这些凭据的输入方法将因外部客户端而异。 有关使用这些凭据的具体说明，请参阅外部客户端的文档。

该图像指示在UI中找到的每个参数的位置，但未过期凭据的密码除外。 虽然其JSON配置文件提供了未过期的凭据，但您可以在 **凭据** 选项卡。

![](../images/ui/credentials/expiring-credentials.png)

下表概述了连接到外部客户端通常需要的参数。

>[!NOTE]
>
>在使用未过期的凭据连接到主机时，仍需要使用 [!UICONTROL 过期凭据] 部分，但密码和用户名除外。

| 参数 | 描述 |
|---|---|
| 服务器/主机 | 您连接到的服务器/主机的名称。 <ul><li>此值用于过期的凭据和未过期的凭据，其形式为 `server.adobe.io`. 值位于 **[!UICONTROL 主机]** 在 [!UICONTROL 过期凭据] 中。</ul></li> |
| 端口 | 要连接的服务器/主机的端口。 <ul><li>此值用于过期的凭据和未过期的凭据，可在 **[!UICONTROL 端口]** 在 [!UICONTROL 过期凭据] 中。 端口的示例值为 `80`.</ul></li> |
| 数据库 | 您连接到的数据库。 <ul><li>此值用于过期的凭据和未过期的凭据，可在 **[!UICONTROL 数据库]** 在 [!UICONTROL 过期凭据] 中。 数据库的示例值为 `prod:all`.</ul></li> |
| 用户名 | 连接到外部客户端的用户的用户名。 <ul><li>此值用于过期的凭据和未过期的凭据。 它采用字母数字字符串的形式，在 `@AdobeOrg`. 此值位于 **[!UICONTROL 用户名]**.</li></ul> |
| 密码 | 连接到外部客户端的用户的密码。 <ul><li>如果您使用的凭据已过期，可在 **[!UICONTROL 密码]** 在 [!UICONTROL 过期凭据] 中。</li><li>如果您使用的是未过期的凭据，则此值是technicalAccountID的连接参数和从配置JSON文件获取的凭据。 密码值采用以下形式： `{technicalAccountId}:{credential}`.</li></ul> |

## 后续步骤

现在，您已了解过期和未过期凭据的工作方式，接下来可以使用这些凭据连接到外部客户端。 有关外部客户端的详细信息，请阅读 [将客户端连接到查询服务指南](../clients/overview.md).
