---
title: pinterest目标迁移到新API。 需要客户操作。
description: pinterest将弃用Real-Time CDP中Pinterest目标当前使用的v4广告商API。 了解您的操作项目，以便无缝过渡到新API而不会中断您的Pinterest营销活动。
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# pinterest目标升级到新API。 要求在2023年12月15日之前采取客户行动

>[!IMPORTANT]
>
>pinterest如果您的组织设置了数据流，以在2023年11月16日之前(该日期为 **[!UICONTROL （新）Pinterest]** 使用最新Pinterest API的目标已添加到目标目录中。

## 发生了什么情况？

pinterest即将弃用v4广告商API，该API当前由 [pinterest目标](/help/destinations/catalog/advertising/pinterest.md) 在Real-Time CDP中。 Adobe正在使用Pinterest，并且正在更新目标以使用 [v5广告商API](https://developers.pinterest.com/docs/getting-started/migration/). 请参阅此页面，了解您的操作项目，以便无缝过渡到新API而不会中断您的Pinterest营销活动。

## 为什么会通知我？

我们已确定您的组织具有活动数据流以向Pinterest激活受众。

## 有什么计划？

Adobe将发布一个新的Pinterest目标卡，该卡利用Pinterest API v5，并在新连接中保留现有数据流。

## 我是否需要执行任何操作来保持激活的受众正常运行？

是，2023年11月16日之后，您需要在Real-Time CDP中使用Pinterest广告商帐户对新的Pinterest目标进行身份验证。 请参阅下面的详细说明。

### 重新向Pinterest进行身份验证 {#reauthenticate}

1. 转到 **[!UICONTROL 目标>帐户]** 并使用屏幕上的过滤器仅筛选Pinterest目标。
   ![仅筛选Pinterest帐户](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. 在 **（新）Pinterest** 目标，选择三点符号……并选择 **[!UICONTROL 编辑详细信息]**.
   ![选择编辑详细信息](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. 选择 **[!UICONTROL 重新连接OAuth]** 并登录到您的Pinterest帐户。
   ![选择重新连接OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. 转到以下部分中的措施项

### 禁用到旧目标的现有流并启用到新目标的流 {#disable-old-enable-new-flows}

然后，您需要手动禁用到旧目标卡的现有流量 **[!UICONTROL （弃用）Pinterest]** 并启用流向新卡片的流 **[!UICONTROL （新）Pinterest]**.

1. 转到 **[!UICONTROL 目标>浏览]** 并使用屏幕上的过滤器来筛选 **[!UICONTROL （新）Pinterest]** 和 **[!UICONTROL （弃用）Pinterest]** 仅限目标。
   ![仅在“浏览”选项卡中筛选Pinterest数据流](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. 选择要与关联的超链接连接名称（上面屏幕快照示例中的忠诚度促销活动） **[!UICONTROL （弃用）Pinterest]** 目标位置并切换 **[!UICONTROL 启用]** 切换到 **关**.
   ![为新连接打开和为旧连接关闭](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-old-destination.png)
3. 选择要与关联的超链接连接名称（上面屏幕快照示例中的忠诚度促销活动） **[!UICONTROL （新）Pinterest]** 目标位置并切换 **[!UICONTROL 启用]** 切换到 **日期**.
   ![为新连接打开和为旧连接关闭](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)
4. 比较旧数据流和新数据流中的激活受众列表，并确保旧数据流中不存在新数据流中缺少的任何新受众。

虽然预计不会造成营销活动中断，但请记得在Pinterest UI中检查一切是否按预期运行。

## 能否分享一些高级别的时间表？

是，请参阅下文：

**2023年11月16日之前**：新目标已准备就绪，您应该会在目录中并行看到两个Pinterest信息卡，并且流向当前Pinterest信息卡的所有现有数据流都会复制到新目标。

![并排显示新旧的Pinterest目标](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>2023年11月16日之后，旧版Pinterest目标会被标记 **[!UICONTROL 弃用]**. <span class="preview">11月16日之后，您对（正在弃用）Pinterest目标的数据流所做的任何更改都将 *非* 自动转移到新的Pinterest目标。 </span>
>例如，我们 *不推荐* 11月16日之后，将新受众激活到旧目标。 如果您这样做，则必须遵循 [常规激活步骤](/help/destinations/ui/activate-segment-streaming-destinations.md) 用于在采取客户操作后将受众添加到新目标。

**2023年12月15日之前**： <span class="preview">客户操作1</span>. 您需要重新向Pinterest进行身份验证，以便新卡连接到Pinterest。 在中查看完整说明 [本节](#reauthenticate).

<span class="preview">客户操作2</span>然后，您需要禁用旧信息卡中指向Pinterest的数据流，并启用新信息卡中的数据流。 在中查看完整说明 [本节](#disable-old-enable-new-flows).

>[!IMPORTANT]
>
>2023年12月15日之后，Adobe不保证旧数据流完整性 **[!UICONTROL （弃用）Pinterest]** 目标。

## 其他须注解项目

在新目标卡上启用数据流并在旧目标卡上禁用数据流后，您应该不会看到营销活动或来自Adobe Real-Time CDP的受众中符合条件的用户档案数发生中断。
