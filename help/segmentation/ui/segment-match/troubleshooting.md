---
keywords: Experience Platform；首頁；熱門主題；分段；區段比對；區段比對
solution: Experience Platform
title: 區段比對常見問題集
description: 「區段比對」是Adobe Experience Platform中的區段共用服務，可讓兩名或以上Platform使用者以安全、受管且隱私權友好的方式交換區段資料。
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# [!DNL Segment Match] 常見問題

本指南針對Adobe Experience Platform區段比對的隱私權與法律問題，提供常見問題解答。

## 預估重疊期間會共用哪些資料，以及Adobe如何確保安全地取得這些量度？

![overlap-report.png](./images/overlap-report.png)

沒有客戶或區段資料會在沙箱之間移動，以取得這些重疊預估量度。 客戶在任何指定沙箱中選取的預先雜湊適用身分，會新增至機率資料結構，其中ID本身會以雜湊格式表示。

這是單向流程，表示原始的預先雜湊識別碼不會公開，且無法進行反向工程。

這些資料結構具有獨特的屬性，可讓工程在它們之間執行聯集和交集作業，即使編碼的資訊經過嚴格壓縮或雜湊處理亦然。 這些操作允許 [!DNL Segment Match] 以取得由兩個不同沙箱的ID所組成的兩個資料結構的預估交集，而不需比較實際值。 從 [!DNL Segment Match] ID僅使用資料結構，不會為了預估目的而離開其個別組織的設定檔存放區。 這讓Adobe符合客戶的隱私權及安全性需求，同時提供高度精確的評估工具，以指導資料共同作業協定。

## 指定哪些身分會收到共用區段ID的背後是哪個程式？

[!DNL Segment Match] 讓客戶可選擇設定要在服務中使用的名稱空間。 如果客戶決定將摘要發佈至合作夥伴沙箱，此選擇會同時套用至先前問題中所述的預估程式與資料傳輸程式。

在兩個不同組織的加密身分之間的資料傳輸程式在中性計算環境中執行。 資料傳輸工作屬於Adobe，且參與夥伴關係的組織無權存取此環境，也無法存取任何可能是資料傳輸工作結果的記錄。

只有區段會籍會內嵌到接收者組織的重疊設定檔片段中，並且不會從傳送者組織向接收者組織傳輸其他身分。 資料傳輸工作不會讀取純文字的個人識別資訊(PII)，因為 [!DNL Segment Match] 只要資料是PII，僅允許在SHA256加密的名稱空間（電子郵件/電話）上重疊。 結果永遠不會儲存在運算環境中。
