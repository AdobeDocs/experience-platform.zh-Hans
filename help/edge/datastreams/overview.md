---
title: 資料串流概觀
description: 将客户端 Experience Platform SDK 集成与 Adobe 产品和第三方目标连接起来。
keywords: 設定；資料串流；資料串流Id；邊緣；資料串流ID；環境設定；edgeConfigId；身分；ID同步已啟用；ID同步容器ID；沙箱；串流入口；事件資料集；目標；使用者端代碼；屬性代號；目標環境ID；Cookie目的地；URL目的地；Analytics設定區塊報表套裝ID；資料收集的資料準備；資料準備；對應程式；XDM對應程式；Edge上的對應程式；
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 4%

---

# 資料串流概觀

数据流表示实施 Adobe Experience Platform Web 和移动 SDK 时的服务器端配置。而 [configure命令](../fundamentals/configuring-the-sdk.md) 在SDK中控制使用者端上必須處理的專案(例如 `edgeDomain`)，資料串流會處理SDK的所有其他設定。 當請求傳送至Adobe Experience Platform Edge Network時， `edgeConfigId` 用於參考資料流。 這可讓您更新伺服器端設定，而不需在網站上變更程式碼。

您可以選取「 」，建立和管理資料串流 **[!UICONTROL 資料串流]** (位於Adobe Experience Platform UI或資料收集UI的左側導覽器中)。

![UI中的資料串流索引標籤](../assets/datastreams/overview/datastreams-tab.png)

如需如何在UI中設定資料流的詳細資訊，請參閱 [設定指南](./configure.md).

## 處理資料串流中的敏感資料 {#sensitive}

>[!IMPORTANT]
>
>本檔案的內容不是法律建議，且用意並非要取代法律建議。 請洽詢貴公司的法律部門，以取得處理敏感資料的建議。

公司資料管理政策和法規要求對於如何收集、處理和使用敏感客戶資料日益加諸限制。 這包括受保護的健康資料(PHI)的收集、處理及使用，此資料須受健康保險便利與責任法案(HIPAA)等法規的約束。

資料串流提供三種方法來協助您安全地處理敏感資料：

* [增強型加密](#encryption)
* [資料控管](#governance)
* [审核日志](#audit-logs)

### 增強型加密 {#encryption}

所有透過Edge Network傳輸中的資料，都是透過以下方式透過安全、加密的連線執行： [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). 如果資料串流將資料帶入Experience Platform，則資料會在Experience Platform資料湖中靜態加密。 檢視檔案： [Experience Platform中的資料加密](../../landing/governance-privacy-security/encryption.md) 以取得詳細資訊。

### 資料控管 {#governance}

資料串流運用Experience Platform的內建資料控管功能，防止將敏感資料傳送至不符合HIPAA標準的服務。 藉由標籤資料流結構描述中包含敏感資料的特定欄位，您可以精細地控制哪些資料欄位可用於特定目的。

以下影片簡要概述如何在UI中設定及強制執行資料串流的資料使用限制：

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

在Experience Platform中，您可以套用 [敏感資料使用標籤](../../data-governance/labels/reference.md#sensitive) 至包含貴組織視為敏感資料的結構描述和欄位。 例如， `RHD` 標籤用來表示受保護的健康資訊(PHI)，以及 `S1` 標籤代表地理位置資料。

>[!NOTE]
>
>如需如何套用資料使用標籤內的詳細資訊， [!UICONTROL 結構描述] 索引標籤在Experience PlatformUI或資料收集UI中，請參閱 [結構描述標籤教學課程](../../xdm/tutorials/labels.md).

建立新資料流時，如果選取的結構描述包含敏感資料使用標籤，則資料流只能設定為將該資料傳送至符合HIPAA要求的目的地。 目前，資料串流唯一支援的HIPAA就緒目的地是Adobe Experience Platform。 其他目的地服務(包括Adobe Target、Adobe Analytics、Adobe Audience Manager、事件轉送和Edge目的地)會針對包含敏感資料使用標籤的資料串流停用。

如果結構描述正在具有非HIPAA就緒服務的現有資料流中使用，嘗試將敏感資料使用標籤新增到結構描述會導致違反原則訊息，並阻止此操作。 此訊息會指定哪個資料流觸發違規，並建議從資料流中移除任何非HIPAA就緒的服務以解決問題。

### 审核日志

在Experience Platform中，可以稽核日誌的形式監控資料流活動。 稽核記錄會告知 **誰** 已執行 **什麼** 動作，以及 **時間**，以及其他能協助您疑難排解資料串流相關問題的內容資料，以協助您的企業遵守公司資料管理原則和法規要求。

每當使用者建立、更新或刪除資料流時，就會建立稽核記錄檔來記錄動作。 每當使用者透過建立、更新或刪除對應時，也會發生相同情況 [資料收集的資料準備](./data-prep.md). 無論更新為資料流還是對應，產生的稽核記錄都會分類在 [!UICONTROL 資料串流] 資源型別。

請參閱以下說明檔案： [稽核記錄](../../landing/governance-privacy-security/audit-logs/overview.md) 有關如何解譯資料串流和其他支援之服務的記錄檔的詳細資訊。

## 后续步骤

本指南提供資料串流及其在資料收集和處理敏感資料中的使用情形的整體概觀。 如需如何設定新資料流的步驟，請參閱 [資料流設定指南](./configure.md).
