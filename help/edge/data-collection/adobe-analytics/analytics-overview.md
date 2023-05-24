---
title: 搭配Platform Web SDK使用Adobe Analytics
description: 瞭解如何使用Adobe Experience Platform Web SDK傳送資料至Adobe Analytics。
keywords: adobe analytics；analytics；對應的資料；對應的變數；
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 836fa7814a6966903639e871bfaea0563847f363
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 搭配Platform Web SDK使用Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] 可將資料傳送至Adobe Analytics。 這可透過翻譯來運作 `xdm` 轉換為Adobe Analytics可以使用的格式。

## 设置

如果您的Customer Config UI中有對應的報表套裝，Adobe Analytics會自動挑選您傳送的資料。 您可以在此處將一個或多個報告對應到指定的設定。 報表套裝對應後，資料會自動開始流動。

## xdm欄位群組

為了更方便擷取最常見的Adobe Analytics量度，我們提供您可使用的Analytics欄位群組。 如需此結構的詳細資訊，請參閱 [Adobe Analytics ExperienceEvent完整擴充功能結構描述欄位群組](../../../xdm/field-groups/event/analytics-full-extension.md)

## 自動對應的資料

Adobe Experience Platform [!DNL Edge Network] 自動對應許多XDM變數。 下列為這些變數的完整清單 [此處](automatically-mapped-vars.md).

## 手動對應資料

任何未由自動對應的資料 [!DNL Edge Network] 可透過處理規則存取。 資料會使用點標籤法扁平化，並可用作contextData。

如果您的結構描述看起來像這樣。

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

這些會是您可用的內容資料索引鍵。

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

以下是會使用此資料的處理規則範例。

![處理規則介面](./assets/edge_analytics_processing_rules.png)

>[!NOTE]
>
>透過Experience Edge收集，所有事件都會傳送至Analytics，以及您為資料串流設定的任何其他服務。 例如，如果您將Analytics和Target都設定為服務，且您分別針對Analytics和Analytics進行呼叫，則這兩個事件都會傳送至Analytics和Target。 這些事件將記錄在Analytics報表中，並可能影響跳出率等量度。
