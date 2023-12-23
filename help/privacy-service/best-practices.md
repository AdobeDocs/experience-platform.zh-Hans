---
title: Privacy Service的最佳实践
description: 了解如何按照这些最佳使用指南完成隐私请求时，减少组织所需的处理时间和成本。
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Privacy Service的最佳实践

当客户希望从您的数据存储访问或删除其个人数据时，可使用Privacy Service自动遵守数据隐私法规。 为了满足这些不断变化的业务需求，Privacy Service提供了一个RESTful API和UI，用于跨Adobe Experience Cloud应用程序提交客户数据的访问和删除请求。

本指南概述了在管理客户数据请求时有效处理隐私请求和优化完成响应时间的最佳实践。

## 快速入门 {#getting-started}

本指南要求您实际了解 [Privacy Service](./home.md) 以及它如何允许您跨Adobe Experience Cloud应用程序管理来自数据主体（客户）的访问和删除请求。 此外，建议您阅读以下指南： [在UI中创建隐私作业请求](./ui/user-guide.md#create-a-new-privacy-job-request) 或 [API](./api/overview.md)，并了解如何以编程方式执行这些操作。

## 先决条件 {#prerequisites}

在Adobe Admin Console中，可通过基于角色的细粒度权限来控制对Adobe Experience Platform Privacy Service的访问。 您需要产品配置文件中的相关权限才能使用Privacy ServiceUI和API中的特定功能。 如果您需要其他权限，请联系您的系统管理员。

管理员可以参阅以下方面的指南： [管理Privacy Service的权限](./permissions.md) 以了解更多信息。

## 隐私作业创建准则 {#creation-guidelines}

要简化请求处理并缩短响应时间，请在创建隐私作业时考虑以下准则。 这同时适用于API和UI方法。

1. **最大程度地提高每个请求的数据主体数量：** 包括尽可能多数据主体，每个请求最多1000个。
2. **组ID以提高效率：** 在每个请求中为单个数据主体（最多九个）对多个ID进行分组。 此 **ID可以来自同一请求中的不同Adobe服务**.
3. **将访问和删除作业结合使用：** 如果数据主体需要，在单个请求中包括“访问”和“删除”作业类型。
4. **仅包括必要的产品：** 仅包括必需或许可的产品。 额外的产品可能会延长处理时间并增加成本。

## 监测隐私作业状态 {#monitor-status}

为了有效监控隐私作业并检查其状态，Privacy Service提供了三种方法。 为了监控效率和生产率，下面列出了可用的方法。 每种方法都包含用于改善您体验的最佳实践指南，随后是结合所有方法的理想方案示例。

### 接收实时通知 {#real-time-notifications}

**I/O事件** 通过状态事件提供近乎实时的状态监控。 这是最有效的方法，因为它无需实施轮询机制并产生额外的API流量。

**Recommendations：**

- **Webhook设置：** 设置Webhook以便在已提交作业的状态发生更改时接收推送通知。 这有助于实时监控。
- **通知：** 在作业和产品级别使用通知来帮助监控请求进度。

请参阅相关文档 [订阅Privacy Service事件](./privacy-events.md) 有关为Privacy Service通知设置事件注册以及如何解释通知有效负荷的说明。

### 基于过滤器检索所有作业 {#retrieve-filtered-responses-for-all-jobs}

要根据任何指定的筛选器检索所有隐私作业数据，请执行以下操作： **向执行GET请求 `/jobs` 端点**. 此API调用有助于提供仅具有单个请求的大型作业ID集当前作业状态的高级视图。 它确实缺少详细的产品响应，但可以使用 [`/jobs/{jobID}` 端点](#retrieve-detailed-responses-for-specific-jobs).

GET请求 `/jobs` 终结点最适合用于收集或比较大量作业ID的状态数据，但是 **非** 用于定期轮询类型活动。

**Recommendations：**

- **查询参数：** 使用特定过滤器来缩小结果范围，例如：数据范围、法规类型和状态（处理、完成等）。

您可以通过Privacy ServiceUI查看组织中所有当前隐私作业的列表。 请参阅 [管理UI中的隐私作业](./ui/user-guide.md#job-requests) 有关如何筛选作业请求列表的信息。 或者，参阅关于 [在Privacy ServiceAPI中使用/job端点](./api/privacy-jobs.md).

Privacy ServiceAPI文档包含以下内容的详细信息 [可用的查询参数过滤器](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### 检索单个作业的详细响应 {#retrieve-detailed-responses-for-specific-jobs}

要检索单个作业的详细响应， **向/jobs/执行GET请求{jobID} 端点**. 此方法适用于更深入的信息收集，例如产品特定的响应和成功消息。 对此端点的调用是查看哪些产品已响应以及哪些产品仍在等待处理的最佳方法，尽管它是 **非** 用于定期轮询活动。

请参阅 `/jobs/{JOB_ID}` 有关详细信息的端点文档 [如何检查特定作业的状态](./api/privacy-jobs.md#check-status).

### 理想方案示例 {#ideal-scenario}

使用webhook ，以便系统能够在请求中的ID组完成时自动更新记录并提供报告或警报。 如果作业仍未完成，系统会通过GET请求向Privacy ServiceAPI检索这些作业状态 `/jobs` 端点，并提供列表的高级更新。

如果特定作业仍在等待处理或返回了错误，您可以通过GET请求来检索详细响应，并向 `/job/{jobId}` 端点。

## 访问请求数据 {#access-request-data}

当请求数据主体信息时，每个服务都以与其存储和使用数据方式一致的格式返回数据。 所有服务都完成请求后，作业详细信息中会提供一个.ZIP存档文件URL，以便下载此数据。 有关信息，请参阅疑难解答指南 [如何下载隐私作业结果](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

以下是有关数据存档管理的注释的关键项目：

- 所有存档文件将在30天后从Experience Platform服务器中删除。 您无法查询超过30天的客户数据。
- 该存档文件的结构包括请求中所包含的每个产品的文件夹以及其中包含的数据文件。 如果找不到指定ID的数据，则存档文件或文件夹可能为空。
- 以前创建的作业的数据只能在完成日期后的30天内访问。 之后，数据将从系统中删除，并且必须发出新请求。

**Recommendations：**

- **Protect数据存档：** URL和.ZIP文件都应受到保护，因为它们可能包含数据主体的个人身份信息(PII)。

## 技术注意事项 {#technical-considerations}

完成Privacy Service请求时，应注意一些技术注意事项：

- **数据保留期：** 任何作业组的最长回顾期间为60天，查询的最长时间范围为30天（起始/终止日期）。
- **网关超时：** 请注意，如果您的请求超过60秒，则可能会从网关中丢弃。
- **错误处理：** 彻底查看错误消息并在适当时重新提交请求。 发生错误后，Privacy Service不会自动重新处理作业。
- **了解HTTP 429错误：** 熟悉HTTP 429错误消息以及缓解问题的必要步骤。 HTTP 429错误是“请求过多”的结果。 请参阅 [常见错误消息](./troubleshooting-guide.md#common-error-messages) 部分，以获取有关如何解决问题的更多信息。

## 后续步骤

通过阅读本文档，您现在拥有了高效和有效地使用该Privacy Service所需的知识和实践。 接下来，查看 [疑难解答指南](./troubleshooting-guide.md) 有关Privacy Service的常见问题解答以及API中常见错误的信息。
