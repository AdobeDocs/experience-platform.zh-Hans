---
keywords: Experience Platform；首頁；熱門主題；Google雲端儲存空間；google雲端儲存空間
solution: Experience Platform
title: Google雲端儲存空間來源聯結器總覽
description: 瞭解如何使用API或使用者介面將Google Cloud Storage連線至Adobe Experience Platform。
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ae22e423119bf378a068349d481f0717a75171bb
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Google雲端儲存空間聯結器

Adobe Experience Platform為AWS等雲端服務供應商提供原生連線， [!DNL Google Cloud Platform]、和 [!DNL Azure]，可讓您從這些系統帶入資料。

雲端儲存空間來源可將您自己的資料帶入Platform，而不需要下載、格式化或上傳。 內嵌資料可以格式化為符合Experience Data Model (XDM)的JSON或Parquet，或以分隔格式提供。 流程的每個步驟都會整合至來源工作流程。 Platform可讓您從匯入資料 [!DNL Google Cloud Storage] 透過批次。

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 連線的必要條件設定 [!DNL Google Cloud Storage] 帳戶

若要連線至平台，您必須先啟用平台的互通性， [!DNL Google Cloud Storage] 帳戶。 若要存取互通性設定，請開啟 [!DNL Google Cloud Platform] 並選取 **[!UICONTROL 設定]** 從 **[!UICONTROL 雲端儲存空間]** 選項。

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

此 **[!UICONTROL 設定]** 頁面便會顯示。 從這裡，您可以檢視關於您的網站資訊， [!DNL Google] 專案ID和您的詳細資訊 [!DNL Google Cloud Storage] 帳戶。 若要存取互通性設定，請選取 **[!UICONTROL 互通性]** 從頂端標題。

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

此 **[!UICONTROL 互通性]** 頁面包含驗證、存取金鑰以及與您的服務帳戶相關聯的預設專案的資訊。 若要為您的服務帳戶產生新的存取金鑰ID和秘密存取金鑰，請選取 **[!UICONTROL 建立服務帳戶的金鑰]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

您可以使用新產生的存取金鑰ID和秘密存取金鑰來連線 [!DNL Google Cloud Storage] 至平台的帳戶。

如需詳細資訊，請閱讀 [建立和管理服務帳戶金鑰](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) 從 [!DNL Google Cloud] 說明檔案。

## 檔案和目錄的命名限制

以下是您在命名雲端儲存體檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許非法URL路徑字元。 程式碼點數類似 `\uE000`雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的相關規則，請參閱 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允許下列檔案名稱：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)，以及兩個點字元(...)。

## Connect [!DNL Google Cloud Storage] 至平台

以下檔案提供有關如何連線的資訊 [!DNL Google Cloud Storage] 使用API或使用者介面的to Platform：

### 使用API

- [使用Flow Service API建立Google Cloud Storage基本連線](../../tutorials/api/create/cloud-storage/google.md)
- [使用Flow Service API探索雲端儲存空間的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流量服務API為雲端儲存空間來源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Google雲端儲存空間來源連線](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中建立雲端儲存體連線的資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
