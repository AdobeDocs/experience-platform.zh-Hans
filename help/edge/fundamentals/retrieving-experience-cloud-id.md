---
title: 检索Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK检索Experience Cloud ID
description: 了解如何获取Adobe Experience Cloud Id。
seo-description: 了解如何获取Adobe Experience Cloud Id。
translation-type: tm+mt
source-git-commit: fc48c11cb1f8a88f9fec8a36646f59f39ac3819f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---


# （测试版）检索Experience Cloud ID

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Cloud为每个消费者使用一个唯一ID。 如果要使用此唯一ID，请使用该命 `getIdentity` 令。 `getIdentity` 返回当前访客的现有ECID。 对于尚未具有ECID的首次访客，此命令将生成新ECID。

>[!NOTE]
>
>此方法通常用于需要读取Experience Cloud ID的自定义解决方案。 标准实施不使用它。

```javascript
alloy("getIdentity")
  .then(function(ecid) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```
