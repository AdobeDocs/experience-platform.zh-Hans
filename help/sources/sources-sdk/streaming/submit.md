---
title: 测试并提交源
description: 以下文档提供了有关如何使用流服务API测试和验证新源，以及如何通过自助源（流SDK）集成新源的步骤。
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---

# 测试和提交源

使用自助源（流SDK）将新源集成到Adobe Experience Platform的最后步骤是测试和提交新源。 完成连接规范并更新流流规范后，即可通过API或UI开始测试源的功能。 成功后，您可以联系Adobe代表以提交新来源。

以下文档提供了有关如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

* 有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).
* 有关如何为Platform API生成凭据的信息，请参阅 [验证和访问Experience PlatformAPI](../../../landing/api-authentication.md).
* 有关如何设置 [!DNL Postman] 对于Platform API，请参阅 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md).
* 要帮助您的测试和调试过程，请下载 [此处的自助源验证收集和环境](../assets/sdk-verification.zip) 并按照下面列出的步骤操作。

## 使用API测试源

要使用API测试源，您必须运行 [自助源验证收集和环境](../assets/sdk-verification.zip) on [!DNL Postman] 同时提供与您的源相关的适当环境变量。

要开始测试，您必须先在 [!DNL Postman]. 接下来，指定要测试的连接规范ID。

>[!NOTE]
>
>以下所有示例变量都是必须更新的占位符值，但 `flowSpecificationId` 和 `targetConnectionSpecId`，它们是固定值。

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `x-api-key` | 用于验证对Experience PlatformAPI的调用的唯一标识符。 请参阅 [验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 有关如何检索 `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 拥有或许可产品和服务并允许其成员访问的公司实体。 请参阅 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md) 有关如何检索 `x-gw-ims-org-id` 信息。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | 完成对Experience PlatformAPI的调用所需的授权令牌。 请参阅 [验证和访问Experience PlatformAPI](../../../landing/api-authentication.md) 有关如何检索 `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | 要在Platform中使用源数据，必须创建目标架构以根据您的需求构建源数据。 有关如何创建目标XDM架构的详细步骤，请参阅 [使用API创建模式](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 与您的架构对应的唯一版本。 | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 的 `meta:altId` 与  `schemaId` 创建新模式时。 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 有关如何创建目标数据集的详细步骤，请参阅 [使用API创建数据集](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 映射集可用于定义源架构中的数据如何映射到目标架构的数据。 有关如何创建映射的详细步骤，请参阅 [使用API创建映射集](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 与映射集对应的唯一ID。 | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 与源对应的连接规范ID。 这是您在 [创建新连接规范](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 流量规范ID `GenericStreamingAEP`. **这是一个固定值**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | 摄取的数据所登陆的数据湖的目标连接ID。 **这是一个固定值**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 检查流运行是否完成时要遵循的指定时间间隔。 | `40` |
| `startTime` | 数据流的指定开始时间。 开始时间必须采用unix时间格式。 | `1597784298` |

提供所有环境变量后，您便可以使用 [!DNL Postman] 界面。 在 [!DNL Postman] 界面中，选择省略号(**...**&#x200B;旁边 [!DNL Sources SSSs Verification Collection] 然后选择 **运行集合**.

![运行者](../assets/runner.png)

的 [!DNL Runner] 界面，用于配置数据流的运行顺序。 选择 **运行SSS验证收集** 来运行集合。

>[!NOTE]
>
>您可以禁用 **删除流程** 运行顺序检查列表（如果您希望使用Platform UI中的源监控功能板）中的。 但是，完成测试后，必须确保删除测试流。

![run-collection](../assets/run-collection.png)

## 使用UI测试源

要在UI中测试源，请转到平台UI中贵组织沙盒的源目录。 从此处，您应会看到新源显示在 *流* 类别。

现在，您的沙盒中提供了新源，因此您必须按照源工作流来测试功能。 要开始，请选择 **[!UICONTROL 设置]**.

![显示新流源的源目录。](../assets/testing/catalog-test.png)

的 [!UICONTROL 添加数据] 中。 要测试源是否可以流式传输数据，请使用界面的左侧上传 [JSON数据示例](../assets/testing/raw.json.zip). 上传数据后，界面的右侧会更新为数据的文件层次结构预览。 选择 **[!UICONTROL 下一个]** 以继续。

![源工作流中的“添加数据”步骤，您可以在此步骤中上传和预览摄取前的数据。](../assets/testing/add-data-test.png)

的 [!UICONTROL 数据流详细信息] 页面允许您选择是要使用现有数据集还是新数据集。 在此过程中，您还可以配置要摄取到配置文件的数据，并启用如下设置 [!UICONTROL 错误诊断] 和 [!UICONTROL 部分摄取].

要进行测试，请选择 **[!UICONTROL 新数据集]** 和提供输出数据集名称。 在此步骤中，您还可以提供可选描述，以向数据集添加更多信息。 接下来，使用 [!UICONTROL 高级搜索] 选项或通过滚动下拉菜单中的现有架构列表来迁移。 选择架构后，请为数据流提供名称和描述。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流中的数据流详细步骤。](../assets/testing/dataflow-details-test.png)

的 [!UICONTROL 映射] 此时会显示步骤，为您提供一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据您的需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以导出计算值或计算值。 有关使用映射器界面和计算字段的完整步骤，请参阅 [数据准备UI指南](../../../data-prep/ui/mapping.md)

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![源工作流的映射步骤。](../assets/testing/mapping-test.png)

的 **[!UICONTROL 审阅]** 步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示您的帐户名称、源类型以及特定于您所使用的流云存储源的其他信息。
* **[!UICONTROL 分配数据集和映射字段]**:显示用于数据流的目标数据集和架构。

审核数据流后，选择 **[!UICONTROL 完成]** 并为创建数据流留出一些时间。

![源工作流的审核步骤。](../assets/testing/review-test.png)

最后，必须检索数据流的流端点。 此端点将用于订阅您的Webhook，从而允许您的流源与Experience Platform通信。 要检索流端点，请转到 [!UICONTROL 数据流活动] 数据流的页面，并从 [!UICONTROL 属性] 的上界。

![数据流活动中的流端点。](../assets/testing/endpoint-test.png)

## 提交源

在您的Adobe源能够完成整个工作流后，您可以继续联系您的Experience Platform代表并提交您的源以便与其他客户组织进行集成。
