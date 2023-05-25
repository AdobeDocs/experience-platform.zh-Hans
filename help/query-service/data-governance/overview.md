---
title: 查询服务中的数据治理
description: 此概述涵盖Experience Platform查询服务中的数据治理的主要元素。
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: 54a6f508818016df1a4ab2a217bc0765b91df9e9
workflow-type: tm+mt
source-wordcount: '2843'
ht-degree: 1%

---

# 查询服务中的数据治理

Adobe Experience Platform将来自多个企业系统的数据汇集在一起，并允许您根据自己的需求，通过查询服务来清理、形状、操作和扩充数据。 这允许营销人员更好地识别、了解和吸引客户。 由于某些数据可能会受到基于组织政策和法规的使用限制，因此确保充分的数据治理是处理个人信息的一个关键方面。 确保所摄取的数据及其相关操作符合定义的数据使用策略至关重要。

利用Query Service中的数据治理，您可以管理客户数据并确保遵守适用于数据使用的法规、限制和策略。 在确保根据您的业务所定义的法规应用使用策略时，这将发挥关键作用。

建议日常执行数据处理的组织概述、实践和执行这些准则，为所有用户营造注重隐私的环境。

在使用查询服务时，以下类别有助于遵守数据合规性法规：

1. 安全性
1. 审核
1. 数据使用
1. 隐私
<!-- 1. Data hygiene -->

本文档将检查治理的各个不同领域，并演示在使用查询服务时如何促进数据合规性。 请参阅 [治理、隐私和安全概述](../../landing/governance-privacy-security/overview.md) 有关Experience Platform如何让您管理客户数据和确保法规遵从性的更全面的信息。

## 安全性

数据安全是保护数据免受未经授权的访问并确保在整个生命周期内安全访问的过程。 通过应用角色和权限（例如基于角色的访问控制和基于属性的访问控制），在Experience Platform中维护安全访问。 凭据、SSL和数据加密也用于确保跨平台的数据保护。

关于查询服务的安全性，主要分为以下几类：

