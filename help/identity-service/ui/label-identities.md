---
keywords: Experience Platform；首頁；熱門主題；標籤身分
title: 在UI中將欄位標示為身分
description: 包含個人識別資訊(PII)的欄位可以標示為身分欄位。 身分欄位中提供的值會由Identity Service解譯為身分。 身分的名稱空間是在標示欄位時指定。
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 在UI中將欄位標示為身分

包含個人識別資訊(PII)的欄位可以標示為身分欄位。 身分欄位中提供的值會由解譯為身分 [!DNL Identity Service]. 身分的名稱空間是在標示欄位時指定。

欄位必須符合下列條件才能標籤為身分：

* 只有字串型別欄位可用於身分
* 身分只能在記錄和時間序列資料中識別
* 只有PII欄位應該標示為身分。 選擇代表較通用資料的欄位會導致關係較不精確，並且可能導致從身分圖表存取相關身分時發生錯誤

如需如何在UI中標籤身分欄位的指示，請參閱以下指南： [在UI中定義身分欄位](../../xdm/ui/fields/identity.md).

## 后续步骤

如需詳細資訊，請參閱 [!DNL Identity Service]，請參閱 [[!DNL Identity Service] 概觀](../home.md).
