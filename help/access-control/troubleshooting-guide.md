---
keywords: Experience Platform；首頁；熱門主題；疑難排解；存取控制
solution: Experience Platform
title: 存取控制疑難排解指南
description: 本檔案提供Adobe Experience Platform存取控制常見問題的解答。
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# 存取控制疑難排解指南

本檔案提供Adobe Experience Platform存取控制常見問題的解答。 關於其他相關問題和疑難排解 [!DNL Platform] 服務，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

[!DNL Experience Platform] 可運用中的產品設定檔 [Adobe Admin Console](https://adminconsole.adobe.com) 若要提供角色型存取控制，請將使用者與許可權和沙箱連結。  請參閱 [存取控制總覽](home.md) 以取得詳細資訊。

## 我可以在哪裡找到目前的存取許可權？

如果您是組織的系統管理員、產品管理員或產品設定檔管理員，則可以在Adobe Admin Console中檢視指派的產品設定檔及其提供的許可權。 請參閱 [存取控制使用手冊](./ui/overview.md) 以取得如何導覽 [!DNL Admin Console] 以檢視產品設定檔的許可權。

如果您不是管理員，您仍然可以透過傳送請求至 `/acl/effective-policies` 存取控制API中的端點。 請參閱下列「檢視有效原則」一節： [存取控制開發人員指南](./api/effective-policies.md) 以取得詳細資訊。

## 中的部分功能 [!DNL Platform] UI無法使用。 這些功能的存取權如何由許可權控制？

如果您沒有特定專案的存取許可權 [!DNL Platform] 功能，則會在以下位置隱藏或顯示為灰色： [!DNL Experience Platform] UI。 例如，若要檢視「[!UICONTROL 設定檔]「索引標籤，您必須擁有」[!UICONTROL 檢視設定檔]「或」[!UICONTROL 管理設定檔]」許可權。 如果您需要其他許可權，請聯絡管理員： [!DNL Experience Platform] 功能。

## 許可權如何分組，哪個群組包含我想使用的許可權？

許可權會依以下專案進行分組和分類： [!DNL Platform] 套用的功能(例如 [!DNL Data Management] 和 [!DNL Profile Management])。 如需可用許可權及其所屬群組的完整清單，請參閱 [許可權區段](home.md#permissions) 在存取控制概觀中。

請參閱 [存取控制總覽](home.md) 有關提供角色型存取控制的詳細資訊。

## 從AdobeIO移轉至Business ID後，許可權會發生什麼事？

存取控制使用使用者ID （指派給使用者的內部唯一ID）來授予許可權。 當組織從Adobe ID移轉至Business ID時，為其使用者設定的所有許可權都將遺失，因為使用者ID變更，且存取控制將使用新產生的使用者ID。 如果您的組織移轉至Business ID，請聯絡您的Adobe代表，以將您的使用者ID從Adobe ID移轉至Business ID。
