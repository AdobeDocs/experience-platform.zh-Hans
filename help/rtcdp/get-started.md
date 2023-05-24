---
keywords: RTCDP；CDP；Real-time Customer Data Platform；即時客戶資料平台；real time cdp；cdp；rtcdp
title: Real-time Customer Data Platform快速入門
description: 在设置您实施的 Adobe Real-Time Customer Data Platform 时请使用此样板场景作为示例。
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2333'
ht-degree: 2%

---

# Real-time Customer Data Platform快速入門

本快速入門手冊將引導您逐步瞭解Real-time Customer Data Platform (Real-Time CDP)的範例實作。 您可以在設定自己的實作時以此為例。 雖然本指南會顯示特定範例，但連結至您可在建立設定時使用的其他資訊。

此範例顯示由Adobe Experience Platform提供支援的Real-time Customer Data Platform的強大功能，可以：

* 從多個來源擷取資料
* 將它們合併為單一 [!DNL real-time customer profile]
* 跨裝置提供一致、相關和個人化的體驗。

## 用例

運動服裝公司Luma一直致力於改善客戶體驗。 他們推出一項新計畫，以提高與禮品相關的銷售額。 此外他們還想減少過度曝光，例如追蹤客戶瀏覽的惱人廣告。

目前，他們在針對訪客日後不會購買的專案重新定位的媒體上花費過多。 例如，Luma不想重新鎖定某人，讓該專案原本是要供其他人一次性購買的。

目前，Luma的資料分散於多個來源。 因此，他們面臨重大挑戰：

* 行銷組織必須與各自擁有資料來源（包括網站、行動應用程式、忠誠度系統、CRM等）的各種團隊合作。
* 當行銷團隊存取資料時，資料通常已過時，不再與其對時間敏感的行銷活動相關。
* 他們需要統一資料，以便鎖定個人而非管道。

因此，Luma具備下列業務目標：

* 從其不同的資料來源建立消費者的即時單一檢視。
* 使用不同管道和裝置中的相關訊息，個人化行銷活動。

為了達成這些目標，行銷團隊需要能夠大規模管理客戶資料。

透過Adobe Experience Platform提供的Real-Time CDP，Luma的行銷組織可以：

1. 從不同的平台收集資料，並確保其可供下游其他行銷活動使用。
1. 建立其消費者的單一即時檢視，不受資料來源地限制。
1. 在每個接觸點上推動一致、相關和個人化的體驗。

## 步骤

本教學課程包含下列步驟：

