---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK；SDK
title: 提交您的源
description: 以下文档提供了有关如何使用Flow Service API测试和验证新源，以及如何通过自助源(Batch SDK)集成新源的步骤。
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# 提交您的源

使用自助式源(Batch SDK)将新源集成到Adobe Experience Platform的最后一步是测试源以进行验证。 成功后，您可以联系Adobe代表以提交新的源。

以下文档提供了有关如何使用测试和调试源的步骤 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

* 有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).
* 有关如何为Platform API生成凭据的信息，请参阅关于的教程 [身份验证和访问Experience PlatformAPI](../../../landing/api-authentication.md).
* 有关如何设置的信息 [!DNL Postman] 有关平台API的信息，请参阅关于的教程 [设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md).
* 为帮助执行测试和调试过程，请下载 [此处为自助源验证收集与环境](../assets/sdk-verification.zip) 并按照下面列出的步骤执行操作。

## 测试源

要测试您的源，您必须运行 [自助式源验证收集与环境](../assets/sdk-verification.zip) 日期 [!DNL Postman] 同时提供与源相关的相应环境变量。

要开始测试，您必须首先在上设置集合和环境 [!DNL Postman]. 接下来，指定要测试的连接规范ID。

### 在“管理工具”中指定分类的 `authSpecName`

输入连接规范ID后，您必须指定 `authSpecName` 用于基础连接的对象。 根据您的选择，这可能是 `OAuth 2 Refresh Code` 或  `Basic Authentication`. 一旦您指定了 `authSpecName`之后，您必须在环境中包含其所需的凭据。 例如，如果您指定 `authSpecName` 作为 `OAuth 2 Refresh Code`，则必须为OAuth 2提供所需的凭据，这些凭据包括 `host` 和 `accessToken`.

### 在“管理工具”中指定分类的 `sourceSpec`

添加验证规范参数后，必须进一步从源规范中添加所需属性。 您可以在中找到所需的属性 `sourceSpec.spec.properties`. 对于 [!DNL MailChimp Members] 下面的示例中，唯一需要的属性是 `listId`，这意味着 `listId` 并且它的ID值与您的 [!DNL Postman] 环境。

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

提供身份验证和源规范参数后，您可以开始填充其余环境变量，请参阅下表以供参考：

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
| `flowSpecificationId` | 的流程规范ID `RestStorageToAEP`. **这是一个固定值**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
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

## 提交您的源

在您的源能够完成整个工作流后，您可以继续联系Adobe代表并提交您的源以进行集成。
