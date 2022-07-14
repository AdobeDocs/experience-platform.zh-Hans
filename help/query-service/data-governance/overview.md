---
title: 查询服务中的数据管理
description: 此概述涵盖Experience Platform查询服务中数据管理的主要元素。
feature: Data Governance
source-git-commit: ec063a0f5600729d3575f98898ade04443f29f2a
workflow-type: tm+mt
source-wordcount: '2667'
ht-degree: 0%

---

# 查询服务中的数据管理

Adobe Experience Platform将来自多个企业系统的数据整合在一起，允许您根据需要通过查询服务来清理、塑造、处理和扩充数据。 这可让营销人员更好地识别、了解和吸引客户。 确保适当的数据管理是处理个人信息的一个关键方面，因为某些数据可能会受到基于组织政策和法律法规的使用限制。 确保您摄取的数据及其相关操作符合定义的数据使用策略，这一点至关重要。

通过查询服务中的数据管理，您可以管理客户数据并确保符合适用于数据使用的法规、限制和策略。 在确保已根据企业定义的法规应用使用策略时，此功能将发挥关键作用。

建议定期执行数据处理的组织概述、实践和实施这些准则，以便为所有用户创建注重隐私的环境。

以下类别在使用查询服务时有助于遵守数据合规法规：

1. 安全性
1. 审核
1. 数据使用情况
1. 隐私
<!-- 1. Data hygiene -->

本文档介绍了管理的每个不同方面，并演示了在使用查询服务时如何促进数据合规性。 请参阅 [管理、隐私和安全概述](../../landing/governance-privacy-security/overview.md) 有关“Experience Platform”如何让您管理客户数据和确保法规遵从性的更广泛信息。

## 安全性

数据安全是保护数据免遭未经授权访问并确保数据在其整个生命周期内安全访问的过程。 通过应用角色和权限，通过诸如基于角色的访问控制和基于属性的访问控制等功能，在Experience Platform中维护安全访问。 凭据、SSL和数据加密还用于确保跨平台的数据保护。

查询服务的安全性分为以下几类：

