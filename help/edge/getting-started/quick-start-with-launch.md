---
title: 快速开始Launch
seo-title: Adobe Experience Platform Web SDK快速开始Launch
description: 使用Experience Platform Web SDK扩展收集数据的快速开始指南
seo-description: 使用Experience Platform Web SDK扩展收集数据的快速开始指南
translation-type: tm+mt
source-git-commit: e23b0ce9c20d5d2d770d1c1261fe08de5743325a

---


# （测试版）先决条件

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

目前，Adobe Experience Platform Web SDK仅支持使用XDM将数据发送到Adobe Experience Platform。 您必须满足以下先决条件。

- 启用 [第一方域(CNAME)](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/ec-cookies/cookies-first-party.html) 。 如果您已经拥有Analytics的CNAME，则应使用该CNAME。
- 有权使用Adobe Experience Platform
- 正在使用最新版的访客ID服务

## 准备平台

要能够将数据发送到Adobe Experience Platform，您必须创建一个XDM模式和一个使用该模式的数据集。

- [使用以下混合](../../xdm/tutorials/create-schema-ui.md) 创建模式:
   - ExperienceEvent实施详细信息
   - ExperienceEvent环境详细信息
   - ExperienceEvent Web详细信息
- 将Adobe Experience Platform Web SDK混合添加到您创建的模式
- [使用模式](https://platform.adobe.com/dataset/overview) 创建数据集，让数据登陆

## 创建配置ID

您可以在启动项中使用边缘配 [置工具创建配](../fundamentals/edge-configuration.md) 置ID。

>注意： 您的组织必须列入此功能的白名单。 请联系您的CSM，让列表参与最终的白名单。

## 在Launch中安装SDK

登录到启动并安装扩 `AEP Web SDK` 展。 在安装SDK时，将提示您配置扩展。 输入您在上面请求的配置ID。 该扩展将自动填充您的组织ID。

有关不同配置选项的更多详细信息，请 [参阅配置SDK](../fundamentals/configuring-the-sdk.md)。

## 发送事件

安装扩展后，开始通过从AEP Web SDK扩展添加“发送信标”操作来发送事件。 建议在每次加载页面时至少发送一个事件，并选中“在视图的开始发生”选项。

有关如何跟踪事件的更多详细信息，请参阅 [跟踪事件](../fundamentals/tracking-events.md)。

## 发送数据

您可以发送与您之前创建的模式及事件匹配的数据。 例如，如果您拥有一个商务站点并将商务混音添加到您的模式，则当某人视图产品时，您会发送以下结构。

```javascript
{
  "commerce": {
    "productListAdds": {
        "value":1
    }
  },
  "productListItems":{
      "name":"Floppy Green Hat",
      "SKU":"HATFLP123",
      "product":"1234567",
      "quantity":2
  }
}
```
