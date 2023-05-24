---
title: 索引鍵值配對資料型別
description: 本檔案提供索引鍵值配對體驗資料模型(XDM)資料型別的概觀。
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
source-git-commit: 1d023ce6184e54693401eb68a04ceeb1464dcaa0
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---

# [!UICONTROL 金鑰值組] 資料型別

[!UICONTROL 金鑰值組] 是標準的體驗資料模型(XDM)資料型別，可擷取一般索引鍵/值組的詳細資訊。 此資料型別用於 [[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能] 欄位群組](../field-groups/event/analytics-full-extension.md) 說明清單變數的陣列專案。

![索引鍵值配對結構](../images/data-types/key-value-pair.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `key` | 字符串 | 一般變數或值的索引鍵（名稱）。 |
| `value` | 字符串 | 變數的值。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
