---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；網頁詳細資訊；資料型別；資料型別；資料型別；網頁
solution: Experience Platform
title: 網頁資訊資料型別
description: 本檔案提供網頁資訊Experience Data Model (XDM)資料型別的概觀。
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# [!UICONTROL 網頁資訊] 資料型別

[!UICONTROL 網頁資訊] 是標準的體驗資料模型(XDM)資料型別，可描述透過特定於全球資訊網通道的體驗事件所記錄的資訊，包括網頁、反向連結及/或與頁面上的互動相關的連結。

![](../images/data-types/web-information.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL 網路互動]](./web-interaction.md) | 說明與互動對應的網頁連結或URL的詳細資訊。 |
| `webPageDetails` | [[!UICONTROL 網頁詳細資料]](./webpage-details.md) | 說明發生網路互動之網頁的詳細資料。 |
| `webReferrer` | [!UICONTROL 对象] | 說明網頁互動的反向連結，這是目前網頁互動有記錄前訪客剛造訪過的URL。 包含下列子屬性： <ul><li>`URL`：反向連結URL。</li><li>`type`：反向連結型別。</li></ul> |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)
