---
title: 在使用者介面中建立SFTP來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立SFTP來源連線。
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# 建立 [!DNL SFTP] ui中的來源連線

本教學課程提供建立 [!DNL SFTP] 來源連線使用Adobe Experience Platform UI。

## 快速入门

本教學課程需要深入瞭解下列Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

>[!IMPORTANT]
>
>建議在使用擷取JSON物件時避免換行或歸位 [!DNL SFTP] 來源連線。 若要繞過此限制，請在每行使用單一JSON物件，並在後續檔案中使用多行。

如果您已有有效的 [!DNL SFTP] 連線時，您可以略過本檔案的其餘部分，並繼續進行上的教學課程 [設定資料流](../../dataflow/batch/cloud-storage.md).

### 收集必要的認證

為了連線到 [!DNL SFTP]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `host` | 與您的關聯的名稱或IP位址 [!DNL SFTP] 伺服器。 |
| `port` | 此 [!DNL SFTP] 您正在連線的伺服器連線埠。 如果未提供，值會預設為 `22`. |
| `username` | 您擁有存取許可權的使用者名稱 [!DNL SFTP] 伺服器。 |
| `password` | 您的密碼 [!DNL SFTP] 伺服器。 |
| `privateKeyContent` | Base64編碼的SSH私密金鑰內容。 OpenSSH金鑰型別必須分類為RSA或DSA。 |
| `passPhrase` | 如果金鑰檔案或金鑰內容受到密語保護，則用來解密私密金鑰的密語或密碼。 如果PrivateKeyContent受密碼保護，則此引數必須搭配PrivateKeyContent的密碼短語作為值使用。 |
| `maxConcurrentConnections` | 此引數可讓您指定Platform在連線至您的SFTP伺服器時將建立的同時連線數目上限。 您必須將此值設定為小於SFTP設定的限制。 **注意**：為現有SFTP帳戶啟用此設定時，只會影響未來的資料流，而不會影響現有的資料流。 |
| 文件夹路径 | 您要提供存取權的資料夾路徑。 [!DNL SFTP] 來源，您可以提供資料夾路徑，以指定使用者對所選子資料夾的存取權。 |

收集完所需的認證後，您可以依照下列步驟建立新的 [!DNL SFTP] 用於連線至Platform的帳戶。

## 連線至您的 [!DNL SFTP] 伺服器

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選取 **[!UICONTROL SFTP]** 然後選取 **[!UICONTROL 新增資料]**.

![已選取SFTP來源的Experience Platform來源目錄。](../../../../images/tutorials/create/sftp/catalog.png)

此 **[!UICONTROL 連線至SFTP]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的FTP或SFTP帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![Experience PlatformUI上的現有SFTP帳戶清單。](../../../../images/tutorials/create/sftp/existing.png)

### 新帳戶

>[!IMPORTANT]
>
>SFTP支援RSA或DSA型別的OpenSSH金鑰。 確定您的關鍵檔案內容開頭為 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` 結束於 `"-----END [RSA/DSA] PRIVATE KEY-----"`. 如果私密金鑰檔案是PPK格式檔案，請使用PuTTY工具從PPK轉換為OpenSSH格式。

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後為您的新提供名稱和說明（選用） [!DNL SFTP] 帳戶。

![SFTP的新帳戶畫面](../../../../images/tutorials/create/sftp/new.png)

此 [!DNL SFTP] 來源支援基本驗證和透過SSH公開金鑰的驗證。

>[!BEGINTABS]

>[!TAB 基本驗證]

若要使用基本驗證，請選取 **[!UICONTROL 密碼]** 然後提供要連線到的主機和連線埠值，以及您的使用者名稱和密碼。 在此步驟中，您也可以指定要提供存取權的子資料夾的路徑。 完成後，選取 **[!UICONTROL 連線到來源]**.

![使用基本驗證的SFTP來源的新帳戶畫面](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH公開金鑰驗證]

若要使用SSH公開金鑰型認證，請選取 **[!UICONTROL SSH公開金鑰]**  然後提供您的主機和連線埠值，以及您的私密金鑰內容和密碼組合。 在此步驟中，您也可以指定要提供存取權的子資料夾的路徑。 完成後，選取 **[!UICONTROL 連線到來源]**.

![使用SSH公開金鑰的SFTP來源的新帳戶畫面。](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## 后续步骤

依照本教學課程，您已建立與SFTP帳戶的連線。 您現在可以繼續下一節教學課程和 [設定資料流，將雲端儲存空間中的資料匯入Platform](../../dataflow/batch/cloud-storage.md).
