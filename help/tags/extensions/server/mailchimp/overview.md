---
title: Mailchimp擴充功能概觀
description: 使用事件轉送來觸發Mailchimp電子郵件。
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 5%

---

# Mailchimp事件轉送擴充功能概觀

>[!NOTE]
>  
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

Mailchimp [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能會將事件傳送至Mailchimp Marketing API，而該API可觸發Mailchimp行銷活動、歷程或交易的電子郵件。

本文介紹如何使用「新增事件」動作來設定擴充功能及設定規則。

## 先决条件

本檔案假設您熟悉擴充功能所使用的相關Mailchimp產品。 如需詳細資訊，請參閱Mailchimp說明檔案 [行銷活動](https://mailchimp.com/help/getting-started-with-campaigns/)， [歷程](https://mailchimp.com/help/about-customer-journeys/)、和 [交易](https://mailchimp.com/help/transactional/).

使用此擴充功能需要Mailchimp帳戶。 您可以註冊帳戶 [此處](https://login.mailchimp.com/signup/). 在Mailchimp帳戶儀表板中，記下以下值以用於本指南：

- 您的Mailchimp網域前置詞
- 您的API金鑰
- 對象ID
- 預設的「寄件者」電子郵件地址

根據您的Mailchimp帳戶計畫，您對Mailchimp客戶歷程工具的存取權可能會受到限制。

>[!TIP]
>  
>如果您使用Mailchimp自動化，例如交易電子郵件或客戶歷程，步驟和畫面可能會稍有不同，此處列出。 不過，使用此擴充功能仍需上述相同資訊。 請參閱 [Mailchimp說明中心](https://mailchimp.com/help/) 以取得您特定帳戶與計畫的每個值的詳細資訊。

### 網域前置詞

登入Mailchimp並登入控制面板檢視後，瀏覽器的位址列應會顯示URL，例如 `https://us11.admin.mailchimp.com` 或只是 `us11.admin.mailchimp.com`. 在此範例中，前置詞 `us11` 只是預留位置，您的值將會不同。 將您的URL和前置詞記錄下來，以供稍後步驟使用。

### API金鑰

若要尋找您帳戶的API金鑰，請在Mailchimp UI中選取您的設定檔圖示，然後選取 **設定檔**. 您應會看到URL，例如 `https://us11.admin.mailchimp.com/account/profile/` 但使用 **您的** 首碼而非 `us11`.

選取 **額外專案**，則 **API金鑰**：

![額外功能表、API金鑰連結](../../../images/extensions/server/mailchimp/menu-API-keys.png)

下 **您的API金鑰**，您可以選擇現有金鑰，或選取 **建立金鑰** 以建立新檔案。 您可以建立新金鑰以專門用於此擴充功能。 複製API金鑰並儲存以供稍後步驟使用。 如需詳細資訊，請參閱Mailchimp檔案以瞭解如何 [產生您的API金鑰](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### 對象ID和寄件者地址

選取 **對象** 在左側導覽中，然後 **受眾控制面板**. 接著，選取您要搭配此擴充功能使用的對象。 若要深入瞭解，請參閱Mailchimp檔案，網址為 [建立對象](https://mailchimp.com/help/create-audience/).

建立並選取您的對象後，選取 **管理對象** 下拉式清單並選擇 **設定**. 此畫面會顯示您對象的各種設定。

在「設定」畫面底部，您應該會看到 `Unique id for audience [audience name]` 位置 `[audience name]` 是您實際對象的名稱。 複製對象ID並儲存以供稍後步驟使用。

選取 **對象名稱和預設值** 並確認 **預設寄件者電子郵件地址** 具有行銷活動的正確值。 請注意，此頁面頂端也會列出Audience ID，與您在上一步中向下複製的值相同。

## Mailchimp自動化

根據您的Mailchimp計畫以及您使用交易式電子郵件、客戶歷程或其他Mailchimp自動化，您的特定歷程設定可能會有所不同。

>[!IMPORTANT]
>  
>您選擇用來在Mailchimp中觸發自動化或歷程的事件名稱，與您必須使用此擴充功能傳送的事件名稱相同。 記下Mailchimp自動化中的事件名稱，並將其儲存以供稍後步驟使用。

## 安装和配置

本節列出安裝及設定擴充功能的步驟。 若要安全地儲存Mailchimp API金鑰，您必須使用事件轉送 [秘密](../../../ui/event-forwarding/secrets.md).

### 建立密碼和資料元素

在事件轉送屬性中， [建立 [!UICONTROL Token] 密碼](../../../ui/event-forwarding/secrets.md#token) 已呼叫 `Mailchimp API Key`.

下一個， [建立資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 使用 [!UICONTROL 核心] 擴充功能和 [!UICONTROL 密碼] 資料元素型別以參照 `Mailchimp API Key` 您剛才建立的密碼。 輸入 `Mailchimp Token` 做為資料元素名稱。

### 安装和配置 扩展

在相同的事件轉送屬性中，選取 **[!UICONTROL 擴充功能]，** 則 **[!UICONTROL 目錄]** 以顯示可供安裝的擴充功能。 從這裡，搜尋Mailchimp擴充功能並選取 **[!UICONTROL 安裝]**.

![安裝Mailchimp擴充功能](../../../images/extensions/server/mailchimp/install.png)

設定畫面隨即顯示。 下 **[!UICONTROL Mailchimp伺服器首碼網域名稱]**，請輸入您先前從Mailchimp帳戶複製的網域，包括唯一的網域首碼。

>[!IMPORTANT]
>
>不包括 `http://` 或 `https://` 在此欄位中。

![扩展配置](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

下 **[!UICONTROL Mailchimp權杖]**，選取資料元素圖示，然後選擇 `Mailchimp Token` 您先前建立的資料元素。 選取 **[!UICONTROL 儲存]** 以儲存變更。

擴充功能現已安裝並設定為可在您的屬性中使用。

## 資料彙集

在中使用此擴充功能時 [規則](../../../ui/managing-resources/rules.md)，擴充功能會隨著每個事件傳送數個資料值至Mailchimp。 對於一般實作，您可以設定 [Adobe Experience Platform Web SDK擴充功能](../../client/sdk/overview.md) 以傳送該資料至 [!DNL Platform Edge Network] 供擴充功能在事件轉送屬性中使用。

此擴充功能所需的資料可以作為XDM資料或非XDM資料從Web SDK傳送。 請參閱檔案以深入瞭解 [傳送XDM資料](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

例如，如果客戶購買產品，或在您的網站上註冊了事件，您可以使用此擴充功能透過Mailchimp傳送確認電子郵件。 從Web SDK傳送所需資訊至Edge Network後，擴充功能會透過Mailchimp觸發電子郵件。

![新增事件動作設定](../../../images/extensions/server/mailchimp/action-configurations.png)

### 数据元素

上一節中的熒幕擷圖顯示您可以與此擴充功能中每個事件一起傳送至Mailchimp的資料。 設定Web SDK以將此資料傳送至Edge Network後，您可以在事件轉送屬性中建立資料元素，讓擴充功能可存取這些值。

下表提供每個可能值的詳細資訊。

| 名称 | 範例路徑 | 类型 | 描述 | 必需 | 限制 |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> 或<br /> `arc.event.data._tenant.emailId` | 字符串 | 接收電子郵件的地址 | **是** | 必須存在於Mailchimp對象中 |
| `listId` | `arc.event.xdm._tenant.listId`<br /> 或<br /> `arc.event.data._tenant.listid` | 字符串 | 對象ID | **是** | 必須符合現有的對象ID |
| `name` | `arc.event.xdm._tenant.name`<br /> 或<br /> `arc.event.data._tenant.name` | 字符串 | 事件名稱 | **是** | 2-30個字元長 |
| `properties` | `arc.event.xdm._tenant.properties`<br /> 或<br /> `arc.event.data._tenant.properties` | 对象 | JSON格式的可選屬性清單，包含有關事件的詳細資訊 | 否 |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> 或<br /> `arc.event.data._tenant.isSyncing` | 布尔 | 建立事件 `is_syncing` 設定為 `true` **不會** 觸發自動化 | 否 |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> 或 `arc.event.data._tenant.occuredAt` | 字符串 | 事件發生時的ISO 8601時間戳記 | 否 |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>此 **範例路徑** 上述值僅為範例。 欄位名稱和 [路徑](../../../ui/event-forwarding/overview.md#data-element-path) 這些資料元素中參照的元素在屬性中可能會有所不同，具體取決於您在上述步驟中命名和設定Web SDK的方式。

在事件轉送屬性中，您可以為上述每個欄位建立資料元素。 建立後，您可以參照 [!UICONTROL 新增事件] 此擴充功能的動作。

![新增事件動作設定](../../../images/extensions/server/mailchimp/action-configurations.png)

您現在可以使用此擴充功能和「新增事件」動作，為您的對象觸發Mailchimp電子郵件。

## 資料驗證

使用事件轉送擴充功能時， [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 非常有用。 在「記錄」區段的「邊緣記錄」下方，您可以檢視事件轉送規則觸發後所提出的請求。 下列熒幕擷取畫面顯示擴充功能向Mailchimp API提出的請求。

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

在Mailchimp控制面板中，您的「對象」或「對象成員」的「活動摘要」檢視上，會提供該「對象」或「對象成員」的事件清單。 這應該會比對擴充功能傳送的事件，並顯示任何傳送的可選資料，以及他們收到的電子郵件或促銷活動。 請參閱 [Mailchimp自動化說明指南](https://mailchimp.com/help/automation/) 以取得更多詳細資料。
