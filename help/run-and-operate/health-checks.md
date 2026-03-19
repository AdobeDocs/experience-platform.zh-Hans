---
title: 运行状况检查
description: 了解如何使用Adobe Experience Platform中的运行状况检查，在架构和身份配置问题影响您的数据操作之前主动检测这些问题。
solution: Experience Platform
type: Documentation
role: Admin, User
hide: true
source-git-commit: ab2420b898dc38d19187cee627b5c44e7fb44a6c
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 1%

---

# 运行状况检查

运行状况检查会扫描您在沙盒中使用的架构和标识，并提供可用于探索和解决[!UICONTROL AI Assistant]问题的摘要。 将来，可以扫描更多对象以获取更全面的报告。

较差的架构和身份配置会导致严重的下游问题，包括不正确的配置文件创建、区段鉴别失败以及不准确的激活。 这些问题难以检测，通常需要专业知识才能诊断。 运行状况检查将您的方法从被动故障诊断转变为主动预防性维护。

通过运行状况检查，您可以：

* **及早检测配置问题**：识别导致个性化、激活等效率低下的缺失的最佳实践、错误配置和模式。
* **接收引导式修正**：获取有关每个问题的含义以及应如何处理的明确指导。
* **持续监视**：此时，运行状况检查将运行每日自动扫描，以便在问题变成严重故障之前捕获问题。 未来版本中的时间表可能会发生变化。

## 先决条件 {#prerequisites}

要访问运行状况检查，您需要&#x200B;**[!UICONTROL View Health Checks]** [访问控制权限](/help/access-control/home.md#permissions)。 请与系统管理员联系以确保您拥有适当的权限。

## 访问运行状况检查 {#access-health-checks}

要从[!UICONTROL Experience Platform] UI访问运行状况检查，请执行以下操作：

1. 从左侧导航中选择&#x200B;**[!UICONTROL Run and Operate]**。
1. 选择 **[!UICONTROL Health Checks]**。

运行状况检查仪表板显示最近扫描结果的摘要。

![运行状况检查仪表板，显示已评估的对象、扫描结果和已识别的问题](assets/health-checks/dashboard.png)

## 了解仪表板 {#understanding-dashboard}

运行状况检查仪表板提供三个方面的信息以帮助您评估实施状态。

### 对象已评估 {#objects-evaluated}

**[!UICONTROL Objects evaluated]**&#x200B;部分显示已扫描的架构和身份命名空间的总数，以及每个类别中找到的问题数。 这让您快速了解沙盒中配置问题的范围和严重性。

### 扫描结果 {#scan-results}

**[!UICONTROL Scan results]**&#x200B;部分显示失败的检查数。 检查失败表示一个或多个运行状况检查检测到需要注意的配置问题。 在&#x200B;**时间戳上完成的**&#x200B;上次每日运行状况扫描显示最近一次扫描的运行时间。

### 已发现的问题 {#identified-issues}

**[!UICONTROL Identified issues]**&#x200B;部分显示每个运行状况检查的卡。 每个信息卡都会显示：

* 运行状况检查名称和问题的简要说明。
* 找到的问题数或不存在问题的确认。
* 显示检查通过还是需要注意的状态指示器。

选择任意卡片以浏览该运行状况检查的详细信息。

## 可用的运行状况检查 {#available-health-checks}

运行状况检查当前评估架构和身份配置的五个基本区域。 这些检查针对整个平台中最具影响力的数据建模问题。

### 标识字段验证 {#identity-field-validation}

扫描以确保标识字段具有最小和最大长度约束以及数据完整性的正则表达式模式规则。

| 详细信息 | 描述 |
| --- | --- |
| **问题** | 标记为标识的字段缺少最小/最大长度或模式验证。 |
| **影响** | 如果不进行验证，垃圾桶值可以输入[!UICONTROL Identity Service]。 诸如“0”、“Guest”之类的值或大小写不匹配（例如，“xyz123”与“XYZ123”）的值会损害在分段和激活期间组装的概要文件的完整性。 |
| **修正** | 对标记为标识的自定义字段设置最小/最大长度和模式约束。 使用正则表达式可强制实施仅数字、大写或小写或特定字符组合等规则。 |

选择&#x200B;**[!UICONTROL Identity Field Validation]**&#x200B;卡后，右侧将打开一个详细信息面板。 该面板显示：

