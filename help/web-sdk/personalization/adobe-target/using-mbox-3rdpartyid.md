---
title: mbox3rdPartyId 的实时配置文件同步
description: 了解如何将mbox3rdPartyId用于Adobe Experience Platform Web SDK。
keywords: 个性化；target；adobe target；renderDecisions；sendEvent；mbox3rdPartyId；
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 5%

---

# 什么是 `mbox3rdPartyId`

Adobe Target中的mbox3rdPartyId是您公司的访客ID，例如您公司的忠诚度计划的会员ID。

当访客登录到某个公司的网站时，该公司通常会创建一个ID，并将其绑定到访客的帐户、会员卡、会员编号或该公司的其他适用标识符。 [了解详情](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html#)


## 使用方法 `mbox3rdPartyId` 使用Web SDK

### 步骤1：配置 `Target Third Party ID Namespace`

配置 `Target Third Party ID Namespace` 在您的 [数据流](../../../datastreams/overview.md)，使用要用作mbox第三方ID的ID命名空间。
[了解有关ID命名空间的更多信息](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans)

![显示Target第三方ID命名空间字段的平台UI。](assets/mbox3rdpartyid.png)

### 第2步：发送 `mbox3rdpartyId` 目标

发送 `mbox3rdpartyId` 在中定位 `sendEvent` 命令，使用您在步骤1中配置的ID命名空间。
[了解有关发送ID的更多信息](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```
