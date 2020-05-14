---
title: 与多个属性交互
seo-title: 与多个属性交互的Adobe Experience Platform Web SDK
description: 了解如何与多个Experience Platform Web SDK属性交互
seo-description: 了解如何与多个Experience Platform Web SDK属性交互
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 与多个属性交互

在某些情况下，您可能希望在同一页面上与两个不同的属性交互。 这些包括：

* 已获得并正在努力将其网站集成在一起的公司
* 多个公司之间的数据共享关系
* 正在测试新Adobe解决方案且不想破坏其现有实施的客户

SDK允许您通过在基本代码中向数组添加另一个名称，为每个属性创建一个单独的实例。 在以下示例中，我们提供了两个名 `mycustomname1` 称 `mycustomname2`。

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

因此，该脚本创建SDK的两个实例。 用于与第一实例交互的全局函数被命 `mycustomname1` 名，用于与第二实例交互的全局函数被命名 `mycustomname2`。

通过创建两个单独的实例，可以为每个实例配置不同的属性。 由于与之交互而出现的任何通信或数据持久性 `mycustomname1` 都与之保持隔离， `mycustomname2` 反之亦然。

按照上面的示例，您可以使用每个实例执行命令，如下所示：

```javascript
mycustomname1("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "configId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

请务必为每个实 `configure` 例执行命令，然后对同一实例执行其他命令。

## 限制

为避免与cookies发生冲突，页面中只有一个Adobe Experience Platform Web SDK实例可以具有特定实例 `configId`。  同样，只有一个Adobe Experience Platform Web SDK实例可以具有特定实例 `orgId`。
