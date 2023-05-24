---
title: 使用Python和SQLAlchemy管理平台資料
description: 瞭解如何使用SQLAlchemy來使用Python而非SQL管理您的平台資料。
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 管理Platform資料，使用 [!DNL Python] 和 [!DNL SQLAlchemy]

瞭解如何使用SQLAlchemy以更靈活地管理Adobe Experience Platform資料。 對於不熟悉SQL的人來說，SQLAlchemy可以在使用關聯式資料庫時大幅縮短開發時間。 本檔案提供連線的指示和範例 [!DNL SQLAlchemy] 查詢服務並開始使用Python與資料庫互動。

[!DNL SQLAlchemy] 是物件關聯對應程式(ORM)和 [!DNL Python] 程式碼程式庫，可將儲存在SQL資料庫中的資料傳輸至 [!DNL Python] 物件。 接著，您就可以使用對Platform Data Lake中保留的資料執行CRUD作業 [!DNL Python] 程式碼。 如此一來，您就不需要只使用PSQL來管理資料。

## 快速入门

取得連線所需的認證 [!DNL SQLAlchemy] 若要Experience Platform，您必須擁有平台UI中查詢工作區的存取權。 如果您目前無法存取查詢工作區，請聯絡您的組織管理員。

## [!DNL Query Service] 認證 {#credentials}

若要尋找您的認證，請登入Platform UI並選取 **[!UICONTROL 查詢]** 從左側導覽，然後是 **[!UICONTROL 認證]**. 如需如何尋找登入憑證的完整指示，請參閱 [認證指南](../ui/credentials.md).

![「認證」索引標籤中反白顯示「查詢服務」的到期認證。](../images/use-cases/credentials.png)

雖然連線埠80是連線查詢服務的建議連線埠，但您也可以使用連線埠5432。

>[!IMPORTANT]
>
>如果您使用即將到期的認證（如上圖所示）來連線至查詢服務，則連線的工作階段期限會在貴組織的設定中定義的設定時段後到期。 依預設，此期間為24小時。 請參閱檔案以瞭解如何 [使用不會到期的認證連線使用者端](../ui/credentials.md#non-expiring-credentials)，或如何 [變更您即將到期認證的工作階段期限](../ui/credentials.md#expiring-credentials).

存取您的QS憑證後，請開啟 [!DNL Python] 所選編輯器。

### 將認證儲存在 [!DNL Python] {#store-credentials}

在您的 [!DNL Python] 編輯者，匯入 `urllib.parse.quote` 程式庫，並將每個認證變數儲存為引數。 此 `urllib.parse` 模組提供標準介面，可將URL字串分成元件。 quote函式會取代URL字串中的特殊字元，讓資料可以安全地用作URL元件。 以下是必要程式碼的範例：

>[!TIP]
>
>使用 [!DNL Python]的三引號來輸入您的多行密碼字串。

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>您提供用來連線的密碼 [!DNL SQLAlchemy] 若您使用即將到期的認證，則「 」的「 」Experience Platform將會到期。 請參閱 [證明資料段落](#credentials) 以取得詳細資訊。

### 建立引擎執行個體 [#create-engine]

建立變數後，匯入 `create_engine` 函式並建立字串，以編譯及格式化SQLAlchemy中的查詢服務認證。 此 `create_engine` 然後使用函式來建構引擎執行個體。

>[!NOTE]
>
>`create_engine`傳回引擎的執行個體。 但是，它直到呼叫需要連線的查詢時才會開啟與查詢服務的連線。

使用協力廠商使用者端存取Platform時，必須啟用SSL。 在引擎中，使用 `connect_args` 以輸入其他關鍵字引數。 建議您將SSL模式設定為 `require`. 請參閱 [SSL模式檔案](../clients/ssl-modes.md) 以取得接受值的詳細資訊。

以下範例顯示 [!DNL Python] 初始化引擎和連線字串所需的程式碼。

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>您提供用來連線的密碼 [!DNL SQLAlchemy] 若您使用即將到期的認證，則「 」的「 」Experience Platform將會到期。 請參閱 [證明資料段落](#credentials) 以取得詳細資訊。

您現在可以使用查詢Platform資料 [!DNL Python]. 下列範例會傳回查詢服務資料表名稱的陣列。

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
