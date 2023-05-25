---
title: 测试并提交源
description: 以下文档提供了有关如何使用Flow Service API测试和验证新源，以及如何通过Self-Serve Sources (Streaming SDK)集成新源的步骤。
hide: true
hidefromtoc: true
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---

# 测试并提交源

使用自助式源（流SDK）将新源集成到Adobe Experience Platform的最后一步是测试和提交新源。 完成连接规范并更新流流规范后，您可以通过API或UI开始测试源的功能。 成功后，您可以联系Adobe代表以提交新的源。

以下文档提供了有关如何使用测试和调试源的步骤 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

* 有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).
* 有关如何为Platform API生成凭据的信息，请参阅关于的教程 [身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md).
* 有关如何设置的信息 [!DNL Postman] 有关平台API的信息，请参阅关于的教程 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md).
* 为帮助执行测试和调试过程，请下载 [此处为自助源验证收集与环境](../assets/sdk-verification.zip) 并按照下面列出的步骤执行操作。

## 使用API测试您的源

要使用API测试源，您必须运行 [自助式源验证收集与环境](../assets/sdk-verification.zip) 日期 [!DNL Postman] 同时提供与源相关的相应环境变量。

要开始测试，您必须首先在上设置集合和环境 [!DNL Postman]. 接下来，指定要测试的连接规范ID。

>[!NOTE]
>
>以下所有示例变量都是必须更新的占位符值，以下除外 `flowSpecificationId` 和 `targetConnectionSpecId`，为固定值。

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `x-api-key` | 用于验证Experience PlatformAPI调用的唯一标识符。 请参阅上的教程 [身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 以获取有关如何检索 `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 企业实体，可以拥有或许可产品和服务，并允许其成员访问。 请参阅上的教程 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md) 以获取有关如何检索 `x-gw-ims-org-id` 信息。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | 完成Experience PlatformAPI调用所需的授权令牌。 请参阅上的教程 [身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 以获取有关如何检索 `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | 为了在Platform中使用源数据，必须创建一个目标架构，以根据您的需求构建源数据。 有关如何创建目标XDM架构的详细步骤，请参阅关于的教程 [使用API创建架构](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 与您的架构对应的唯一版本。 | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 此 `meta:altId` 该项会与  `schemaId` 创建新架构时。 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 有关如何创建目标数据集的详细步骤，请参阅关于的教程 [使用API创建数据集](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 映射集可用于定义源架构中的数据如何映射到目标架构的数据。 有关如何创建映射的详细步骤，请参阅关于的教程 [使用API创建映射集](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 与映射集对应的唯一ID。 | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 与源对应的连接规范ID。 这是您之后生成的ID [创建新的连接规范](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 的流程规范ID `GenericStreamingAEP`. **这是一个固定值**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | 摄取的数据登陆所在数据湖的目标连接ID。 **这是一个固定值**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 检查流运行是否完成时要遵循的指定时间间隔。 | `40` |
| `startTime` | 为数据流指定的开始时间。 开始时间的格式必须是unix时间。 | `1597784298` |

提供所有环境变量后，您可以使用以下代码开始运行集合： [!DNL Postman] 界面。 在 [!DNL Postman] 界面中，选择省略号(**...**)旁边 [!DNL Sources SSSs Verification Collection] 然后选择 **运行收藏集**.

![跑步者](../assets/runner.png)

此 [!DNL Runner] 界面，允许您配置数据流的运行顺序。 选择 **运行SSS验证收集** 以运行收藏集。

>[!NOTE]
>
>您可以禁用 **删除流** 如果您希望使用Platform UI中的源监控仪表板，请访问运行订单核对清单。 但是，测试完成后，必须确保删除测试流。

![运行集合](../assets/run-collection.png)

## 使用UI测试源

要在UI中测试源，请在Platform UI中转到您组织的沙盒的源目录。 从这里，您应该看到新源显示在 *流* 类别。

由于新源现在可在沙盒中使用，您必须按照源工作流测试功能。 要开始，请选择 **[!UICONTROL 设置]**.

![显示新流源的源目录。](../assets/testing/catalog-test.png)

此 [!UICONTROL 添加数据] 步骤。 要测试源是否可以流式传输数据，请使用界面的左侧进行上传 [示例JSON数据](../assets/testing/raw.json.zip). 上传数据后，界面的右侧将更新为数据的文件层次结构预览。 选择 **[!UICONTROL 下一个]** 以继续。

![源工作流中的添加数据步骤，您可以在其中上传和预览数据，然后再引入。](../assets/testing/add-data-test.png)

此 [!UICONTROL 数据流详细信息] 页面允许您选择是要使用现有数据集，还是新数据集。 在此过程中，您还可以配置要摄取到配置文件的数据，并启用以下设置 [!UICONTROL 错误诊断] 和 [!UICONTROL 部分摄取].

要进行测试，请选择 **[!UICONTROL 新建数据集]** 并提供输出数据集名称。 在此步骤中，您还可以提供可选描述，以将详细信息添加到数据集。 接下来，使用选择要映射到的架构 [!UICONTROL 高级搜索] 选项中进行选择，或者通过滚动下拉菜单中的现有架构列表来进行选择。 选择架构后，为数据流提供名称和描述。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流中的数据流详细信息步骤。](../assets/testing/dataflow-details-test.png)

此 [!UICONTROL 映射] 步骤随即显示，为您提供了一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的综合步骤，请参阅 [数据准备UI指南](../../../data-prep/ui/mapping.md)

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![源工作流的映射步骤。](../assets/testing/mapping-test.png)

此 **[!UICONTROL 审核]** 步骤，允许您在创建新数据流之前对其进行查看。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示您的帐户名称、源类型以及特定于您使用的流云存储源的其他其他信息。
* **[!UICONTROL 分配数据集和映射字段]**：显示用于数据流的目标数据集和架构。

查看数据流后，选择 **[!UICONTROL 完成]** 并留出一些时间来创建数据流。

![源工作流的审核步骤。](../assets/testing/review-test.png)

最后，您必须检索数据流的流端点。 此端点将用于订阅您的webhook，允许您的流源与Experience Platform通信。 要检索您的流端点，请转到 [!UICONTROL 数据流活动] 之前创建的数据流页面，并从 [!UICONTROL 属性] 面板。

![数据流活动中的流端点。](../assets/testing/endpoint-test.png)

## 提交您的源

在您的来源能够完成整个工作流后，您可以继续联系您的Adobe代表并提交您的来源，以便跨其他Experience Platform组织进行集成。
