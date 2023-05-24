---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；欄位；結構描述；全名；xdm：fullName；人員名稱；名稱；資料型別；資料型別；
solution: Experience Platform
title: 個人名稱資料型別
description: 本檔案提供人員名稱XDM資料型別的概觀。
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# [!UICONTROL 個人名稱] 資料型別

[!UICONTROL 個人名稱] 是標準XDM資料型別，說明人員的全名。 由於不同語言和文化的名稱結構慣例差異極大，因此名稱一律應使用此資料型別進行模型化。

此外，資料型別提供許多可選屬性，可用於只需要使用全名片段的情況，例如建立正式或非正式的問候語。

<img src="../images/data-types/person-name.png" width="500" /><br />

| 属性 | 描述 |
| --- | --- |
| `courtesyTitle` | 個人職稱、尊稱或稱呼的縮寫(例如 `Mr.`， `Miss.`，或 `Dr.`)。 |
| `firstName` | 書寫順序中的名稱第一區段最常在名稱的語言中接受。 |
| `fullName` | 以姓名的語言中最常被接受的書寫順序書寫的個人全名。 |
| `lastName` | 在姓名的語言中最常被接受的書寫順序的最後一個姓名區段。 |
| `middleName` | 名字和姓氏之間提供的中間名、替代名或附加名。 |
| `suffix` | 在個人姓名之後提供的一組字母，以提供其他資訊(例如 `Jr.`， `Sr.`， `M.D.`， `PhD`， `I`， `II`， `III`、等等)。 |

{style="table-layout:auto"}

有關人員名稱資料型別的更多詳細資訊，請參閱公共XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
