---
title: 与Adobe Experience Platform Web SDK中的多个资产交互
description: 了解如何与多个Experience PlatformWeb SDK资产交互。
keywords: 多个属性；配置；sendEvent；edgeConfigId；orgId；
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 与多个属性交互

在某些情况下，您可能希望与同一页面上的两个不同属性进行交互。 这些情况包括：

* 已被收购并正致力于整合其网站的公司
* 多个公司之间的数据共享关系
* 正在测试新Adobe解决方案但又不想中断现有实施的客户

SDK允许您通过向基础代码中的数组添加其他名称来为每个属性创建单独的实例。 以下示例提供了两个名称： `mycustomname1` 和 `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

因此，该脚本将创建两个SDK实例。 与第一个实例交互的全局函数已命名 `mycustomname1` 与第二个实例进行交互的全局函数被命名为 `mycustomname2`.

通过创建两个单独的实例，可以为每个实例配置不同的资产。 由于与交互而发生的任何通信或数据持久性 `mycustomname1` 与隔离 `mycustomname2`.

根据上述示例，您可以使用每个实例执行命令，如下所示：

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

请务必执行 `configure` 命令，然后再对同一实例执行其他命令。

## 限制

为避免与Cookie冲突，请仅有一个Adobe Experience Platform实例 [!DNL Web SDK] 页面中可以有一个 `edgeConfigId`. 同样，只有一个Adobe Experience Platform实例 [!DNL Web SDK] 可以有特定的 `orgId`.
