---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询；查询编辑器；查询编辑器；查询编辑器；
solution: Experience Platform
title: 查询服务凭据指南
description: Adobe Experience Platform查询服务提供了一个用户界面，可用于编写和执行查询、查看先前执行的查询以及访问由您组织内的用户保存的查询。
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: ba4ff2715d4e3eb71377542ab2361b967cd3ac11
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 1%

---

# 凭据指南

Adobe Experience Platform查询服务允许您与外部客户端连接。 您可以使用过期凭据或不过期凭据连接到这些外部客户端。

>[!NOTE]
>
>凭据面板并非自动对所有用户可用。 请联系您的Adobe客户团队以申请 [!UICONTROL 凭据] 选项卡，以便在需要时包含在查询服务工作区中。 如有请求，此更改将在整个组织中实施，并由Adobe的工程团队执行。 它不是由用户控制的设置。

## 过期凭据 {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="客户端的 SSL 模式"
>abstract="必须在连接到查询服务的客户端中启用 SSL。确保 SSL 模式设置为“要求”。"

您可以使用过期凭据快速设置与外部客户端的连接。

![突出显示“过期凭据”部分的查询仪表板凭据选项卡。](../images/ui/credentials/expiring-credentials.png)

此 **[!UICONTROL 过期凭据]** 部分提供了以下信息：

- **[!UICONTROL 主机]**：要将客户端连接到的主机名称。 这会合并您的组织名称，如Platform UI顶部功能区中所示。
- **[!UICONTROL 端口]**：要连接的主机端口号。
- **[!UICONTROL 数据库]**：要连接客户端的数据库名称。
- **[!UICONTROL 用户名]**：用于连接到查询服务的用户名。
- **[!UICONTROL 密码]**：用于连接到查询服务的密码。 为了安全起见，UI中的密码已进行哈希处理。 选择复制图标(![复制图标。](../images/ui/credentials/copy-icon.png))以将完整的未散列凭据复制到剪贴板。
- **[!UICONTROL PSQL命令]**：自动插入所有相关信息以供您在命令行中使用PSQL连接到Query Service的命令。
- **[!UICONTROL 过期]**：过期凭据的过期日期和时间。 令牌的默认有效期为24小时，但可以在Admin Console的高级设置中更改。

