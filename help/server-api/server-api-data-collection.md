---
title: 資料彙集
description: 瞭解Adobe Experience Platform Edge Network Server API如何建構收集的資料。
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---


# 資料彙集

此 [!DNL Server API] 提供兩種型別的資料收集端點：

* [互動式資料收集端點](interactive-data-collection.md)，用於使用者端預期伺服器會傳回回應時。 在執行資料收集時，這些端點也可以從其他Edge Network服務傳回內容。
* [非互動式事件資料彙集](non-interactive-data-collection.md)，在預期伺服器沒有回應時使用。 這些端點僅用於資料收集。

## `Event` 物件 {#event-object}

由收集的資料 [!DNL Server API] 在中建構 `Event` 物件。 此物件的結構如下所述。

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
| `xdm` | 对象 | *必需*. 包含XDM格式資料（對應於資料集結構）的JSON物件。 |
| `data` | 对象 | *可选*. 包含自由格式資料的JSON物件，可由Edge Network對應至XDM。 |

