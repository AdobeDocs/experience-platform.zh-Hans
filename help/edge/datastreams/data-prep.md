---
title: 为数据收集准备数据
description: 了解在为Adobe Experience Platform Web和移动SDK配置数据流时，如何将数据映射到Experience Data Model(XDM)事件模式。
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 1%

---

# 为数据收集准备数据

数据准备是一项Adobe Experience Platform服务，它允许您映射、转换和验证数据以及从中映射、转换和验证数据 [体验数据模型(XDM)](../../xdm/home.md). 配置启用了平台的 [数据流](./overview.md)，则可以在将源数据发送到Platform Edge Network时，使用数据准备功能将其映射到XDM。

>[!NOTE]
>
>有关所有数据准备功能（包括计算字段的转换函数）的全面指导，请参阅以下文档：
>
>* [数据准备概述](../../data-prep/home.md)
>* [数据准备映射函数](../../data-prep/functions.md)
>* [使用数据准备处理数据格式](../../data-prep/data-handling.md)


本指南介绍如何在数据收集UI中映射数据。 要按照这些步骤进行操作，请开始创建一个数据流（包括） [基本配置步骤](./overview.md#create).

有关数据收集的数据准备过程的快速演示，请参阅以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL 选择数据] {#select-data}

选择 **[!UICONTROL 保存并添加映射]** 完成数据流的基本配置后， **[!UICONTROL 选择数据]** 中。 在此，您必须提供一个JSON对象示例，该对象表示您计划发送到Platform的数据的结构。

要直接从数据层捕获属性，JSON对象必须具有单个根属性 `data`. 的子属性 `data` 然后，应以映射到要捕获的数据层属性的方式构建对象。 选择以下部分，查看带有 `data` 根。

+++JSON文件示例(包含 `data` 根

```json
{
  "data": {
    "eventMergeId": "cce1b53c-571f-4f36-b3c1-153d85be6602",
    "eventType": "view:load",
    "timestamp": "2021-09-30T14:50:09.604Z",
    "web": {
      "webPageDetails": {
        "siteSection": "Product section",
        "server": "example.com",
        "name": "product home",
        "URL": "https://www.example.com"
      },
      "webReferrer": {
        "URL": "https://www.adobe.com/index2.html",
        "type": "external"
      }
    },
    "commerce": {
      "purchase": 1,
      "order": {
        "orderID": "1234"
      }
    },
    "product": [
      {
        "productInfo": {
          "productID": "123"
        }
      },
      {
        "productInfo": {
          "productID": "1234"
        }
      }
    ],
    "reservation": {
      "id": "anc45123xlm",
      "name": "Embassy Suits",
      "SKU": "12345-L",
      "skuVariant": "12345-LG-R",
      "priceTotal": "112.99",
      "currencyCode": "USD",
      "adults": 2,
      "children": 3,
      "productAddMethod": "PDP",
      "_namespace": {
        "test": 1,
        "priceTotal": "112.99",
        "category": "Overnight Stay"
      },
      "freeCancellation": false,
      "cancellationFee": 20,
      "refundable": true
    }
  }
}
```

+++

要从XDM对象数据元素中捕获属性，相同的规则将应用于JSON对象，但根属性必须以 `xdm` 中。 选择以下部分，可查看带有 `xdm` 根。

+++JSON文件示例(包含 `xdm` 根

```json
{
  "xdm": {
    "environment": {
      "type": "browser",
      "browserDetails": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36",
        "javaScriptEnabled": true,
        "javaScriptVersion": "1.8.5",
        "cookiesEnabled": true,
        "viewportHeight": 900,
        "viewportWidth": 1680,
        "javaEnabled": true
      },
      "domain": "adobe.com",
      "colorDepth": 24,
      "viewportHeight": 1050,
      "viewportWidth": 1680
    },
    "device": {
      "screenHeight": 1050,
      "screenWidth": 1680
    }
  }
}
```

+++

您可以选择将对象上传为文件的选项，或将原始对象粘贴到提供的文本框中。 如果JSON有效，则会在右侧面板中显示预览架构。 选择 **[!UICONTROL 下一个]** 继续。

![预期传入数据的JSON示例](../images/datastreams/data-prep/select-data.png)

## [!UICONTROL 映射]

的 **[!UICONTROL 映射]** 步骤，允许您将源数据中的字段映射到平台中目标事件架构的字段。 在此，您可以通过两种方式配置映射：

* [创建新映射规则](#create-mapping) 的数据流。
* [导入映射规则](#import-mapping) 来自现有数据流。

### 创建新映射 {#create-mapping}

要开始配置，请选择 **[!UICONTROL 添加新映射]** 创建新映射行。

![添加新映射](../images/datastreams/data-prep/add-new-mapping.png)

选择源图标(![“源”图标](../images/datastreams/data-prep/source-icon.png))，并在出现的对话框中，选择要在提供的画布中映射的源字段。 选择字段后，请使用 **[!UICONTROL 选择]** 按钮继续。

![选择要在源架构中映射的字段](../images/datastreams/data-prep/source-mapping.png)

接下来，选择架构图标(![“架构”图标](../images/datastreams/data-prep/schema-icon.png))以打开目标事件架构的类似对话框。 选择要在确认之前将数据映射到的字段 **[!UICONTROL 选择]**.

![选择要在目标架构中映射的字段](../images/datastreams/data-prep/target-mapping.png)

此时将重新显示映射页面，并显示已完成的字段映射。 的 **[!UICONTROL 映射进度]** 部分更新以反映已成功映射的字段总数。

![已成功映射反映进度的字段](../images/datastreams/data-prep/field-mapped.png)

>[!TIP]
>
>如果要将一个对象数组（在源字段中）映射到不同对象的数组（在目标字段中），请添加 `[*]` 在源和目标字段路径中的数组名称之后，如下所示。
>
>![数组对象映射](../images/datastreams/data-prep/array-object-mapping.png)

### 导入现有映射规则 {#import-mapping}

如果您之前创建过数据流，则可以将其配置的映射规则重新用于新数据流。

>[!WARNING]
>
>从其他数据流导入映射规则将覆盖您在导入之前可能添加的任何字段映射。

要开始，请选择 **[!UICONTROL 导入映射]**.

![显示 [!UICONTROL 导入映射] 按钮](../images/datastreams/data-prep/import-mapping-button.png)

在显示的对话框中，选择要导入其映射规则的数据流。 选择数据流后，选择 **[!UICONTROL 预览]**.

![显示正在选择的现有数据流的图像](../images/datastreams/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>数据流只能在同一数据流中导入 [沙盒](../../sandboxes/home.md). 换言之，您无法将数据流从一个沙盒导入到另一个沙盒。

下一个屏幕显示所选数据流的已保存映射规则的预览。 确保显示的映射符合您的预期，然后选择 **[!UICONTROL 导入]** 以确认映射并将其添加到新数据流。

![显示要导入的映射规则的图像](../images/datastreams/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>如果导入的映射规则中的任何源字段未包含在示例JSON数据中 [提前提供](#select-data)，则导入中将不包含这些字段映射。

### 完成映射

继续按照上述步骤将其余字段映射到目标架构。 虽然您不必映射所有可用的源字段，但必须映射目标架构中设置为必需的任何字段，才能完成此步骤。 的 **[!UICONTROL 必填字段]** 计数器指示当前配置中尚未映射的必填字段数。

当必填字段计数达到零且您对映射满意后，请选择 **[!UICONTROL 保存]** 完成更改。

![映射完成](../images/datastreams/data-prep/mapping-complete.png)

## 后续步骤

本指南介绍了在数据收集UI中设置数据流时如何将数据映射到XDM。 如果您遵循的是常规数据流教程，则现在可以返回到 [查看数据流详细信息](./overview.md).