1. 建置 [客戶設定檔](#customer-profile).
1. [個人化](#personalizing-the-user-experience) 使用者體驗。
1. 使用 [多個資料來源](#using-multiple-data-sources).
1. [配置数据源](#configuring-a-data-source).
1. [收集資料](#bringing-the-data-together-for-a-specific-customer) 適用於特定客戶。
1. 設定 [區段](#segments).
1. 設定 [目的地](#destinations).
1. [跨裝置拼接設定檔](#cross-device-identity-stitching).
1. [分析設定檔](#analyzing-the-profile).

## 客戶設定檔

客戶首次造訪您的網站時，您對他們一無所知。

![image](assets/luma-site.png)

導覽時，系統會即時擷取資料，不僅會傳送至Adobe Analytics中的報表套裝，也會直接傳送至Adobe Experience Platform。 收集資料時，您會根據中的行為資料，開始形成消費者的單一檢視。 [!DNL Experience Platform's real-time customer profile].

網站的許多訪客可能是先前從Luma購買的回頭客。  Luma必須個人化傳訊和供應專案，以處理新訪客和回訪訪客以及知名客戶。

### 新客戶的首次造訪

例如，未識別的訪客導覽至Luma網站上的男性區段，並檢視幾件運動衫。

![image](assets/luma-sweatshirts.png)

當客戶導覽以深入瞭解這些產品時，這些產品檢視會在Adobe Analytics中收集並傳送至 [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

Luma可將訪客的行為對應至Adobe Experience Platform上的使用者設定檔，並開始收集該消費者行為的更豐富檢視。

### 取得更詳細的客戶檢視

隨著客戶繼續與網站互動，畫面會更清晰。 例如，假設訪客新增產品至購物車並登入。

客戶登入時，她自稱是Sarah Rose。

![image](assets/luma-login.png)

兩個身分已合併：

* 匿名瀏覽資料
* 與Sarah Rose的帳戶相關聯的現有資料

兩個身分都會合併為中的單一設定檔 [!DNL Experience Platform]. Luma現在擁有此消費者的統一檢視。

根據匿名訪客在網站男性區段的瀏覽行為，我們可能假設該客戶為男性。 Luma現在已經登入，可以辨識Sarah Rose了。 Luma使用 [!DNL Real-Time Customer Profile] 以調整跨頻道傳送給她的訊息。

## 個人化使用者體驗

我們以忠誠訊息歡迎Sarah，並感謝Sarah成為銅級會員，提供更多關於福利以及如何提升其地位和積分的資訊。

她導覽至首頁以瀏覽更多內容。

![image](assets/luma-personal.png)

Sarah會獲得個人化的首頁體驗，並依據她動態傳送 [!DNL Real-Time Customer Profile] 在Adobe Experience Platform中。

她能看到相關內容，這要歸功於Adobe Target中的Adobe Sensei支援個人化，其中會考量她過去的購買行為以及對於執行服裝和用具的相似性。 Luma也根據她最近瀏覽過的內容，為男士量身打造適合跑步的男士目錄內容。

在本頁的下方，Sarah會看到精選產品，以及根據她最近檢視的專案而設計的新建議匣。

此個人化內容可協助Sarah快速找到相關專案。 這能增加轉換次數，並提供更令人愉快的客戶體驗。

### 帶回客戶

Sarah分心並離開網站，結束工作階段。 Luma可在Adobe Experience Platform中使用她的資料，協助將她帶回網站。

Real-time Customer Data Platform採用Adobe Experience Platform技術，專為客戶體驗管理而打造。 它可讓組織：

* 簡化資料整合與啟用
* 控管已知和未知的資料使用方式
* 大規模加速行銷使用案例

## 使用多个数据源

Luma的團隊將其所有行為和客戶資料放在一個地方。

![image](assets/luma-dash.png)

他們可以擷取下列所有來源的資料：

* 現有的Adobe Experience Cloud解決方案資料
* 非Adobe來源，例如Luma的忠誠度計畫、客服中心和銷售點系統資料
* 來自Luma資料來源的即時串流資料
* 來自Adobe解決方案的即時資料（無需新標籤）

來自不同來源的所有這些資料會合併至單一統一客戶設定檔中。

## 配置数据源

使用 [!DNL Real-Time Customer Data Platform] 將新的資料來源帶入Platform。 Real-Time CDP包括資料來源目錄，可快速輕鬆地新增至設定檔。

![image](assets/luma-source-cat.png)

例如，若要內嵌Luma的CRM資料，請篩選目錄 *CRM*，以及所有內含下列專案的現成可用聯結器 *CRM* 都會列出。 若要新增 [!DNL Microsoft Dynamics CRM] 資料：

1. 授權連線。

   ![image](assets/luma-source-auth.png)

1. 從建議的XDM預先對應表格清單中選擇要匯入的內容。

   <!--    ![image](assets/luma-source-import.png) -->

   例如，選取 **[!UICONTROL 連絡人]**. 連絡人資料的預覽會自動載入，因此您可以確保一切如預期般顯示。

   Adobe Experience Platform會將標準欄位自動對應至 [!DNL Experience Data Model] (XDM)設定檔結構描述。

1. 檢閱欄位對應。

   <!--    ![image](assets/luma-source-mapping.png) -->

   例如，仔細檢查連絡人的電子郵件欄位是否已正確對應。\
   您可以選擇預覽資料並執行進階對應。

1. 設定排程。

   ![image](assets/luma-source-sched.png)

已完成。 您剛才已新增 [!DNL Microsoft CRM] 做為資料來源至 [!DNL Experience Platform].

### 標籤使用原則的內嵌資料

Luma有許多內部原則，會限制使用特定種類的已收集資訊，且必須符合資料使用方面的法律和隱私權相關考量。 使用Adobe Experience Platform資料控管，可將預先定義的資料使用標籤套用至資料集（以及這些資料集內的特定欄位），讓Luma根據特定使用限制來分類其資料。

![](assets/governance-labels.png)

套用資料使用標籤後，Luma就可以使用資料控管來建立資料使用原則。 資料使用原則是描述您可在包含特定標籤的資料上執行的動作型別的規則。 當嘗試在Real-Time CDP中執行構成原則違規的動作時，會阻止該動作，並提供警示以顯示違反哪個原則及原因。

## 將特定客戶的資料彙集在一起

在此案例中，搜尋Sarah Rose的設定檔。 她的個人資料隨即出現，並附上她用來登入的電子郵件。

<!-- ![image](assets/luma-find-profile.png) -->

Luma擁有的所有關於Sarah顯示器的設定檔資訊。 這包括她的個人資訊，例如地址和電話號碼、通訊偏好設定以及她符合資格的區段。

| 类别 | 描述 |
|---|---|
| 标识 | 顯示連結在一起的身分 [!DNL Platform] 來自Sarah跨頻道和裝置與Luma的互動。 會顯示她來自網站的ECID。 她的身分也包含行動應用程式的ECID、電子郵件ID，以及最近新增的CRM ID [!DNL Microsoft Dynamics] 和從Luma忠誠度系統傳入Adobe Experience Platform的忠誠度ID。 |
| 事件 | 顯示Sarah與Luma品牌的所有互動資料。 這包括她剛檢視的專案、過去檢視的任何專案、收到的電子郵件、她與客服中心的互動，以及每次互動發生在哪個頻道和裝置。 |

Real-Time CDP設定檔可將Luma行銷團隊的工作流程從數週縮短至數分鐘，並根據此360度客戶檢視開啟個人化的可能性。 設定檔會合併她在登入前瀏覽網站時的行為資料，以及她現有的客戶設定檔，以建立Sarah的全面檢視。

行銷團隊可以使用此增強功能、 [!DNL Real-Time Customer Profile] 以便更個人化Sarah的體驗，並提高她對Luma的品牌忠誠度。

## 区段

強大的Adobe Experience Platform區段功能可讓行銷人員根據中擷取的資料，結合屬性、事件和現有區段 [!DNL Real-Time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

在此案例中，Sarah最近在網站上的互動表現出與她過去行為不同的行為。 她通常購買女裝。 不過，她購物車中的商品是男士大運動衫。

Luma資料科學團隊已針對購買傾向建立模型。 有一種模式可識別現有消費者的服飾類別（例如女士/女士）或大小突然變化。 Sarah的購買行為改變表明，她不是在為自己購物。

<!-- ![image](assets/luma-gift.png) -->

### 定義區段

修改或建立代表似乎正在購買禮品之購物車放棄者的區段：

```sql
Profile: Category != Preferred Category 
AND 
Product Size != Preferred Size 
in last 7 days.  
AND 
Abandoned Cart 
AND 
Loyalty member 
```

<!-- ![image](assets/luma-abandon.png)-->

因為Sarah在購物車中新增了一個明顯的禮物專案並捨棄了，Luma可以使用免費的禮物包裝選件鎖定她。

## 目标

當您新增「放棄贈送禮品購物車」區段時，您可以大致檢視有多少人屬於此區段。 您可以對其採取動作，並使其可用於跨管道的個人化。

選取 **[!UICONTROL 傳送至目的地]**.

在Real-Time CDP中，Luma可順暢地對受眾區段進行個人化。\
我們在這裡看到Luma可將此目的地傳送至的所有目的地，包括Adobe和非Adobe解決方案：

![image](assets/luma-dest.png)

### 選取目的地

在此案例中，Luma想要跨以下目的地透過個人化重新鎖定此對象：

* Google，用於顯示

   <!--* Facebook -->
* Adobe Campaign，用於電子郵件

<!-- ![image](assets/luma-sched-dest.png) -->

### 正在排程目的地

您也可以排程區段在特定時間開始或結束。 區段將會在排程日期在設定的平台上發佈並自動更新。

>[!NOTE]
>
>（選擇性）如果您選取日期欄位，則會自動排程90天之後。

選取 **[!UICONTROL 儲存]** 前往下一頁。

當此對象中的客戶進行購買時，其對此對象的成員資格會即時隱藏。 他們不再符合資格，因為其狀態已變更。

這樣一來，Luma媒體團隊主管就不會對未合格的受眾使用清查資源，進而節省數十萬美元。

### 強制目的地的資料使用原則

Adobe Experience Platform包含隱私權與安全性控制項，用來判斷區段是否可啟動至特定目的地。 啟用是根據建立目的地時指派的行銷目的來啟用或限制，以及您的組織定義的資料使用原則。

如果您的活動違反原則，系統會顯示警告。 此警告包含資料譜系資訊，可協助您識別違反原則的原因，以及您可以如何解決違規。

有了這些控制項， [!DNL Experience Platform] 協助Luma以負責的方式遵守法規與市場。 這些控制具有彈性，可以修改以符合Luma安全和治理團隊的要求，讓他們能夠自信地滿足區域和組織管理已知和未知客戶資料的要求。

### 資料流程畫布

儲存後，視覺資料流程畫布會顯示從統一設定檔對應至您選取之三個目的地的區段。

![image](assets/luma-flow.png)

## 跨裝置身分識別拼接

Sarah在行動裝置上瀏覽社群媒體網站，且看到Luma廣告。 這讓她想起購物車中留下的物品。

稍後，她開啟電子郵件，並看到重新定位的電子郵件。 她從電子郵件中選取Luma連結。

此連結會將Sarah帶往Luma行動首頁，她在其中看到Adobe Target提供的高度個人化體驗。

* 她受到青銅會員的歡迎。
* 她看到「禮物」訊息。
* 她也會看到「免費贈品包裝」訊息，這是她銅牌會員資格權益的一部分。
* 根據她對於執行的喜好，主圖影像中仍會鎖定她。

她購買毛衣、增加禮物包裝，並寫禮品單。 她也可以選擇記住這個活動，並收到明年的提醒，以便在這個時候收到禮物。 她說是的，並排定在第二年進行電子郵件促銷活動，以提醒她購買其他禮物。

多虧了受眾抑制功能，Sarah的男士毛衣就不會成為目標。

## 分析設定檔

Luma行銷人員使用Adobe Experience Platform檢視Real-Time CDP儀表板上的贈送禮物區段。 他們檢視此行動方案隨時間推移的結果，並看到其成長。 客戶對優惠方案做出回應，並花費更多金錢。

這些見解讓行銷人員能針對此訊號採取行動，此訊號透過在CDP中取得此資料以及讓客戶（例如Sarah）附加至區段而強化。

Luma使用此CDP資料來提高忠誠度和客戶滿意度。
