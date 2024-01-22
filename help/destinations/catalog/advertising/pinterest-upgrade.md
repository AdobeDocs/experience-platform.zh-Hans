---
title: pinterest目标迁移到新API。 需要客户操作。
description: pinterest将弃用Real-Time CDP中Pinterest目标当前使用的v4广告商API。 了解您的操作项目，以便无缝过渡到新API而不会中断您的Pinterest营销活动。
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: e3341ec6f62844858ecda7dd4db70d085f0bf217
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# pinterest目标升级到新API。 要求在2024年1月18日之前采取客户行动。

>[!IMPORTANT]
>
>如果您的组织设置了数据流，以在2023年11月16日（新页面发布日期）之前将数据导出到Pinterest，则本页上的客户措施项适用于您 **[!UICONTROL pinterest]** 使用最新Pinterest API的目标已添加到目标目录中。

## 发生了什么情况？

pinterest已弃用v4广告商API，该API用于 [pinterest目标](/help/destinations/catalog/advertising/pinterest.md) 在Real-Time CDP中。 Adobe更新了目标以使用 [v5广告商API](https://developers.pinterest.com/docs/getting-started/migration/). 请参阅此页面，了解您的操作项目，以便无缝过渡到新API而不会中断您的Pinterest营销活动。

## 为什么会通知我？

我们已确定您的组织具有活动数据流以向Pinterest激活受众。

## 有什么计划？

Adobe已发布新的Pinterest目标卡，该卡利用Pinterest API v5，并将保留新连接中的现有数据流。

## 我是否需要执行任何操作来保持激活的受众正常运行？

是，在2024年1月18日之前，您需要在Real-Time CDP中使用Pinterest广告商帐户对新的Pinterest目标进行身份验证。 请参阅下面的详细说明。

### 重新向Pinterest进行身份验证 {#reauthenticate}

1. 转到 **[!UICONTROL 目标>帐户]** 并使用屏幕上的过滤器仅筛选Pinterest目标。
   ![仅筛选Pinterest帐户](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. 在 **pinterest** 目标，选择三点符号……并选择 **[!UICONTROL 编辑详细信息]**.
   ![选择编辑详细信息](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. 选择 **[!UICONTROL 重新连接OAuth]** 并登录到您的Pinterest帐户。
   ![选择重新连接OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. 转到以下部分中的措施项

### 启用流到新目标 {#disable-old-enable-new-flows}

然后，您需要启用新的数据流  **[!UICONTROL pinterest]** 卡片。

1. 转到 **[!UICONTROL 目标>浏览]** 并使用屏幕上的过滤器来筛选 **[!UICONTROL pinterest]** 仅限目标。
   ![仅在“浏览”选项卡中筛选Pinterest数据流](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. 选择要与关联的超链接连接名称（上面屏幕快照示例中的忠诚度促销活动） **[!UICONTROL pinterest]** 目标位置并切换 **[!UICONTROL 启用]** 切换到 **日期**.
   ![为新连接打开和为旧连接关闭](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## 能否分享一些高级别的时间表？

是，请参阅下文：

**2023年11月16日之前**：新目标已准备就绪，您应会在目录中并行看到两张Pinterest信息卡，直到Pinterest停止支持旧的v4 API。 您发送到当前Pinterest卡的所有现有数据流都会复制到新目标。

![并排显示新旧的Pinterest目标](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

<!--

>[!IMPORTANT]
>
>After November 16th, 2023 the legacy Pinterest destination is marked **[!UICONTROL Deprecating]**. <span class="preview">Any changes that you make to dataflows to the (Deprecating) Pinterest destination after November 16th will *not* be automatically carried over to the new Pinterest destination. </span>
>For example, we *do not recommend* that you activate new audiences to the old destination after November 16th. If you do that, you will then have to follow the [regular activation steps](/help/destinations/ui/activate-segment-streaming-destinations.md) to add the audience to the new destination once the customer actions are taken.

-->

**2023年12月15日之前**： <span class="preview">客户操作1</span>. 您需要重新向Pinterest进行身份验证，以便新卡连接到Pinterest。 在中查看完整说明 [本节](#reauthenticate).

<span class="preview">客户操作2</span>然后，您需要在新信息卡中启用数据流。 在中查看完整说明 [本节](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**2024年1月18日之后**： <span class="preview">pinterest已关闭对V4广告商API的访问。 任何尚未升级到新目标的Real-Time CDP客户现在都将发现其数据流无法升级到Pinterest目标。 [重新向Pinterest进行身份验证](#reauthenticate) 和 [启用数据流](#disable-old-enable-new-flows) ，以将营销活动恢复到Pinterest。</span>

<!--

## Other items to note

After you enable the dataflows on the new destination card and disable the dataflows on the old destination cards, you should see no disruption in your campaigns or in the numbers of qualified profiles in the audiences coming in from Adobe Real-Time CDP.

-->
