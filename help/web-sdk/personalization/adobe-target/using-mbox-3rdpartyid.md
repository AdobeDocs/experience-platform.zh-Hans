---
title: mbox3rdPartyId的实时配置文件同步
description: 了解如何将mbox3rdPartyId用于Adobe Experience Platform Web SDK。
keywords: 个性化；target；adobe target；renderDecisions；sendEvent；mbox3rdPartyId；
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---

# `mbox3rdPartyId`是什么

Adobe Target中的mbox3rdPartyId是您公司的访客ID，例如您公司的忠诚度计划的会员ID。

当访客登录到某个公司的网站时，该公司通常会创建一个ID，并将其绑定到访客的帐户、会员卡、会员编号或该公司的其他适用标识符。 [了解详情](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=zh-Hans#)


## 如何将`mbox3rdPartyId`与Web SDK一起使用

### 步骤1：配置`Target Third Party ID Namespace`

使用要用作mbox第三方ID的ID命名空间，在[数据流](../../../datastreams/overview.md)中配置`Target Third Party ID Namespace`。
[了解有关ID命名空间的更多信息](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans)

![Experience Platform UI显示Target第三方ID命名空间字段。](assets/mbox3rdpartyid.png)

### 步骤2：将`mbox3rdpartyId`发送到Target

使用您在步骤1中配置的ID命名空间，在`sendEvent`命令中将`mbox3rdpartyId`发送到Target。
[了解有关发送ID的详细信息](../../identity/overview.md#syncing-identities)

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
