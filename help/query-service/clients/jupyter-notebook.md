---
title: 將Jupyter Notebook連線至查詢服務
description: 瞭解如何連結Jupyter Notebook與Adobe Experience Platform查詢服務。
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Connect [!DNL Jupyter Notebook] 至查詢服務

本檔案說明連線所需的步驟 [!DNL Jupyter Notebook] 使用Adobe Experience Platform查詢服務。

## 快速入门

本指南要求您已擁有 [!DNL Jupyter Notebook] 並熟悉其介面。 若要下載 [!DNL Jupyter Notebook] 或如需詳細資訊，請參閱 [正式 [!DNL Jupyter Notebook] 檔案](https://jupyter.org/).

取得連線所需的認證 [!DNL Jupyter Notebook] 若要Experience Platform，您必須擁有 [!UICONTROL 查詢] Platform UI中的工作區。 如果您目前沒有「 」的存取權，請聯絡您的組織管理員 [!UICONTROL 查詢] 工作區。

>[!TIP]
>
>[!DNL Anaconda Navigator] 是桌上型圖形化使用者介面(GUI)，可讓您更輕鬆地安裝及啟動一般功能 [!DNL Python] 計畫，例如 [!DNL Jupyter Notebook]. 它還有助於在不使用命令列命令的情況下管理套件、環境和通道。
>請依照其網站上的引導式安裝程式，前往 [安裝您偏好的應用程式版本](https://docs.anaconda.com/anaconda/install/).
>從「蟒蛇導覽器」首頁畫面中選取 **[!DNL Jupyter Notebook]** 從支援的應用程式清單中啟動程式。
>如需詳細資訊，請參閱 [Anaconda官方檔案](https://docs.anaconda.com/anaconda/navigator/).

官方Jupyter檔案提供以下指示： [從命令列介面執行筆記本](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI)。

## Launch [!DNL Jupyter Notebook]

在您開啟新之後 [!DNL Jupyter Notebook] 網頁應用程式，選取 **[!DNL New]** UI中的下拉式清單，後面接著 **[!DNL Python 3]** 以建立新的Notebook。 此 [!DNL Notebook] 編輯器出現。

在 [!DNL Notebook] 編輯器中，輸入下列值： `pip install psycopg2-binary` 並選取 **[!DNL Run]** 命令列中的。 成功訊息會顯示在輸入行下方。

>[!IMPORTANT]
>
>在此過程中，您必須選取 **[!DNL Run]** 以執行每一行程式碼。

接下來，匯入 [!DNL PostgreSQL] 資料庫配接器 [!DNL Python]. 輸入值： `import psycopg2`並選取 **[!DNL Run]**. 此程式沒有成功訊息。 如果沒有錯誤訊息，請繼續進行下一個步驟。

您現在必須輸入值來提供您的Adobe Experience Platform認證： `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. 您的連線認證可在以下網址找到： [!UICONTROL 查詢] 區段，在 [!UICONTROL 認證] Platform UI的索引標籤。 請參閱檔案，瞭解如何 [尋找您的組織認證](../ui/credentials.md) 以取得詳細指示。

使用協力廠商使用者端時，建議使用不會到期的認證，以省下重複輸入詳細資料的工作。 如需相關指示，請參閱檔案 [如何產生和使用不會到期的認證](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>從Platform UI複製認證時，不需要其他認證格式。 它們可以在一行中指定，屬性和值之間有單一空格。 認證會以引號括住，且 **not** 以逗號分隔。

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

您的 [!DNL Jupyter Notebook] 執行個體現在已連線至查詢服務。

## 查詢執行範例

現在您已連線 [!DNL Jupyter Notebook] 若要查詢服務，您可以使用以下專案對資料集執行查詢： [!DNL Notebook] 輸入。 以下範例使用簡單查詢來示範此程式。

輸入下列值：

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

接下來，呼叫引數(`data` （在上述範例中），以未格式化的回應顯示查詢結果。

若要以更易懂的方式格式化結果，請使用下列命令：

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

這些命令不會產生成功訊息。 如果沒有錯誤訊息，您可以使用函式以表格格式輸出SQL查詢的結果。

輸入並執行 `df.head()` 函式以檢視清單化的查詢結果。

## 后续步骤

現在您已連線至查詢服務，您可以使用 [!DNL Jupyter Notebook] 以寫入查詢。 如需如何寫入和執行查詢的詳細資訊，請參閱 [running queries指南](../best-practices/writing-queries.md).
