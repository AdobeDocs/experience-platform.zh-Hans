---
title: 快速入门
seo-title: Adobe Experience Platform Web SDK与Launch快速入门
description: 使用Experience Platform Web SDK扩展收集数据的快速入门指南
seo-description: 使用Experience Platform Web SDK扩展收集数据的快速入门指南
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （测试版）先决条件

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

目前，Adobe Experience Platform Web SDK仅支持使用XDM将数据发送到Adobe Experience Platform。 您必须满足以下先决条件。

- 启用 [第一方域(CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) 。 如果您已经拥有Analytics的CNAME，则应使用该CNAME。
- 有权使用Adobe Experience Platform
- 正在使用最新版本的访客ID服务

## 准备平台

要能够将数据发送到Adobe Experience Platform，必须创建XDM架构和使用该架构的数据集。

- [使用以下混音创建架构](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md) :
   - ExperienceEvent实施详细信息
   - ExperienceEvent环境详细信息
   - ExperienceEvent Web详细信息
- 将Adobe Experience Platform Web SDK混音添加到您创建的架构
- [使用您的架构](https://platform.adobe.com/dataset/overview) ，创建数据集，以便将数据放入此位置

## 请求配置ID

您必须具有配置ID才能使用SDK。 配置ID可确保您的数据路由到正确的位置。 您可以从顾问处或通过客户关怀获得配置ID。 他们需要以下信息：

- **组织ID:** 您可以使用此处的说明找到 [它](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html)
- **数据集ID:** 单击数据集时，该功能在数据集UI中可用
- **架构ID:** 在架构创建屏幕的URL中可用
- **友好名称：** 这是将来用于此配置的UI中的易记名称

## 在Launch中安装SDK

登录到启动并安装扩 `AEP Web SDK` 展。 在安装SDK时，将提示您配置扩展。 输入您在上面请求的配置ID。 该扩展会自动填充您的组织ID。

有关不同配置选项的更多详细信息，请 [参阅配置SDK](../fundamentals/configuring-the-sdk.md)。

## 发送活动

安装扩展后，通过从AEP Web SDK扩展添加“发送信标”动作，开始发送事件。 建议您在每次加载页面时至少发送一个事件，并选中“在视图开始时发生”选项。

有关如何跟踪事件的更多详细信息，请参阅 [跟踪事件](../fundamentals/tracking-events.md)。

## 发送数据

您可以发送与之前创建的架构及事件相匹配的数据。 例如，如果您拥有一个商务站点，并将商务混音添加到您的架构中，则当某人查看产品时，您会发送以下结构。

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