* [访问控制](#access-control)：访问通过角色和权限（包括数据集和列级别的权限）进行控制。
* 通过以下方式保护数据 [连通性](#connectivity)：通过与过期凭据或非过期凭据建立有限连接，通过Platform和外部客户端保护数据。
* 通过以下方式保护数据 [加密和系统级别密钥](#encryption)：通过加密在数据空闲时确保数据安全性。

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### 访问控制 {#access-control}

Adobe Experience Platform中的访问控制允许您使用 [Adobe Admin Console](https://adminconsole.adobe.com/) 使用基于角色的权限管理对查询服务功能的访问。 同样，您可以通过对架构和数据字段的标签管理来控制对特定数据属性的访问。

本节概述了用户为充分利用查询服务功能而必须拥有的访问控制权限。 查看文档 [管理权限](../../access-control/ui/permissions.md) 和 [管理用户](../../access-control/ui/users.md) 以获取有关为产品配置文件分配访问权限的详细说明。

#### 相关权限

下表根据相关访问控制权限的作用域级别定义了相关访问控制权限。

**查询执行权限**

要在Query Service中运行查询，必须为用户分配具有以下权限的角色：

| 权限 | 描述 |
|---|---|
| [!UICONTROL 管理查询] | 此权限允许用户执行数据探索和批量查询，这可以读取现有数据集或将数据写入数据集。 这包括两者 `CREATE TABLE AS SELECT` (`CTAS`)和 `INSERT INTO AS SELECT` (`ITAS`)个查询。 |

**数据集权限**

此部分用作在通过查询服务查询数据时访问数据集所需的基于资源的访问的指南。

通过“权限”界面，您可以为数据集和架构定义基于资源的访问控制，并具有以下权限：

| 权限 | 描述 |
|---|---|
| [!UICONTROL 管理数据集] | 此权限提供对架构的只读访问权限，并允许读取、创建、编辑和删除用于查询服务的数据集。 |
| [!UICONTROL 查看数据集] | 此权限允许对用于查询服务的数据集和架构进行只读访问。 |

#### 列/字段的访问控制

基于属性的访问控制功能使Query Service用户能够限制对关键用户数据的访问。 可以根据分配给角色的权限来授予或限制访问权限。 用户对单个列的访问受相关数据使用标签和应用于分配给用户的角色的权限集控制。

使用数据使用标签标记架构字段组和类会将数据使用限制应用于具有相同字段组和类的所有架构。 请参阅概述，位于 [基于属性的访问控制](../../access-control/abac/overview.md) 以了解有关此功能的全面信息。

此功能允许您向所选的用户组授予对机密列的访问权限。 列的访问控制可以限制特定类型用户的读取和写入功能。

列的访问控制可以在架构级别应用于标准架构和临时架构。 将数据使用标签应用于XDM架构，以限制对一个或多个列的访问。 数据标签始终得到应用，即使对于通过查询服务创建的数据集，使用预定义模式或作为CTAS操作的一部分生成的临时模式。

使用标签和角色应用了适当的访问级别后，当用户尝试访问不可访问的数据时，会发生以下系统行为：

1. 如果用户被拒绝访问架构中的某一列，则该用户也被拒绝对受限列的读取或写入权限。 这适用于以下常见方案：

   * **用例1**：当用户尝试执行仅影响受限列的查询时，系统会引发该列不存在的错误。
   * **用例2**：当用户尝试执行具有多个列（包括受限列）的查询时，系统仅返回所有非受限列的输出。

1. 如果用户尝试访问计算字段，则要求用户有权访问构成中使用的所有字段，或者系统拒绝访问计算字段。

#### 视图的访问控制

查询服务提供了将标准ANSI SQL用于 [`CREATE VIEW`](../sql/syntax.md#create-view) 语句。 对于高度敏感的数据工作流，您必须在创建视图时实施适当的控件。

此 `CREATE VIEW` 关键字定义查询的视图，但该视图并未实际实现。 相反，每次在查询中引用视图时都会运行查询。 当用户从数据集创建视图时，父数据集的基于角色和属性的访问控制规则是 **非** 分层应用。 因此，在创建视图时，必须明确设置每个列的权限。

#### 对加速数据集创建基于字段的访问限制 {#create-field-based-access-restrictions-on-accelerated-datasets}

使用 [基于属性的访问控制功能](../../access-control/abac/overview.md) 您可以在中定义事实和维度数据集的组织或数据使用范围 [加速存储](../data-distiller/query-accelerated-store/send-accelerated-queries.md). 这允许管理员管理对特定区段的访问权限，并更好地管理授予用户或用户组的访问权限。

要对加速数据集创建基于字段的访问限制，您可以使用查询服务CTAS查询创建加速数据集，并基于现有XDM架构或临时架构构建这些数据集。 然后，管理员可以 [添加和编辑架构的数据使用标签](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) 或 [临时架构](./ad-hoc-schema-labels.md#edit-governance-labels). 您可以从应用、创建和编辑架构的标签 [!UICONTROL 标签] 中的工作区 [!UICONTROL 架构] UI。

数据使用标签还可以是 [直接应用于或编辑数据集](../../data-governance/labels/user-guide.md#add-labels) 通过数据集UI，或从访问控制创建 [!UICONTROL 标签] 工作区。 请参阅指南，了解如何 [创建新标签](../../access-control/abac/ui/labels.md) 了解更多信息。

随后，用户可以控制对单个列的访问，这些访问由附加的数据使用标签以及应用于分配给用户的角色的权限集控制。

### 连接性 {#connectivity}

可通过Platform UI或与外部兼容的客户端建立连接来访问查询服务。 对所有可用前端的访问由一组凭据控制。

#### 通过外部客户端连接

使用第三方客户端访问查询服务需要凭据进行授权。 必须提供这些凭据，才能使用任何兼容的外部客户端访问查询服务。 您可以使用以下任一方式连接到外部客户端 [过期凭据](#expiring-credentials) 或 [未过期的凭据](#non-expiring-credentials).

#### 通过过期凭据的连接时间有限 {#expiring-credentials}

[过期凭据](../ui/credentials.md) 允许用户与外部客户端建立临时连接。 这组凭据仅在24小时内有效。 这些类型的凭据的到期情况与凭据选项卡一起显示在查询服务仪表板中。

![突出显示了过期凭据的查询服务工作区中的凭据选项卡。](../images/data-governance/overview/expiring-credentials.png)

#### 未过期的凭据 {#non-expiring-credentials}

[未过期的凭据](../ui/credentials.md#non-expiring-credentials) 允许您与外部客户端建立永久连接，从而更轻松地连接到查询服务，而无需手动密码。

要启用生成不会过期的凭据的选项，必须遵循概述的 [必备的工作流](../ui/credentials.md#prerequisites). 在此过程中，您的组织管理员需要配置产品配置文件的权限，以便管理员能够控制哪些帐户有权使用不会过期的凭据。

可以为允许使用不会过期凭据的技术用户帐户分配角色，以确保通过根据其责任和需求定义其读写访问权限范围来适当管理数据。 请参阅前面关于 [通过访问控制使用基于角色的权限](#access-control) 以管理对查询服务的访问。

完成先决条件工作流后，授权用户现在可以 [生成所需的连接凭据](../ui/credentials.md#generate-credentials).

#### SSL数据加密

为了提高安全性，查询服务为SSL连接提供本机支持，以加密客户端/服务器通信。 Platform支持各种SSL选项，以满足您的数据安全需求并平衡加密和密钥交换的处理开销。

请参阅指南，了解可用功能 [第三方客户端连接到查询服务的SSL选项](../clients/ssl-modes.md) ，以了解更多信息，包括如何使用 `verify-full` ssl参数值。

### 加密 {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

加密是使用算法过程将数据转换为编码和不可读的文本，以确保在没有解密密钥的情况下信息受到保护且不可访问。

查询服务数据合规性确保数据始终加密。 传输中的数据始终符合HTTPS标准，静态数据在Azure Data Lake存储中使用系统级别的密钥进行加密。 请参阅相关文档 [如何在Adobe Experience Platform中加密数据](../../landing/governance-privacy-security/encryption.md) 了解更多信息。 有关如何在Azure Data Lake Storage中加密静态数据的详细信息，请参阅 [Azure官方文档](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## 审核 {#audit}

查询服务记录用户活动，并将该活动分类为不同的日志类型。 日志提供信息 **谁** 已执行 **什么** 操作，以及 **时间**. 日志中记录的每个操作都包含元数据，这些元数据可指示操作类型、日期和时间、执行操作的用户的电子邮件 ID 以及与操作类型相关的其他属性。

Platform用户可以根据需要请求任何日志类别。 此部分提供有关为查询服务捕获的信息类型以及可在何处访问此信息的详细信息。

### 查询日志 {#query-logs}

查询日志UI允许您监视和查看已通过查询编辑器或查询服务API运行的所有查询的执行详细信息。 这为查询服务活动带来了透明度，允许您检查元数据 **所有** 已跨查询服务执行的查询。 它包括所有类型的查询，无论是探索查询、批量查询还是计划查询。

查询日志可通过以下位置中的Platform UI访问： [!UICONTROL 日志] 的选项卡 [!UICONTROL 查询] 工作区。

![高亮显示详细信息面板的“查询日志”选项卡。](../images/data-governance/overview/queries-log.png)

### 审核日志 {#audit-logs}

审核日志包含比查询日志更详细的信息，并可让您根据属性（如用户、日期、查询类型等）筛选日志。 除了查询日志UI中提供的详细信息之外，审核日志还存储单个用户的详细信息及其会话数据或到第三方客户端的连接。

审核记录提供了用户操作的精确记录，可以帮助解决问题，并帮助您的企业有效地遵守公司数据管理政策和法规要求。 审核日志提供了所有Platform活动的记录。 使用审核日志，您可以审核与查询执行、模板和已计划查询相关的用户操作，以提高用户在查询服务中执行的操作的透明度和可见性。

下表列出了由审核日志捕获的查询类别及其记录的操作类型：

| 类别 | 操作类型 |
|---|---|
| 查询 | Execute |
| 查询模板 | 创建、删除、更新 |
| 计划查询 | 创建、删除、更新 |

以下是三个扩展服务器日志的列表，这些日志的详细信息比查询日志中的详细信息更多。 在审核日志查询类别中找到扩展日志：

1. **元查询日志**：执行查询时，执行各种关联的后端子查询（例如解析）。 这些类型的查询称为“元数据”查询。 其相关详情见审核日志。
1. **会话日志**：系统会在用户登录查询服务时为其创建会话条目日志，而不管用户是否执行查询。
1. **第三方客户端连接日志**：当用户成功将查询服务连接到第三方客户端时，会生成连接审核日志。

请参阅 [审核日志概述](../../landing/governance-privacy-security/audit-logs/overview.md) 有关审核日志如何帮助您的组织实现数据合规性的更多信息。

## 数据使用 {#data-usage}

Platform中的数据治理框架提供了一种统一的方式，可用于在所有Adobe解决方案、服务和平台上负责任地使用数据。 它协调在整个的Adobe Experience Cloud中捕获、通信和使用元数据的系统方法。 这进而可帮助数据控制者根据所需的营销操作以及对来自这些预期营销操作的数据施加的限制来标记数据。 请参阅概述，位于 [数据使用标签](../../data-governance/labels/overview.md) 以了解数据管理如何让您将数据使用标签应用于数据集和字段的更多信息。

最佳实践是在数据历程的每个阶段努力实现数据合规性。 为此，使用临时架构的派生数据集应适当标记，作为数据治理框架的一部分。 查询服务形成的派生数据集有两种类型：使用标准架构的数据集和使用临时架构的数据集。

>[!NOTE]
>
>使用查询服务创建的数据集称为“派生数据集”。

由于临时架构由个人用户出于特定目的创建，因此XDM架构字段为该特定数据集进行命名空间，不适合跨不同数据集使用。 因此，临时架构在Experience PlatformUI中默认不可见。 尽管标准架构和临时架构在数据使用标签的应用方面没有区别，但查询服务为设置标签而创建的临时架构必须首先在Platform UI中可见。 请参阅指南，网址为 [在Platform UI中发现临时架构](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) 了解更多详细信息。

在访问架构后，您可以 [将标签应用于单个字段](../../xdm/tutorials/labels.md). 标记某个架构后，从该架构派生的所有数据集都将继承这些标签。 从此处，您可以设置数据使用策略，以限制将带有特定标签的数据激活到特定目标。 有关更多信息，请参阅以下文章的概述： [数据使用策略](../../data-governance/policies/overview.md).

## 隐私 {#privacy}

[Privacy Service](../../privacy-service/home.md) 帮助您根据隐私法规管理客户访问和删除其数据的请求。 它通过搜索数据以查找预先存在的标识符来完成此操作，并根据请求的隐私作业访问或删除该数据。 必须正确标记数据，服务才能确定在隐私作业期间要访问或删除哪些字段。 受隐私请求约束的数据必须包含客户身份信息，这样才能将不同的数据段与隐私请求所针对的个人联系起来。 查询服务可以使用唯一标识符扩充它使用的数据，以满足隐私作业的要求。

隐私请求可以发送到数据湖或配置文件数据存储。 从数据湖中删除的记录不会导致从这些记录中删除用户档案。 此外，从Data Lake中删除个人信息的隐私作业不会删除其个人资料，因此隐私作业完成后摄取的任何信息（包含该个人资料ID）都会正常更新该个人资料。 这再次表明需要正确识别临时架构中使用的数据。

有关以下内容的更多信息，请参阅Privacy Service文档 [隐私请求的身份数据](../../privacy-service/identity-data.md) 以及如何配置数据操作并利用Adobe技术有效地检索适当的身份信息以用于客户隐私请求。

数据治理的查询服务功能简化并简化了数据分类过程并遵守了数据使用法规。 标识数据后，可使用查询服务在所有输出数据集上分配主标识。 您 **必须** 将身份添加到数据集，以方便数据隐私请求并努力实现数据合规性。

可通过Platform UI将架构数据字段设置为标识字段，并且查询服务还允许您 [使用SQL命令&#39;ALTER TABLE&#39;标记主身份](../sql/syntax.md#alter-table). 使用设置标识 `ALTER TABLE` 当使用SQL而不是通过Platform UI直接从架构创建数据集时，命令特别有用。 有关如何执行操作的说明，请参阅文档 [在UI中定义标识字段](../../xdm/ui/fields/identity.md) 使用标准架构时。

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
