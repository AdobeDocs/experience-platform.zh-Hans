---
description: 本页说明如何使用Destination SDK中的/sample-profiles API端点基于源架构生成示例配置文件。 您可以使用这些示例配置文件来测试基于文件的目标配置。
title: 根据源架构生成示例配置文件
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 1%

---


# 根据源架构生成示例配置文件

测试基于文件的目标的第一步是使用 `/sample-profiles` 端点，以基于您现有的源架构生成示例配置文件。

示例配置文件可以帮助您了解配置文件的JSON结构。 此外，它们还为您提供了一个默认值，您可以使用自己的配置文件数据进行自定义，以便进一步进行目标测试。

## 快速入门 {#getting-started}

在继续之前，请查看 [快速入门指南](../../getting-started.md) 要成功调用API需要了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 先决条件 {#prerequisites}

在使用 `/sample-profiles` 端点，确保您满足以下条件：

* 您有一个通过Destination SDK创建的基于文件的现有目标，并且您可以在以下位置中看到该目标： [目标目录](../../../ui/destinations-workspace.md).
* 您已在Experience PlatformUI中为目标创建至少一个激活流程。 此 `/sample-profiles` 端点根据您在激活流中定义的源架构创建配置文件。 请参阅 [激活教程](../../../ui/activate-batch-profile-destinations.md) 以了解如何创建激活流程。
* 要成功发出API请求，您需要与要测试的目标实例对应的目标实例ID。 在Platform UI中浏览与目标建立的连接时，从URL获取应在API调用中使用的目标实例ID。

  ![显示如何从URL获取目标实例ID的UI图像。](../../assets/testing-api/get-destination-instance-id.png)

## 生成用于目标测试的样本配置文件 {#generate-sample-profiles}

您可以通过对以下网站发出GET请求，根据源架构生成示例配置文件： `/sample-profiles` 具有要测试的目标实例ID的端点。

**API格式**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| 查询参数 | 描述 |
| -------- | ----------- |
| `destinationInstanceId` | 要为其生成示例配置文件的目标实例的ID。 请参阅 [先决条件](#prerequisites) 部分，了解有关如何获取此ID的详细信息。 |
| `count` | *可选*. 要生成的样本配置文件数。 参数可以取的值介于 `1 - 1000`. 如果未定义此属性，则API生成单个示例配置文件。 |

**请求**

以下请求根据目标实例中定义的源架构生成一个具有相应配置文件的示例配置文件 `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回具有指定数量的示例配置文件的HTTP状态200，其中包含与源XDM架构对应的受众成员资格、身份和配置文件属性。

>[!NOTE]
>
> 响应仅返回目标实例中使用的受众成员资格、身份和配置文件属性。 即使源架构具有其他字段，这些字段也会被忽略。

```json
[
   {
      "segmentMembership":{
         "ups":{
            "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
               "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
               "status":"realized"
            },
            "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
               "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
               "status":"realized"
            }
         }
      },
      "personalEmail":{
         "address":"john.smith@abc.com"
      },
      "identityMap":{
         "crmid":[
            {
               "id":"crmid-P1A7l"
            }
         ]
      },
      "person":{
         "name":{
            "firstName":"string",
            "lastName":"string"
         }
      }
   }
]
```

![该图像显示了从UI到API响应中的字段的映射。](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| 属性 | 描述 |
| -------- | ----------- |
| `segmentMembership` | 描述个人受众成员资格的映射对象。 有关的详细信息 `segmentMembership`，读取 [受众成员资格详细信息](../../../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | 上次此配置文件符合区段资格的时间戳。 |
| `status` | 一个字符串字段，指示受众成员资格是否已在当前请求中实现。 接受以下值： <ul><li>`realized`：用户档案是区段的一部分。</li><li>`exited`：作为当前请求的一部分，配置文件将退出受众。</li></ul> |
| `identityMap` | 描述个人的各种标识值及其关联的命名空间的映射类型字段。 有关的详细信息 `identityMap`，请参见 [模式组合基础](../../../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## API错误处理 {#api-error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中的。

## 后续步骤

阅读本文档后，您现在知道如何根据在目标中配置的源架构生成示例配置文件 [激活流程](../../../ui/activate-batch-profile-destinations.md).

您现在可以自定义这些用户档案，或在API返回用户档案时使用，目的是 [测试基于文件的目标配置](file-based-destination-testing-api.md).
