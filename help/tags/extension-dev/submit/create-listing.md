---
title: 為擴充功能建立Exchange清單
description: 瞭解如何將擴充功能新增至Adobe Experience Platform中的公用目錄。
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: fcc586034317fb31122721fa9754b580c761a1da
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 24%

---

# 為擴充功能建立Exchange清單

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

Adobe Experience Platform有一個統一的目錄，使用者可以在其中檢視可用於安裝的標籤擴充功能。 此目錄可在產品中使用，並包含三種型別的擴充功能：

1. **公開擴充功能**：這些是專為任何使用者用於生產而設計的完整擴充功能。
1. **私人擴充功能**：這些是專為生產環境設計的完整擴充功能，但由貴公司中的其他使用者開發，僅供貴公司中的使用者使用。
1. **開發擴充功能**：這些擴充功能正在開發中，僅可在貴公司內使用，且僅適用於特別指定為開發屬性的屬性。

除了產品目錄中的擴充功能外，公開擴充功能也會在 [Experience CloudExchange應用程式市集](https://exchange.adobe.com/apps/browse/ec).

這些清單可讓擴充功能開發人員張貼功能說明、提供其他支援和檔案的連結，以及將擴充功能行銷給可能不知道您的公司或擴充功能之潛在使用者。 在此Marketplace中，您的擴充功能將有公開清單可供檢視，且使用者不需經過Platform驗證。 對於公開擴充功能，建立此Exchange清單是必要步驟。

>[!TIP]
>
>在發佈Exchange清單時，系統會自動將連結新增至清單內容，讓您的客戶和潛在客戶可以點選和 `Connect with publisher` 以取得有關您產品和服務的詳細資訊。 不會顯示您的連絡人電子郵件地址，因為這些訊息會由Exchange系統轉寄給您。

若沒有公司可上傳及測試您的擴充功能套件，您應註冊Exchange計畫並開始加入清單。 這將觸發公司帳戶的建立（需要一些時間，完成後，您會收到一封電子郵件），您可將其用於上傳和測試擴充功能。 同樣地，只有公開擴充功能才需要Exchange清單。

如果您已有公司帳戶，或您不需要Exchange清單（僅限私人副檔名），您可以略過此步驟的其餘部分，並繼續 [上傳和測試您的擴充功能](./upload-and-test.md).

## 创建列表

>[!NOTE]
>
>下列程式詳細說明如何在Adobe交換程式中建立應用程式清單。 這是用於Adobe Experience Platform中各種整合和擴充功能的術語。

![Experience Cloud應用程式管理員連結位置](../images/getting-started/app-mgr-link.png)

1. 登录到 [Exchange 合作伙伴网站](https://partners.adobe.com/exchangeprogram/experiencecloud)。登入後，選取 **應用程式管理員** 名稱旁的連結。
1. 選取 **建立新應用程式** 標籤，然後選取 **建立新應用程式** ，或選取適用的範本。
1. 提供列表信息。如需App Manager的詳細資訊，請參閱完整 [文章](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931). 清單資訊應清楚說明擴充功能的功用及其功用。 清單可作為您應用程式的行銷空間。 透過清楚的說明、網站登陸頁面的連結、說明檔案的連結或支援電子郵件地址等，在這裡推廣您的擴充功能。 雖然擴充功能檢視的空間有限，但Exchange清單仍提供機會，可同時推廣您的擴充功能和公司。 以下是改善擴充功能促銷的建議：
   - **應用程式圖示**  — 確認Exchange清單的圖示具有適當尺寸；png請使用512 x 512，jpg請使用1:1外觀比例。

      >[!NOTE]
      >
      >這與擴充功能程式碼中使用的檔案格式不同。 扩展本身将包含 svg 文件作为[图标](../manifest.md)。

   - **精選影像**  — 使用獨一無二、可彰顯品牌和應用程式的影像，吸引眾人目光。 「精選影像」是當有人分享您的Exchange清單連結或在社群媒體上發表相關文章時所顯示的影像。 因此，它必須是您品牌的模型表示法。
   - **应用程序发布者的徽标** - 这是您公司的徽标，请确保该图标具有适当的尺寸，即，1280 x 720 或 2560 x 1440 (16:9) 的 png 或 jpg 格式。
   - **設定指示**  — 告知客戶如何設定Adobe Experience Platform擴充功能。 請確定客戶瞭解您的網站或網站的 [設定檢視](../configuration.md) 在屬性中安裝您的擴充功能後，就會立即顯示。
   - **标记** - 在编辑列表的第一页，请确保在“自定义标记”字段中包含“Launch”一词。這會使您的清單顯示在Exchange Marketplace中的標籤搜尋中：
      ![](../images/getting-started/custom-tags.jpg)
   - **沙箱**  — 您需先透過沙箱帳戶存取Adobe解決方案，才能存取完整功能版本的Adobe Experience Platform。 您可以在创建应用程序列表时申请这些沙盒帐户。在 **連線** 區段選取您所建立的應用程式（您的標籤擴充功能）適用的特定連線，以及何時點選 **儲存**，就會視需要產生沙箱請求。
1. 提交您的清單。 Adobe Exchange 团队将审核您的应用程序，并在需要更新时向您提供反馈。如果您將 **立即發佈** 核取方塊提交清單時，會在核准後立即發佈。 如果您希望稍後再發佈應用程式，請取消勾選核取方塊。您的擴充功能清單獲得核准後，畫面會以藍色顯示 **發佈** 按鈕會顯示在應用程式（擴充功能）清單頁面上的旁邊。

### 创建有效列表

請檢視 [應用程式提交指引](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) 有關如何建立最吸引人的清單的詳細資訊。

#### 提交 Exchange 列表后

提交列表后，Adobe Exchange 团队会审核相关应用程序，审核结果要么是批准该应用程序，要么是提出更改意见。应用程序提交指南详细介绍了此过程。

如果您未登录过 Exchange 网站，请按照[计划注册指南](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html)中的说明，确保注册您的电子邮件地址以加入 Exchange 计划。每位使用者都必須將其電子郵件與公司的合作夥伴帳戶建立關聯。 您可以透過電子郵件將此程式的問題導向至 <ExchangeHelpEC@adobe.com>.

#### 在获得初步批准后更新您的 Exchange 列表

当您更新扩展或者只是需要更新 Exchange 列表时，请登录到[合作伙伴门户](https://partners.adobe.com/exchangeprogram/experiencecloud)，然后选择您姓名旁边的“应用程序管理器”按钮。接下来，选择您的应用程序，并按照上面介绍的最初用于创建列表的流程来执行操作。重新提交后，Adobe Exchange 团队会审核更改情况，并将批准更改，或对更改情况提出意见。

## 將擴充功能套件連結至清單

您的清單獲得核准並公開使用後，我們建議您提供中公開清單的連結 `exchange_url` 的欄位 `extension.json` 副檔名套件中的檔案。  這會在標籤擴充功能目錄中建立「更多資訊」連結，以便產品內的使用者可以找到您的清單及其額外資訊。
