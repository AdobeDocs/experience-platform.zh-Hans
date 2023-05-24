---
title: 與Adobe Experience Platform Web SDK中的多個屬性互動
description: 瞭解如何與多個Experience PlatformWeb SDK屬性互動。
keywords: 多個屬性；設定；sendEvent；edgeConfigId；orgId；
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 與多個屬性互動

在某些情況下，您可能會想要與相同頁面上的兩個不同屬性互動。 這些案例包括：

* 已收購且正致力於整合其網站的公司
* 多家公司之間的資料共用關係
* 正在測試新Adobe解決方案且不想中斷現有實施的客戶

SDK可讓您藉由在基底程式碼中的陣列中新增其他名稱，為每個屬性建立個別的執行個體。 下列範例提供兩個名稱： `mycustomname1` 和 `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

因此，指令碼會建立兩個SDK例項。 與第一個執行個體互動的全域函式已命名 `mycustomname1` 而用來與第二個執行個體互動的全域函式已命名 `mycustomname2`.

藉由建立兩個個別的執行個體，每個執行個體都可以針對不同的屬性進行設定。 由於與互動而發生的任何通訊或資料持續性 `mycustomname1` 與隔離 `mycustomname2`.

在上述範例之後，您可以使用每個例證執行命令，如下所示：

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

請務必執行 `configure` 命令之前，執行相同執行個體上的其他命令。

## 限制

為避免與Cookie衝突，請只使用一個Adobe Experience Platform例項 [!DNL Web SDK] 在頁面中可以有特定 `edgeConfigId`. 同樣地，只有一個Adobe Experience Platform例項 [!DNL Web SDK] 可以有特定 `orgId`.