>[!TIP]
>
>要更改与查询服务的过期凭据连接的会话生命周期，请导航到 [Admin Console](https://adminconsole.adobe.com/) 并选择以下屏幕选项： **设置** > **隐私和安全性** > **身份验证设置** > **高级设置** > **最长会话时长**.
>
>![“Admin Console设置”选项卡，其中突出显示“隐私和安全性”、“身份验证设置”和“最长会话寿命”。](../images/ui/credentials/max-session-life.png)
>
>有关以下内容的更多信息，请参阅Adobe帮助 [高级设置](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) 管理控制台提供的。

### 连接到查询会话中的Customer Journey Analytics数据 {#connect-to-customer-journey-analytics}

使用带有Power BI或Tableau的Customer Journey AnalyticsBI扩展来访问您的Customer Journey Analytics [数据视图](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views) 使用SQL。 通过将查询服务与BI扩展集成，您可以直接在查询服务会话中访问数据视图。 此集成简化了使用查询服务作为其PostgreSQL接口的BI工具的功能。 此功能消除了BI工具中重复数据视图的需要，确保跨平台的一致报告，并简化了Customer Journey Analytics数据与BI平台中其他源的集成。

请参阅文档以了解如何 [将查询服务连接到各种桌面客户端应用程序](../clients/overview.md) 例如 [Power BI](../clients/power-bi.md) 或 [表格](../clients/tableau.md)

>[!IMPORTANT]
>
>需要Customer Journey Analytics工作区项目和数据视图才能使用此功能。

要在Power BI或Tableau中访问Customer Journey Analytics数据，请选择 [!UICONTROL 数据库] 下拉菜单，然后选择 `prod:cja` 从可用选项删除。 接下来，复制您的 [!DNL Postgres] 在Power BI或Tableau配置中使用的身份证明参数（主机、端口、数据库、用户名等）。

![突出显示数据库下拉列表的“查询服务凭据”选项卡。](../images/ui/credentials/database-dropdown.png)

>[!NOTE]
>
>当您连接Power BI或Tableau以Customer Journey Analytics时，会使用查询服务“并发会话”权利。 如果需要其他会话和查询，可以购买额外的临时查询用户包附加组件以获取五个额外的并发会话和一个额外的并发查询。

您还可以直接从Query Editor或Postgres CLI访问Customer Journey Analytics数据。 为此，请参考 `cja` 数据库。 请参阅查询编辑器 [查询创作指南](./user-guide.md#query-authoring) 有关如何写入、执行和保存查询的详细信息。

请参阅 [BI扩展指南](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/bi-extension) 有关使用SQL访问Customer Journey Analytics数据视图的完整说明。

## 未过期的凭据 {#non-expiring-credentials}

您可以使用不会过期的凭据来设置与外部客户端的更永久的连接。

>[!NOTE]
>
>未过期的凭据具有以下限制：<br><ul><li>用户必须使用由以下组成的用户名和密码登录 `{technicalAccountId}:{credential}`. 欲知更多信息，请参见 [生成凭据](#generate-credentials) 部分。</li><li>创建过期凭据后，将创建具有一组基本权限的新角色，该角色允许用户查看架构和数据集。 “管理查询”权限也已分配给此角色，以与查询服务一起使用。</li><li>当列出查询对象时，第三方客户端可能会执行与预期不同的操作。 例如，某些第三方客户，如 [!DNL DB Visualizer] 不会在左侧面板中显示视图名称。 但是，如果在SELECT查询中调用视图名称，则视图名称可访问。 同样地， [!DNL PowerUI] 可能不会列出通过SQL创建的要选择用于创建功能板的临时视图。</li></ul>

### 先决条件

在生成不会过期的凭据之前，必须在Adobe Admin Console中完成以下步骤：

1. 登录 [Adobe Admin Console](https://adminconsole.adobe.com/) 并从顶部导航栏中选择相关的组织。
2. [选择产品配置文件。](../../access-control/ui/browse.md)
3. [配置两者 **沙盒** 和 **管理查询服务集成** 权限](../../access-control/ui/permissions.md) 用于产品配置文件。
4. [将新用户添加到产品配置文件](../../access-control/ui/users.md) 因此授予了他们配置的权限。
5. [将用户添加为产品配置文件管理员](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) 允许为任何活动的产品配置文件创建帐户。
6. [将用户添加为产品配置文件开发人员](https://helpx.adobe.com/cn/enterprise/using/manage-developers.html) 以创建集成。

要详细了解如何分配权限，请阅读以下文档： [访问控制](../../access-control/home.md).

现在，已在Adobe Developer Console中配置了用户使用过期凭据功能所需的所有权限。

### 生成凭据 {#generate-credentials}

要创建一组不会过期的凭据，请返回到Platform UI并选择 **[!UICONTROL 查询]** 从左侧导航访问 [!UICONTROL 查询] 工作区。 接下来，选择 **[!UICONTROL 凭据]** 选项卡，后接 **[!UICONTROL 生成凭据]**.

![突出显示“凭据”选项卡和“生成凭据”的“查询”仪表板。](../images/ui/credentials/generate-credentials.png)

将出现一个对话框，允许您生成凭据。 要创建不会过期的凭据，必须提供以下详细信息：

- **[!UICONTROL 名称]**：您生成的凭据的名称。
- **[!UICONTROL 描述]**：（可选）对您生成的凭据的描述。
- **[!UICONTROL 分派给]**：凭据将分配给的用户。 此值应为创建凭据的用户的电子邮件地址。
- **[!UICONTROL 密码]** （可选）凭据的可选密码。 如果未设置密码，Adobe将自动为您生成密码。

提供所有必需的详细信息后，选择 **[!UICONTROL 生成凭据]** 以生成您的凭据。

![将突出显示生成凭据对话框。](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>时间 **[!UICONTROL 生成凭据]** ，则会将配置JSON文件下载到本地计算机。 因为Adobe会 **非** 记录生成的凭据，您必须安全地存储下载的文件并保留凭据的记录。
>
>此外，如果凭据未使用90天，则凭据将被注销。

配置JSON文件包含技术帐户名称、技术帐户ID和凭据等信息。 提供时采用以下格式。

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

保存生成的凭据后，选择 **[!UICONTROL 关闭]**. 您现在可以看到所有未过期的凭据的列表。

![突出显示未过期的凭据部分的查询仪表板凭据选项卡。](../images/ui/credentials/list-credentials.png)

您可以编辑或删除未过期的凭据。 要编辑不会过期的凭据，请选择铅笔图标(![铅笔图标。](../images/ui/credentials/edit-icon.png))。要删除未过期的凭据，请选择删除图标(![垃圾桶图标。](../images/ui/credentials/delete-icon.png))。

编辑未过期的凭据时，将显示一个模式窗口。 您可以提供以下详细信息以进行更新：

- **[!UICONTROL 名称]**：您生成的凭据的名称。
- **[!UICONTROL 描述]**：（可选）对您生成的凭据的描述。
- **[!UICONTROL 分派给]**：凭据将分配给的用户。 此值应为创建凭据的用户的电子邮件地址。

![更新帐户对话框。](../images/ui/credentials/update-credentials.png)

提供所有必需的详细信息后，选择 **[!UICONTROL 更新帐户]** 以完成凭据的更新。

## 使用凭据连接到外部客户端 {#use-credential-to-connect}

您可以使用过期凭据或不过期凭据与外部客户端(例如Aqua Data Studio、Looker或Power BI)连接。 这些凭据的输入方法因外部客户端而异。 有关使用这些凭据的特定说明，请参阅外部客户端的文档。

该图像指示在UI中找到的每个参数的位置，但不会过期的凭据的密码除外。 虽然过期凭据由其JSON配置文件提供，但您可以在以下位置查看过期凭据： **凭据** 选项卡。

![查询工作区凭据选项卡，其中高亮显示过期凭据部分。](../images/ui/credentials/expiring-credentials.png)

下表概述了连接到外部客户端通常所需的参数。

>[!NOTE]
>
>使用未过期的凭据连接到主机时，仍需要使用 [!UICONTROL 过期凭据] 部分（密码和用户名除外）。
>输入用户名和密码的格式使用冒号分隔的值，如本示例所示 `username:{your_username}` 和 `password:{password_string}`.

| 参数 | 描述 | 示例 |
|---|---|---|
| **服务器/主机** | 要连接的服务器/主机的名称。 <ul><li>此值用于过期凭据和非过期凭据，其形式为 `server.adobe.io`. 该值位于下 **[!UICONTROL 主机]** 在 [!UICONTROL 过期凭据] 部分。</ul></li> | `acme.platform.adobe.io` |
| **端口** | 要连接的服务器/主机的端口。 <ul><li>此值同时用于过期凭据和不过期凭据，可在以下位置找到 **[!UICONTROL 端口]** 在 [!UICONTROL 过期凭据] 部分。</ul></li> | `80` |
| **数据库** | 要连接的数据库。 <ul><li>此值用于过期凭据和不过期凭据，并位于 **[!UICONTROL 数据库]** 在 [!UICONTROL 过期凭据] 部分。 </ul></li> | `prod:all` |
| **用户名** | 连接到外部客户端的用户名。 <ul><li>此值用于过期凭据和非过期凭据。 它以前采用字母数字字符串的形式 `@AdobeOrg`. 此值位于 **[!UICONTROL 用户名]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **密码** | 连接到外部客户端的用户的密码。 <ul><li>如果您使用的是过期凭据，则可在 **[!UICONTROL 密码]** 内部 [!UICONTROL 过期凭据] 部分。</li><li>如果您使用的是未过期的凭据，此值是来自technicalAccountID的拼接参数和从配置JSON文件获取的凭据。 密码值采用以下形式： `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>即将过期的凭据密码包含超过一千个字符的字母数字字符串。 没有给出任何示例。</li><li>未过期的凭据密码如下：<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## 后续步骤

现在，您已了解过期凭据和不过期凭据的工作方式，可以使用这些凭据连接到外部客户端。 有关外部客户端的详细信息，请阅读 [连接客户端至查询服务指南](../clients/overview.md).
