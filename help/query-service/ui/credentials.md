---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询编辑器；查询编辑器；查询编辑器；查询编辑器；
solution: Experience Platform
title: 查询服务UI指南
topic-legacy: guide
description: Adobe Experience Platform查询服务提供了一个用户界面，可用于编写和执行查询、查看以前执行的查询，以及访问由IMS组织内的用户保存的查询。
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: aabe89f236bc68a51f14ee1909687982f4fe5973
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---


# 凭据指南

Adobe Experience Platform查询服务允许您与外部客户端连接。 您可以使用过期凭据或未过期的凭据连接到这些外部客户端。

## 过期凭据

您可以使用过期凭据快速设置与外部客户端的连接。

![](../images/ui/credentials/expiring-credentials.png)

**[!UICONTROL 过期凭据]**&#x200B;部分提供以下信息：

- **[!UICONTROL 主机]**:要连接到的主机的名称。要连接到查询服务，这将包括您当前使用的IMS组织的名称。
- **[!UICONTROL 端口]**:要连接到的主机的端口号。
- **[!UICONTROL 数据库]**:要连接到的数据库的名称。
- **[!UICONTROL 用户名]**:用于连接到查询服务的用户名。
- **[!UICONTROL 密码]**:用于连接到查询服务的密码。
- **[!UICONTROL PSQL命令]**:命令自动插入所有相关信息，以便您使用命令行上的PSQL连接到查询服务。
- **[!UICONTROL 过期]**:过期凭据的到期日期。凭据在生成后24小时过期。

## 未过期的凭据

您可以使用未过期的凭据来设置与外部客户端的更永久连接。

要创建一组未过期的凭据，请选择&#x200B;**[!UICONTROL 生成凭据]**。

>[!NOTE]
>
>在创建未过期的凭据之前，您必须同时具有&#x200B;**沙盒**&#x200B;和&#x200B;**管理查询服务集成**&#x200B;权限。 要了解如何分配这些权限，请阅读[Access Control](../../access-control/home.md)上的文档。

![](../images/ui/credentials/generate-credentials.png)

此时会出现生成凭据模式窗口。 要创建未过期的凭据，您需要提供以下详细信息：

- **[!UICONTROL 名称]**:要生成的凭据的名称。
- **[!UICONTROL 描述]**:（可选）对要生成的凭据的描述。
- **[!UICONTROL 分配给]**:将为其分配凭据的用户。此值应为创建凭据的用户的电子邮件地址。
- **[!UICONTROL 密码]** （可选）凭据的可选密码。如果未设置密码，Adobe将自动为您生成密码。

提供所有必需的详细信息后，请选择&#x200B;**[!UICONTROL 生成凭据]**&#x200B;以生成凭据。

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>选择&#x200B;**[!UICONTROL 生成凭据]**&#x200B;按钮后，将生成一个配置文件，其中包含技术帐户名称、技术帐户ID和凭据等信息。 由于Adobe **不**&#x200B;记录生成的凭据，因此&#x200B;**必须**&#x200B;安全地存储下载的文件并保留凭据记录。
>
>此外，如果凭据90天未使用，则凭据将被删除。

现在，您已保存生成的凭据，请选择&#x200B;**[!UICONTROL 关闭]**。 您现在可以看到所有未过期凭据的列表。

![](../images/ui/credentials/list-credentials.png)

您可以编辑或删除未过期的凭据。 要编辑未过期的凭据，请选择铅笔图标(![](../images/ui/credentials/edit-icon.png))。 要删除未过期的凭据，请选择删除图标(![](../images/ui/credentials/delete-icon.png))。

编辑未过期的凭据时，会显示一个模式窗口。 您可以提供以下详细信息以进行更新：

- **[!UICONTROL 名称]**:要生成的凭据的名称。
- **[!UICONTROL 描述]**:（可选）对要生成的凭据的描述。
- **[!UICONTROL 分配给]**:将为其分配凭据的用户。此值应为创建凭据的用户的电子邮件地址。

![](../images/ui/credentials/update-credentials.png)

提供所有必需的详细信息后，请选择&#x200B;**[!UICONTROL 更新帐户]**&#x200B;以完成凭据更新。

## 使用凭据连接到外部客户端

您可以使用过期或未过期的凭据与外部客户端(如Aqua Data Studio、Looker或Power BI)进行连接。

连接到这些外部客户端时，通常需要包含以下信息：

- **服务器/主机**:您连接到的服务器/主机的名称。此值采用`server.adobe.io`格式，可在过期凭据部分的&#x200B;**[!UICONTROL Host]**&#x200B;下找到。
- **端口**:要连接的服务器/主机的端口。此值位于过期凭据部分的&#x200B;**[!UICONTROL 端口]**&#x200B;下。 端口的示例值为`80`。
- **用户名**:连接到外部客户端的用户的用户名。此格式为`ID@AdobeOrg`，可在过期凭据部分的&#x200B;**[!UICONTROL Username]**&#x200B;下找到。
- **密码**:连接到外部客户端的用户的密码。如果您使用的是过期凭据，则可在过期凭据部分的&#x200B;**[!UICONTROL Password]**&#x200B;下找到此凭据。 如果您使用的是未过期的凭据，则此值由以下格式的技术帐户ID和凭据组成：`technicalAccountId:credential`。
- **数据库**:您连接到的数据库。此值位于过期凭据部分的&#x200B;**[!UICONTROL Database]**&#x200B;下。 数据库的示例值为`prod:all`。

## 后续步骤

现在，您已了解过期和未过期凭据的工作方式，接下来可以使用这些凭据连接到外部客户端。 有关外部客户端的详细信息，请阅读[将客户端连接到查询服务指南](../clients/overview.md)。