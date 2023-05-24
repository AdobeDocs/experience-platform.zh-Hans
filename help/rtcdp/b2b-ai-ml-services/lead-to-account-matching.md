---
title: Real-Time CDP B2B中的銷售機會帳戶比對
type: Documentation
description: 有關Experience PlatformCDP B2B中潛在客戶與帳戶比對功能的概述和詳細資訊。
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---

# Real-Time CDP B2B中的銷售機會帳戶比對

## 概述 {#overview}

帳戶式行銷是B2B行銷日益重要的策略。 帳戶式行銷提供下列主要優點，可吸引特定的高價值客戶：

- 清除ROI
- 銷售與行銷協調
- 個人化方法
- 減少浪費的資源
- 較短的銷售週期

帳戶型行銷可將已知人員和匿名Web訪客連結至銷售帳戶。 這可讓行銷團隊在客戶歷程的初期與目標客戶的潛在潛在客戶互動，以增加其轉換機會。 已知個人記錄通常包括下列部分或全部資訊：

- 個人名稱
- 电子邮件地址
- 聯絡電話
- 公司名稱
- 公司網站
- 職稱
- 位置

潛在客戶帳戶比對可讓您將已知人員設定檔聯結到帳戶設定檔。 然後，您可以在B2B內容（例如帳戶、商機等）中劃分資料區段及鎖定資料。 個人資料可以分為以下三個類別：

- **帳戶個人設定檔：** 個人設定檔已透過來自資料來源的關係與至少一個帳戶設定檔相關聯。 這表示至少有一個聯絡人片段。

>[!NOTE]
>
> 執行銷售線索與帳戶比對工作時，帳戶個人檔案不相符。

- **已知人員設定檔：** 此人員設定檔未與任何帳戶設定檔建立關聯，且下列人員設定檔屬性中至少有一個具有值：

   - 电子邮件地址
   - 公司名稱
   - 公司網站

- **匿名人員設定檔：** 此人員設定檔未關聯至任何帳戶設定檔，且下列任何人員設定檔屬性都沒有值：

   - 电子邮件地址
   - 公司名稱
   - 公司網站

>[!NOTE]
>
> 個人設定檔可能與多個帳戶設定檔相關。 不過，銷售線索與帳戶的比對程式只會比對到最佳比對。 如果需要更廣泛的相符集合，請將潛在客戶與帳戶相符與相關帳戶功能相關聯。

## 工作原理 {#how-it-works}

每日執行的工作會同時使用確定性和機率因素，以比對已知的潛在客戶設定檔，而不需建立現有的帳戶關聯。 已知潛在客戶設定檔將具有下列任一可用屬性：

- b2b.companyName
- b2b.companyWebsite
- 工作電子郵件

>[!NOTE]
>
> b2b.personKey.sourceKey屬性必須存在。

b2b.companyName、b2b.companyWebsite和b2b.personKey.sourceKey屬性可位於B2B person結構描述的b2b欄位群組中。

![顯示屬性的B2B人員結構描述](/help/rtcdp/accounts/images/b2b-person-schema.png)

workEmail屬性可作為B2B人員結構描述中的頂層欄位群組找到。

![顯示工作電子郵件的B2B個人結構描述](/help/rtcdp/accounts/images/b2b-person-workemail.png)

只有在符合分數超過內部信賴臨界值時，才會最符合設定檔。 結果會儲存在現有帳戶個人關係XDM的新系統資料集中。

潛在客戶帳戶比對服務會在新的人員設定檔快照可供使用時執行（每24小時執行一次）。 請參閱檔案以取得以下專案的詳細資訊： [銷售線索與帳戶的比對設定](/help/rtcdp/accounts/account-profile-ui-guide.md).

## 如何檢視銷售線索與帳戶的比對輸出 {#how-to-view}

工作執行後，結果會儲存在現有帳戶個人關係XDM的新資料集中。

若要預覽資料集，請選取 **[!UICONTROL 預覽資料集]** 右上角。

![新資料集](/help/rtcdp/accounts/images/b2b-dataset-output.png)

資料集包含相符的帳戶資訊，以及您所選資料集的相符分數。 此 **[!UICONTROL 關係來源]** 欄位會指出是否來自銷售線索與帳戶比對程式。

![預覽資料集信賴分數和輸出](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## 監控銷售線索到帳戶比對工作 {#monitoring-jobs}

您可以透過控制面板監控任何銷售線索的工作狀態和相關度量，以取得帳戶比對工作。

請參閱檔案以取得更多關於 [監控銷售線索與帳戶比對的工作](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
