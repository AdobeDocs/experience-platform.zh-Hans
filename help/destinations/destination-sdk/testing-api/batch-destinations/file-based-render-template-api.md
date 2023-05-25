---
description: 此页说明如何使用/authoring/testing/template/render端点可视化目标配置中定义的模板化客户数据字段的外观。
title: 验证模板化的客户字段
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 6bd169075cd3826ae2a0907e6e624fd901076a4a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# 验证模板化的客户字段

## 概述 {#overview}

此 `/authoring/testing/template/render` 端点帮助您可视化模板化的方法 [客户数据字段](../../functionality/destination-configuration/customer-data-fields.md) 在目标配置中定义的内容，如下所示。

端点会为您的客户数据字段生成随机值，并在响应中返回它们。 这有助于您验证客户数据字段的语义结构，例如存储段名称或文件夹路径。

## 快速入门 {#getting-started}

在继续之前，请查看 [快速入门指南](../../getting-started.md) 要成功调用API需要了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 先决条件 {#prerequisites}

在使用 `/template/render` 端点，确保您满足以下条件：

* 您有一个通过Destination SDK创建的基于文件的现有目标，并且您可以在以下位置中看到该目标： [目标目录](../../../ui/destinations-workspace.md).
* 要成功发出API请求，您需要与要测试的目标实例对应的目标实例ID。 在Platform UI中浏览与目标建立的连接时，从URL获取应在API调用中使用的目标实例ID。

   ![显示如何从URL获取目标实例ID的UI图像。](../../assets/testing-api/get-destination-instance-id.png)

## 呈现模板化的客户字段 {#render-customer-fields}

**API格式**

```http
POST /authoring/testing/template/render/destination
```

为了说明此API端点的行为，让我们考虑一个包含以下客户数据字段配置的基于文件的目标：

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**请求**

以下请求调用 `/authoring/testing/template/render` 端点，它会返回一个响应，其中包含上面提到的两个客户数据字段的随机生成值。

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| 参数 | 描述 |
| -------- | ----------- |
| `destinationId` | 的ID [目标配置](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 您正在测试的对象。 |
| `templates` | 在中定义的模板化字段名称 [目标服务器配置](../../authoring-api/destination-server/create-destination-server.md). |

**响应**

成功的响应会返回 `HTTP 200 OK` 状态，正文包括为模板化字段随机生成的值。

此响应可帮助您验证客户数据字段的正确结构，例如存储段名称或文件夹路径。


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## API错误处理 {#api-error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中的。

## 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何验证中定义的客户数据字段配置 [目标服务器](../../authoring-api/destination-server/create-destination-server.md).
