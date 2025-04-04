---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源sdk；sdk；SDK
title: 提交您的Source
description: 以下文档提供了有关如何使用Flow Service API测试和验证新源，以及通过自助源(批处理SDK)集成新源的步骤。
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# 提交您的源

使用自助式源(批量SDK)将新源集成到Adobe Experience Platform的最后一步是测试源以供验证。 成功后，您可以联系Adobe代表以提交新的源。

以下文档提供了有关如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)测试和调试源的步骤。

## 快速入门

* 有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../landing/api-guide.md)指南。
* 有关如何生成Experience Platform API凭据的信息，请参阅有关[身份验证和访问Experience Platform API](../../../landing/api-authentication.md)的教程。
* 有关如何为Experience Platform API设置[!DNL Postman]的信息，请参阅[设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md)上的教程。
* 为帮助进行测试和调试，请在此处](../assets/sdk-verification.zip)下载[自助式源验证集合和环境，然后执行下面列出的步骤。

## 测试源

要测试您的源，您必须在[!DNL Postman]上运行[自助源验证集合和环境](../assets/sdk-verification.zip)，同时提供与您的源相关的适当环境变量。

要开始测试，您必须先在[!DNL Postman]上设置集合和环境。 接下来，指定要测试的连接规范ID。

### 指定`authSpecName`

输入连接规范ID后，您必须指定用于基本连接的`authSpecName`。 根据您的选择，这可以是`OAuth 2 Refresh Code`或`Basic Authentication`。 指定`authSpecName`后，您必须在环境中包含其所需的凭据。 例如，如果将`authSpecName`指定为`OAuth 2 Refresh Code`，则必须为OAuth 2提供所需的凭据，即`host`和`accessToken`。

### 指定`sourceSpec`

添加验证规范参数后，必须接着从源规范中添加所需属性。 您可以在`sourceSpec.spec.properties`中找到所需的属性。 在以下[!DNL MailChimp Members]示例中，唯一需要的属性是`listId`，这意味着`listId`并且它的ID值对应到您的[!DNL Postman]环境。

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

提供身份验证和源规范参数后，您可以开始填充其余的环境变量，请参阅下表以供参考：

>[!NOTE]
>
>以下所有示例变量都是必须更新的占位符值，但属于固定值的`flowSpecificationId`和`targetConnectionSpecId`除外。

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `x-api-key` | 用于对调用Experience Platform API进行身份验证的唯一标识符。 有关如何检索`x-api-key`的信息，请参阅有关[身份验证和访问Experience Platform API](../../../landing/api-authentication.md)的教程。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 公司实体，可以拥有产品或服务，也可以为其授予产品和服务许可证，并允许其成员访问。 有关如何检索`x-gw-ims-org-id`信息的说明，请参阅有关[设置开发人员控制台和 [!DNL Postman]](../../../landing/postman.md)的教程。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | 完成对Experience Platform API的调用所需的授权令牌。 有关如何检索`authorizationToken`的信息，请参阅有关[身份验证和访问Experience Platform API](../../../landing/api-authentication.md)的教程。 | `Bearer authorizationToken` |
| `schemaId` | 为了在Experience Platform中使用源数据，必须创建目标架构，以根据您的需求构建源数据。 有关如何创建目标XDM架构的详细步骤，请参阅有关使用API [创建架构的教程](../../../xdm/api/schemas.md)。 | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 与您的架构对应的唯一版本。 | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 创建新架构时与`schemaId`一起返回的`meta:altId`。 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 有关如何创建目标数据集的详细步骤，请参阅有关[使用API创建数据集的教程](../../../catalog/api/create-dataset.md)。 | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 映射集可用于定义源架构中的数据如何映射到目标架构的数据。 有关如何创建映射的详细步骤，请参阅有关[使用API创建映射集的教程](../../../data-prep/api/mapping-set.md)。 | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 与映射集对应的唯一ID。 | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 与源对应的连接规范ID。 这是您在[创建新连接规范](./create.md)后生成的ID。 | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 流规范ID `RestStorageToAEP`。 **这是一个固定值**。 | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | 摄取的数据登陆所在数据湖的目标连接ID。 **这是一个固定值**。 | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 检查流运行是否完成时要遵循的指定时间间隔。 | `40` |
| `startTime` | 为数据流指定的开始时间。 开始时间的格式必须为unix时间。 | `1597784298` |

提供所有环境变量后，即可使用[!DNL Postman]界面开始运行集合。 在[!DNL Postman]界面中，选择[!DNL Sources SSSs Verification Collection]旁边的省略号(**...**)，然后选择&#x200B;**运行收藏集**。

![运行者](../assets/runner.png)

将显示[!DNL Runner]接口，允许您配置数据流的运行顺序。 选择&#x200B;**运行SSS验证集合**&#x200B;以运行该集合。

>[!NOTE]
>
>如果您希望在Experience Platform UI中使用源监视仪表板，则可以禁用运行订单清单中的&#x200B;**删除流**。 但是，测试完成后，必须确保删除测试流。

![运行集合](../assets/run-collection.png)

## 提交您的源

在源能够完成整个工作流后，您可以继续联系Adobe代表并提交源以进行集成。