* **[!UICONTROL Description]**：扫描以确保标识字段具有最小/最大长度以及用于数据完整性的正则表达式模式规则。 列出受影响的架构和字段。
* **[!UICONTROL Impact]**：如果架构中的标识字段没有设置最小/最大长度和模式验证，则可能会导致数据不一致，从而影响数据的完整性和质量。
* **[!UICONTROL General areas of impact]**： [!UICONTROL Identity Service]中的低质量标识符；拼接不可靠。
* **[!UICONTROL Experience League Documentation]**：指向数据建模最佳实践的链接。
* **[!UICONTROL Affected Schemas]**：受影响架构的列表，每个架构均带有扩展器以查看更多详细信息，并带有打开该架构的链接。

![身份字段验证详细信息面板，显示描述、影响和受影响的架构](assets/health-checks/identity-field-validation-detail.png)

有关详细信息，请参阅架构最佳实践文档中的[数据完整性提示](/help/xdm/schema/best-practices.md#data-integrity-tips)。

### 身份标识图链接规则 {#identity-graph-linking-rules}

验证是否为沙盒配置了身份图链接规则以防止折叠的用户档案。

| 详细信息 | 描述 |
| --- | --- |
| **问题** | 没有为此沙盒配置身份图形链接规则。 |
| **影响** | 如果不链接规则，则多个不同的配置文件可以合并为单个配置文件（图形折叠）。 来自共享设备的某些数据或非唯一身份可能会触发不需要的合并，从而导致个性化不准确。 |
| **修正** | 导航到&#x200B;**[!UICONTROL Identities]**&#x200B;菜单，选择&#x200B;**[!UICONTROL Settings]**，然后选择每个图形的至少一个唯一标识。 这将启用身份图链接规则并防止配置文件折叠。 |

选择&#x200B;**[!UICONTROL Identity Graph Linking Rules]**&#x200B;卡后，右侧将打开一个详细信息面板。 该面板显示：

* **[!UICONTROL Description]**：验证是否配置了正确的链接规则以防止折叠的配置文件。 它显示当前规则状态和每个图的唯一身份。
* **[!UICONTROL Impact]**：如果未设置身份图形链接规则，则某些数据可能会尝试将多个不同的配置文件合并到单个配置文件中。 要防止不必要的合并，应使用通过标识图链接规则提供的配置。
* **[!UICONTROL General areas of impact]**：折叠或合并的配置文件。
* **[!UICONTROL Experience League Documentation]**：链接到身份图形链接规则概述，以了解更多信息。
* **[!UICONTROL Configure linking rules]**：检查失败时，将显示一个按钮，以便您可以直接从面板配置链接规则。

![身份图形链接规则详细信息面板，显示说明、影响和配置链接规则按钮](assets/health-checks/identity-graph-linking-detail.png)

有关详细信息，请参阅[身份图链接规则概述](/help/identity-service/identity-graph-linking-rules/overview.md)和[实施指南](/help/identity-service/identity-graph-linking-rules/implementation-guide.md)。

### 人员和非人员身份配置 {#people-non-people-identity}

验证架构类中人员和非人员身份类型的正确使用。

| 详细信息 | 描述 |
| --- | --- |
| **问题** | 非人员标识符用于个人配置文件或体验事件类架构，或者人员标识符用于查找架构。 |
| **影响** | 配置文件架构上的非人员标识符不参与身份图，这会导致身份解析不完整。 查找架构上的人员标识符会使配置文件计数虚增，并使数据不符合查找用例的资格。 这两种情形都可能导致未来产品增强功能中断您的实施。 |
| **修正** | 查看标记的架构并更正身份类型分配。 尽可能从个人配置文件架构中删除非人员标识符。 对于数据集已使用的架构，请参阅[架构演化规则](/help/xdm/schema/composition.md#evolution)。 |

选择&#x200B;**[!UICONTROL People & Non-People Identity Config]**&#x200B;卡后，右侧将打开一个详细信息面板。 该面板显示：

* **[!UICONTROL Description]**：验证跨架构类正确使用了标识类型。 列出配置错误的架构并突出显示错误的分配。
* **[!UICONTROL Impact]**：如果为非人员实体指定了人员身份，这将夸大配置文件计数，并使此数据不符合查找条件。 如果为人员实体指定非人员身份，则数据不可用于流或边缘分段。
* **[!UICONTROL General areas of impact]**：标识图不完整；配置文件计数夸大；查找误用。
* **[!UICONTROL Affected Schemas]**：存在问题的架构列表。 展开架构行可查看每个错误配置的路径、身份名称和架构类型。 使用链接图标打开架构。

![人员和非人员身份配置详细信息面板，显示描述、影响以及包含可扩展行的受影响架构](assets/health-checks/people-non-people-identity-detail.png)

有关详细信息，请参阅[身份类型文档](/help/identity-service/features/namespaces.md#identity-type)和[架构最佳实践](/help/xdm/schema/best-practices.md)。

### 自定义身份命名空间描述 {#namespace-missing-description}

扫描以确保自定义身份命名空间元数据和描述完整。

| 详细信息 | 描述 |
| --- | --- |
| **问题** | 自定义身份命名空间缺少其描述字段。 |
| **影响** | 缺少描述可能会导致使用和调试期间出现混淆。 |
| **修正** | 通过填写描述字段来记录每个自定义命名空间。 包括验证条件（最小/最大长度、模式）和标识由哪个外部源系统创建这些标识的生命周期信息。 |

选择&#x200B;**[!UICONTROL Custom Identity Namespace Description]**&#x200B;卡后，右侧将打开一个详细信息面板。 该面板显示：

* **[!UICONTROL Description]**：扫描以确保命名空间元数据和描述完整。 显示说明字段为空的命名空间和所有者。
* **[!UICONTROL Impact]**：对自定义身份命名空间设置描述可提供每个命名空间用途的上下文，从而增强清晰度。 这有助于团队成员和利益相关者快速了解每个命名空间的功能，而不会产生混淆。
* **[!UICONTROL General areas of impact]**：调试或使用混淆；验证意图不明确。
* **[!UICONTROL Experience League Documentation]**：用于创建自定义命名空间的链接以获取更多信息。
* **[!UICONTROL Affected namespaces]**：缺少描述的自定义身份命名空间列表。 使用每个命名空间旁边的链接图标可查看或编辑命名空间。

![自定义身份命名空间描述详细信息面板，显示描述、影响和受影响的命名空间列表](assets/health-checks/custom-namespace-description-detail.png)

有关详细信息，请参阅有关[创建自定义命名空间](/help/identity-service/features/namespaces.md#create-namespaces)的文档。

### 已弃用的身份命名空间 {#deprecated-namespace}

检测应标记为清理的过时或未使用的标识命名空间。

| 详细信息 | 描述 |
| --- | --- |
| **问题** | 过时的标识命名空间不会标记为已弃用。 |
| **影响** | 未使用或过时的命名空间会造成对正在使用的内容的混淆，并增加标识字段标签错误的风险。 |
| **修正** | 重命名未使用的命名空间以包含“不使用”前缀（例如，“不使用 — [原始名称]”）。 Adobe Experience Platform当前不支持命名空间删除，因此建议重命名命名空间。 |

选择&#x200B;**[!UICONTROL Deprecated Identity Namespace]**&#x200B;卡后，右侧将打开一个详细信息面板。 该面板显示：

* **[!UICONTROL Description]**：检测已过时或未使用的标识命名空间以进行清理。 列出具有上次使用时间戳或架构引用的未使用命名空间。
* **[!UICONTROL Impact]**：未在任何架构中使用的身份命名空间应该标记为要删除，方法是在其名称中添加“DEPRECATED”或“DO NOT USE”标记。 当前不支持删除身份命名空间。
* **[!UICONTROL General areas of impact]**：混淆和标签错误的风险。
* **[!UICONTROL Experience League Documentation]**：指向过时的身份命名空间的链接，以供进一步参考。
* **[!UICONTROL Affected namespaces]**：已过时或未使用的身份命名空间列表。 使用每个命名空间旁边的链接图标可查看或管理命名空间。

![已弃用的身份命名空间详细信息面板，显示说明、影响以及受影响的命名空间列表](assets/health-checks/deprecated-namespace-detail.png)

有关详细信息，请参阅关于过时命名空间的[Experience Cloud知识库文章](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-18155){target="_blank"}。

## 后续步骤 {#next-steps}

查看您的运行状况检查结果后，探索以下资源以加深您的了解：

* 了解用于设计可靠数据模型的[架构最佳实践](/help/xdm/schema/best-practices.md)。
* 了解[标识图链接规则](/help/identity-service/identity-graph-linking-rules/overview.md)以防止配置文件折叠。
* 查看[身份命名空间文档](/help/identity-service/features/namespaces.md)以了解命名空间管理最佳实践。
* 探索其他[运行和操作工具](/help/run-and-operate/overview.md)（包括[[!UICONTROL Job Schedules]](/help/run-and-operate/job-schedules.md)）以查看批处理操作。
