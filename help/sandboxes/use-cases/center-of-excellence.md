---
title: 使用沙盒工具启用卓越中心
description: 通过创建一个“黄金沙盒”包来标准化多个沙盒中的最佳实践，从而使用沙盒工具启用卓越中心。
exl-id: 6f242ad5-bb02-4a6d-b255-d196dd5fe4b8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 8%

---

# 使用沙盒工具启用卓越中心

通过创建一个“黄金沙盒”包来标准化多个沙盒中的最佳实践，从而使用沙盒工具启用卓越中心。

![跨不同组织导出包的概述](../images/use-cases/packages-across-orgs.png){zoomable="yes"}

## 为什么考虑此用例 {#why-this-use-case}

许多大型公司或企业为不同的组织、团队、区域或开发环境使用多个沙盒。 借助[沙盒工具](../ui/sandbox-tooling.md)的强大功能，您可以创建黄金沙盒包，以确保多个沙盒之间组织标准的一致性、合规性和一致性。

这个金色的沙盒包创建了一个卓越中心以高效共享关键配置。 使用沙盒工具，您可以轻松地跨多个沙盒导入包。 您还可以将您的包共享给其他组织，以确保广泛的一致性。

按照此用例中描述的步骤，创建自己的黄金沙盒包。

## 行业示例 {#industry-example}

例如，考虑一家跨不同地区（如北美、欧洲和非洲）运营的银行。 每个市场或地区都有自己的Adobe Experience Platform实例。 该银行希望维护一个集中化的数据模型，该模型由一个全球架构师团队管理，可在所有市场推出单一版本的数据模型。

该银行选择使用沙盒工具来创建和维护黄金沙盒包。 这有助于提高开发效率，允许一致的数据模型，并确保跨所有区域的一致性。

## 先决条件和规划 {#prerequisites-and-planning}

在计划在组织内创建自己的英才中心时，请在计划流程中考虑以下先决条件：

- 确定要包含在包中的最佳实践和配置。
- 创建一个沙盒，并将所有相关的已验证配置设置为Golden Sandbox。
- 如有需要，请让利益相关者对您的基线标准提出意见并达成一致。

### 用户界面功能、Experience Platform组件以及您将使用的Experience Cloud产品 {#ui-functionality-and-elements}

要成功实施此用例，您必须使用Adobe Experience Platform的多个区域。 确保您具有所有这些区域所需的[基于属性的访问控制权限](../../access-control/abac/overview.md)，或要求系统管理员授予您必要的权限。

- [沙盒工具](../ui/sandbox-tooling.md)
- [沙盒管理](../ui/user-guide.md)
- [数据集](../../catalog/datasets/overview.md)
- [架构](../../xdm//home.md)
- [受众](../../segmentation/home.md)
- 来自Adobe Journey Optimizer的[历程](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

## 如何实现该用例：高级概述 {#achieve-the-use-case-high-level}

1. 创建基线配置，以在Golden Sandbox中表示您的最佳实践。 这可能包括数据集、架构、受众或历程等对象。
2. 使用沙盒工具，将配置导出到包中。
3. 将此包导入所有相关沙盒中。
4. 如果您有多个组织，请在组织间共享此资源包。
5. 监控导入和导出，并通过审核日志跟踪更改。
6. 随着标准的发展定期更新您的黄金沙箱，确保所有沙箱与最佳实践保持一致。

## 如何实现用例：分步说明 {#step-by-step-instructions}

通读以下部分（其中包括指向更多文档的链接）以完成上方高级概述中的每个步骤。

### 创建您的金色沙盒

启用卓越中心的第一步是创建您的黄金沙盒。 此沙盒应包含代表您最佳实践的基线配置。 要创建此Golden沙盒，请按照[在Experience Platform中创建新沙盒](../ui/user-guide.md#create-a-new-sandbox)的指南操作。

创建沙盒后，开始创建基线对象配置，如[架构](../../xdm/ui/resources/schemas.md#create-a-new-schema)、[数据集](../../catalog/datasets/user-guide.md#create-a-dataset)或[受众](../../segmentation/ui/segment-builder.md)。 在继续之前，请务必查看您的配置。

### 将沙盒导出到资源包中

现在，您的沙盒包含基线对象配置，可以使用沙盒工具将其导出到包中。 按照有关[导出整个沙盒](../ui/sandbox-tooling.md#export-an-entire-sandbox)的指南创建您的黄金沙盒包。

### 将您的包导入相关的沙盒中

现在您的资源包已创建，您可以将此资源包导入相关的沙盒中。 最佳实践是将包含整个沙盒的包导入空沙盒中。 使用沙盒工具，您可以轻松[将整个沙盒包](../../sandboxes/ui/sandbox-tooling.md#import-the-entire-sandbox-package)直接导入Experience Platform中的沙盒中。

### 跨组织共享包

沙盒工具允许您在不同组织之间共享已创建的包。 按照[包共享指南](../../sandboxes/ui/sharing-packages-across-orgs.md)共享您的黄金沙盒包。

### 通过审核日志监控导入和导出

在导入或导出包时，您可以使用Experience Platform中的&#x200B;**[!UICONTROL 作业]**&#x200B;仪表板监控作业的状态。 要了解有关监视作业的更多信息，请阅读有关[监视导入详细信息](../../sandboxes/ui/sandbox-tooling.md#monitor-import-details)的指南。

### 定期更新金色沙盒

现在，您的金沙盒包已经完成，您已经建立了一个标准化的卓越中心，您可以继续导入沙盒或在组织间共享。 随着最佳实践的更改和开发，定期更新黄金沙盒中的基准对象配置很重要。 更新沙盒时，您可以按照此相同流程创建黄金沙盒包的新小版本。

>[!NOTE]
>
> 上述步骤遵循Experience Platform用户界面中的流程。 可以通过各种端点使用API遵循相同的步骤。 有关通过API发出每个请求的信息，请参阅`sandboxes` [端点指南](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/api/sandboxes#create)和`packages` [端点指南](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages)。

## 由合作伙伴数据支持实现的其他用例 {#other-use-cases}

探索通过沙盒工具启用的更多用例：

- [使用沙盒工具备份对象配置](./backup-object-configuration.md)