* [访问控制](#access-control):访问权限通过角色和权限（包括数据集和列级别权限）进行控制。
* 通过保护数据 [连接](#connectivity):通过使用过期的凭据或未过期的凭据建立有限连接，可通过平台和外部客户端保护数据。
* 通过保护数据 [加密和系统级密钥](#encryption):数据处于静态时，通过加密来确保数据安全。

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### 访问控制 {#access-control}

Adobe Experience Platform中的访问控制允许您使用 [Adobe Admin Console](https://adminconsole.adobe.com/) 使用基于角色的权限管理对查询服务功能的访问权限。 同样，您也可以通过架构和数据字段上的标签管理来控制对特定数据属性的访问权限。

本节概述了用户为充分利用查询服务功能必须具有的所需访问控制权限。 请参阅 [管理权限](../../access-control/ui/permissions.md) 和 [管理用户](../../access-control/ui/users.md) 有关为产品配置文件分配访问权限的详细说明。

#### 相关权限

相关的访问控制权限根据权限级别在下表中定义。

**查询执行权限**

要在查询服务中运行查询，必须为用户分配具有以下权限的角色：

| 权限 | 描述 |
|---|---|
| [!UICONTROL 管理查询] | 此权限允许用户执行数据探索和批量查询，这些查询可以读取现有数据集或在数据集上写入数据。 这包括两者 `CREATE TABLE AS SELECT` (`CTAS`)和 `INSERT INTO AS SELECT` (`ITAS`)查询。 |

**数据集权限**

本节将作为指南，介绍在通过查询服务查询数据时访问数据集所需的基于资源的访问。

通过权限界面，您可以为具有以下权限的数据集和架构定义基于资源的访问控制：

| 权限 | 描述 |
|---|---|
| [!UICONTROL 管理数据集] | 此权限为架构提供只读访问权限，并允许读取、创建、编辑和删除数据集以与查询服务一起使用。 |
| [!UICONTROL 查看数据集] | 此权限允许对数据集和架构进行只读访问，以与查询服务一起使用。 |

#### 列/字段的访问控制

基于属性的访问控制功能使查询服务用户能够限制对关键用户数据的访问。 可根据分配给角色的权限授予或限制访问权限。 用户对单个列的访问权限由相关数据使用标签和应用于分配给用户的角色的权限集来控制。

标记架构字段组和具有数据使用标签的类将数据使用限制应用于具有相同字段组和类的所有架构。 请参阅 [基于属性的访问控制](../../access-control/abac/overview.md) 以了解有关此功能的全面信息。

此功能允许您向所选用户组授予对机密列的访问权限。 对列的访问控制可以限制特定类型用户的读和写功能。

列的访问控制可以在标准架构和临时架构的架构级别应用。 将数据使用标签应用于XDM架构，以限制对一个或多个列的访问。 数据标签功能始终如一地应用，甚至对于通过查询服务创建的数据集（使用预定义架构或作为CTAS操作一部分生成的临时架构）也是如此。

使用标签和角色应用适当的访问级别后，当用户尝试访问不可访问的数据时，会发生以下系统行为：

1. 如果用户被拒绝访问某个架构中的某一列，则该用户也被拒绝对受限列进行读或写的权限。 这适用于以下常见情况：

   * **用例1**:当用户尝试执行仅影响受限列的查询时，系统会引发该列不存在的错误。
   * **用例2**:当用户尝试执行包含多个列（包括受限列）的查询时，系统将仅返回所有非受限列的输出。

1. 如果用户尝试访问计算字段，则用户必须有权访问组合中使用的所有字段，否则系统也会拒绝访问计算字段。

#### 视图的访问控制

查询服务提供使用标准ANSI SQL的功能 [`CREATE VIEW`](../sql/syntax.md#create-view) 语句。 对于高度敏感的数据工作流，在创建视图时必须强制实施适当的控制。

的 `CREATE VIEW` 关键字定义查询的视图，但该视图未实际化。 而是在每次在查询中引用视图时运行查询。 当用户从数据集创建视图时，父数据集基于角色和属性的访问控制规则将为 **not** 分层应用。 因此，在创建视图时，您必须明确地设置每个列的权限。

### 连接 {#connectivity}

查询服务可通过平台UI访问，或通过与外部兼容客户端建立连接来访问。 所有可用前线的访问由一组凭据控制。

#### 通过外部客户端进行连接

使用第三方客户端访问查询服务时，需要凭据进行授权。 使用任何兼容的外部客户端访问查询服务时，必须提供这些凭据。 您可以使用以下任一方式连接到外部客户端 [过期凭据](#expiring-credentials) 或 [未过期的凭据](#non-expiring-credentials).

#### 通过过期凭据的连接时间有限 {#expiring-credentials}

[过期凭据](../ui/credentials.md) 允许用户与外部客户端形成临时连接。 此凭据集仅在24小时内有效。 查询服务仪表板中的凭据选项卡可同时查看这些类型凭据的到期情况。

![查询服务工作区中的“凭据”选项卡，其中突出显示了过期的凭据。](../images/data-governance/overview/expiring-credentials.png)

#### 未过期的凭据 {#non-expiring-credentials}

[未过期的凭据](../ui/credentials.md#non-expiring-credentials) 允许您与外部客户端形成永久连接，从而更轻松地连接到查询服务，而无需手动密码。

要启用生成未过期凭据的选项，您必须遵循 [先决条件工作流](../ui/credentials.md#prerequisites). 在此过程中，您的组织管理员需要配置产品配置文件的权限，从而让管理员控制哪些帐户有权使用未过期的凭据。

可以为具有未过期凭据的技术用户帐户分配角色，以通过根据用户的职责和需求定义其读写权限范围来确保适当的数据管理。 请参阅 [通过访问控制使用基于角色的权限](#access-control) 以管理对查询服务的访问权限。

先决性工作流完成后，授权用户现在可以 [生成所需的连接凭据](../ui/credentials.md#generate-credentials).

#### SSL数据加密

为了提高安全性，查询服务为加密客户端/服务器通信的SSL连接提供本机支持。 平台支持各种SSL选项，以满足您的数据安全需求，并平衡加密和密钥交换的处理开销。

请参阅上的指南 [用于与查询服务的第三方客户端连接的SSL选项](../clients/ssl-modes.md) 有关更多信息，包括如何使用 `verify-full` SSL参数值。

### 加密 {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

加密是使用算法过程将数据转换为编码且不可读的文本，以确保信息在没有解密密钥的情况下受到保护且无法访问。

查询服务数据合规性可确保数据始终加密。 传输中的数据始终符合HTTPS，并且静态数据在Azure数据湖存储中使用系统级别密钥进行加密。 请参阅 [数据在Adobe Experience Platform中的加密方式](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html) 以了解更多信息。 有关Azure数据湖存储中静态数据如何加密的详细信息，请参阅 [官方Azure文档](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## 审核 {#audit}

查询服务记录用户活动，并以不同的日志类型对该活动进行分类。 日志提供有关 **who** 执行 **什么** 操作和 **when**. 日志中记录的每个操作都包含元数据，这些元数据指示操作类型、日期和时间、执行操作的用户的电子邮件ID，以及与操作类型相关的其他属性。

平台用户可以根据需要请求任何日志类别。 本节提供有关为查询服务捕获的信息类型以及可访问此信息的位置的详细信息。

### 查询日志 {#query-logs}

查询日志UI允许您监控和查看已通过查询编辑器或查询服务API运行的所有查询的执行详细信息。 这为查询服务活动带来了透明度，允许您检查 **全部** 已在查询服务中执行的查询。 无论查询是探索性查询、批处理查询还是计划查询，它都包含所有类型的查询。

查询日志可通过 [!UICONTROL 日志] 选项卡 [!UICONTROL 查询] 工作区。

![“查询日志”选项卡突出显示了详细信息面板。](../images/data-governance/overview/queries-log.png)

### 审核日志 {#audit-logs}

审核日志包含比查询日志更详细的信息，并且允许您根据用户、日期、查询类型等属性筛选日志。 除了查询日志UI中提供的详细信息之外，审核日志还会存储有关单个用户的详细信息，以及其会话数据或与第三方客户端的连接情况。

通过提供用户操作的准确记录，审核跟踪可帮助解决问题，并帮助您的企业有效地遵守公司数据管理策略和法规要求。 审核日志提供所有平台活动的记录。 使用审核日志，您可以审核与查询执行、模板和计划查询相关的用户操作，以提高查询服务中用户所执行操作的透明度和可见性。

下表指示了审核日志捕获的查询类别及其记录的操作类型：

| 类别 | 操作类型 |
|---|---|
| 查询 | Execute |
| 查询模板 | 创建、删除、更新 |
| 计划查询 | 创建、删除、更新 |

下面是三个扩展服务器日志的列表，其中包含的详细信息比查询日志中提供的详细信息更多。 在审核日志查询类别中可找到扩展日志：

1. **元查询日志**:执行查询时，会执行各种关联的后端子查询（如解析）。 这些类型的查询称为“元数据”查询。 其相关详细信息可在审核日志中找到。
1. **会话日志**:无论用户是否执行查询，系统都会在登录查询服务时为用户创建一个会话条目日志。
1. **第三方客户端连接日志**:当用户成功将查询服务连接到第三方客户端时，将生成连接审核日志。

请参阅 [审核日志概述](../../landing/governance-privacy-security/audit-logs/overview.md) 有关审核日志如何帮助您的组织实现数据合规性的更多信息。

## 数据使用情况 {#data-usage}

平台中的数据管理框架提供了一种统一的方式，以负责任地使用所有Adobe解决方案、服务和平台中的数据。 它协调了在整个Adobe Experience Cloud中捕获、传输和使用元数据的系统方法。 这反过来又有助于数据控制者根据所需的营销操作以及这些预期营销操作对该数据施加的限制来标记数据。 请参阅 [数据使用标签](../../data-governance/labels/overview.md) 有关“数据管理”如何允许您将数据使用情况标签应用到数据集和字段的更多信息。

在数据历程的每个阶段都努力实现数据合规性是最佳做法。 为此，应在数据管理框架中正确标记使用临时架构的派生数据集。 查询服务可形成两种类型的派生数据集：使用标准架构的数据集和使用临时架构的数据集。

>[!NOTE]
>
>使用查询服务创建的数据集称为“派生的数据集”。

由于临时架构是由单个用户为特定目的创建的，因此XDM架构字段将为该特定数据集命名，而不是用于不同的数据集。 因此，默认情况下，临时架构不会显示在Experience PlatformUI中。 尽管标准架构和临时架构之间数据使用标签的应用没有区别，但是由查询服务为标签目的创建的临时架构必须首先在平台UI中可见。 请参阅 [在平台UI中了解临时架构](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) 以了解更多详细信息。

访问架构后，您可以 [将标签应用于单个字段](../../xdm/tutorials/labels.md). 标记架构后，从该架构派生的所有数据集都将继承这些标签。 从此处，您可以设置数据使用策略，以限制将具有特定标签的数据激活到特定目标。 有关更多信息，请参阅 [数据使用策略](../../data-governance/policies/overview.md).

## 隐私 {#privacy}

[Privacy Service](../../privacy-service/home.md) 帮助您管理客户请求以根据法律隐私法规访问和删除其数据。 它通过搜索数据以查找预先存在的标识符来执行此操作，并根据请求的隐私作业访问或删除该数据。 必须正确标记数据，以便服务确定在隐私作业期间要访问或删除的字段。 受隐私请求约束的数据必须包含客户身份信息，以便将不同的数据片段与隐私请求所适用的个人绑定。 查询服务可以使用唯一标识符扩充其使用的数据，以满足隐私作业的需要。

可以将隐私请求发送到数据湖或配置文件数据存储区。 从数据湖中删除的记录不会导致删除从这些记录中创建的用户档案。 此外，从数据湖中删除个人信息的隐私作业不会删除其配置文件，因此在隐私作业完成后摄取的任何信息（包含该配置文件ID）都会正常更新该配置文件。 这重申需要正确识别在特定模式中使用的数据。

有关 [隐私请求的身份数据](../../privacy-service/identity-data.md) 以及如何配置数据操作并利用Adobe技术来有效检索客户隐私请求的适当身份信息。

用于数据管理的查询服务功能简化并简化了数据分类流程，并遵守了数据使用法规。 在识别数据后，查询服务允许您为所有输出数据集分配主标识。 您 **必须** 将身份添加到数据集中，以便于提出数据隐私请求，并努力实现数据合规性。

架构数据字段可以通过Platform UI设置为标识字段，并且查询服务还允许您 [使用SQL命令“ALTER TABLE”标记主标识](../sql/syntax.md#alter-table). 使用 `ALTER TABLE` 命令在使用SQL创建数据集时特别有用，而不是直接通过Platform UI从架构创建数据集时。 有关如何 [在UI中定义标识字段](../../xdm/ui/fields/identity.md) 使用标准架构时。

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
