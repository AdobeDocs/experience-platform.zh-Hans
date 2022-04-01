---
title: 与Adobe Experience Platform交互
description: 了解如何使用边缘网络服务器API与Adobe Experience Platform交互
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: 数据收集；出口；analytics;Adobe Experience Platform Edge Network Api;aep
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---


# 与Adobe Experience Platform交互

## 概述 {#overview}

要启用Experience Platform数据收集，您必须先 [配置数据流](../edge/fundamentals/datastreams.md) 将事件转发到Experience Platform数据集。

配置完成后，数据流配置应包含 `com_adobe_experience_platform`，如下例所示：


```json
{
  // datastream config header

  "settings": {
    "com_adobe_experience_platform": {
      "sandboxName": "prod",
      "enabled": true,
      "datasets": {
        "event": {
          "xdmSchema": "https://ns.adobe.com/atag/schemas/35a31609b6d3242736751df469ade031",
          "datasetId": "5f67e6ad9501b0194b5aafb6"
        }
      }
    }

    // other settings
  }
}
```
