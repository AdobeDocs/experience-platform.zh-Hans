---
title: 数据收集
description: 了解Adobe Experience Platform Edge Network Server API如何构建收集的数据
seo-description: Learn how the Adobe Experience Platform Edge Network Server API structures the collected data
keywords: 数据收集；收集；Adobe Experience Platform Edge Network;API；结构
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 4%

---


# 数据收集

的 [!DNL Server API] 提供了两种类型的数据收集端点：

* [交互式数据收集端点](interactive-data-collection.md)，用于客户端希望服务器返回响应时。 执行数据收集时，这些端点还可以返回来自其他边缘网络服务的内容。
* [非交互式事件数据收集](non-interactive-data-collection.md)，在服务器没有响应时使用。 这些端点仅用于数据收集。

## `Event` 对象 {#event-object}

由 [!DNL Server API] 在 `Event` 对象。 此对象的结构如下所述。

```json
{
   "xdm":{
      "identityMap":{
         "Email_LC_SHA256":[
            {
               "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
               "primary":true
            }
         ]
      },
      "eventType":"web.webpagedetails.pageViews",
      "web":{
         "webPageDetails":{
            "URL":"https://alloystore.dev/",
            "name":"home-demo-Home Page",
            "pageViews":{
               "value":1
            }
         }
      },
      "placeContext":{
         "localTime":"2021-08-09T17:09:20.859+03:00",
         "localTimezoneOffset":-180
      },
      "timestamp":"2021-08-09T14:09:20.859Z"
   },
   "data":{
      "prop1":"custom value",
      "var10":"search (organic)"
   }
}
```

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| `xdm` | 对象 | *必需*. 包含XDM格式数据的JSON对象，与数据集架构相对应。 |
| `data` | 对象 | *可选*. 包含自由格式数据的JSON对象，这些数据可通过边缘网络映射到XDM。 |

