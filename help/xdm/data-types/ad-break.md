---
title: 廣告插播資料型別
description: 本檔案提供廣告插播Experience Data Model (XDM)資料型別的概觀。
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 4%

---

# [!UICONTROL 廣告插播] 資料型別

[!UICONTROL 廣告插播] 是標準的體驗資料模型(XDM)資料型別，可描述如何將計時廣告插入定時媒體中。

![資料型別結構](../images/data-types/ad-break.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `_dc.title` | 字符串 | 廣告插播的易記名稱。 |
| `_id` | 字符串 | 廣告插播的唯一識別碼。 |
| `offset` | 整数 | 從主要內容開始的廣告插播位移（以秒為單位）。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
