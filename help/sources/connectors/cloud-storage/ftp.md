---
keywords: Experience Platform；首頁；熱門主題；FTP；ftp；
solution: Experience Platform
title: FTP來源聯結器概述
description: 瞭解如何使用API或使用者介面將FTP伺服器連線到Adobe Experience Platform。
exl-id: a6186fad-8a7b-4103-80c7-a522ff69fe9e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# (Beta) FTP聯結器

>[!NOTE]
>
>FTP聯結器為Beta版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

Adobe Experience Platform為AWS等雲端服務供應商提供原生連線， [!DNL Google Cloud Platform]、和 [!DNL Azure]，可讓您從這些系統帶入資料。

雲端儲存空間來源可將您自己的資料帶入 [!DNL Platform] 而不需要下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會整合至來源工作流程。 [!DNL Platform] 可讓您透過批次從FTP或SFTP伺服器匯入資料。

>[!IMPORTANT]
>
>使用FTP來源聯結器建立資料流時，由於在FTP伺服器內遇到累加更新的延遲問題，強烈建議設定一次性擷取排程。

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 檔案和目錄的命名限制

以下是您在命名雲端儲存體檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許非法URL路徑字元。 程式碼點數類似 `\uE000`雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的相關規則，請參閱 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允許下列檔案名稱：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)，以及兩個點字元(...)。

## 將FTP連線至 [!DNL Platform]

以下檔案提供如何將FTP伺服器連線至的相關資訊 [!DNL Platform] 使用API或使用者介面：

### 使用API

- [使用流量服務API建立FTP基本連線](../../tutorials/api/create/cloud-storage/ftp.md)
- [使用Flow Service API探索雲端儲存空間的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流量服務API為雲端儲存空間來源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在使用者介面中建立FTP來源連線](../../tutorials/ui/create/cloud-storage/ftp.md)
- [在UI中建立雲端儲存體連線的資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
