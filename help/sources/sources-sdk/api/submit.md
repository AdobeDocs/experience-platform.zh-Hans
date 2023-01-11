---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
title: 提交源
description: 以下文档提供了有关如何使用流服务API测试和验证新源，以及如何通过自助源（批处理SDK）集成新源的步骤。
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# 提交源

使用自助源（批处理SDK）将新源集成到Adobe Experience Platform的最后一步是测试源以进行验证。 成功后，您可以联系Adobe代表以提交新来源。

以下文档提供了有关如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

* 有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).
* 有关如何为Platform API生成凭据的信息，请参阅 [验证和访问Experience PlatformAPI](../../../landing/api-authentication.md).
* 有关如何设置 [!DNL Postman] 对于Platform API，请参阅 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md).
* 要帮助您的测试和调试过程，请下载 [此处的自助源验证收集和环境](../assets/sdk-verification.zip) 并按照下面列出的步骤操作。

## 测试源

要测试源，必须运行 [自助源验证收集和环境](../assets/sdk-verification.zip) on [!DNL Postman] 同时提供与您的源相关的适当环境变量。

要开始测试，您必须先在 [!DNL Postman]. 接下来，指定要测试的连接规范ID。

### 在“管理工具”中指定分类的 `authSpecName`

输入连接规范ID后，必须指定 `authSpecName` 用于基础连接。 根据您的选择，这可能是 `OAuth 2 Refresh Code` 或  `Basic Authentication`. 指定 `authSpecName`，则必须在环境中包含其必需的凭据。 例如，如果您指定 `authSpecName` as `OAuth 2 Refresh Code`，则您必须为OAuth 2提供必需的凭据，这些凭据 `host` 和 `accessToken`.

### 在“管理工具”中指定分类的 `sourceSpec`

添加身份验证规范参数后，您必须从源规范中添加所需的属性。 您可以在 `sourceSpec.spec.properties`. 对于 [!DNL MailChimp Members] 以下示例中，唯一必需的属性是 `listId`，表示 `listId` 并且它与 [!DNL Postman] 环境。

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

提供身份验证和源规范参数后，您可以开始填充其余的环境变量，请参阅下表以作参考：

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
| `flowSpecificationId` | 流量规范ID `RestStorageToAEP`. **这是一个固定值**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
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

## 提交源

在您的源代码能够完成整个工作流后，您可以继续联系您的Adobe代表并提交源代码以进行集成。
