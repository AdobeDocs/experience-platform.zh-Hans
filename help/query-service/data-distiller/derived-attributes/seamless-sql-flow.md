---
title: 衍生屬性的無縫SQL流程
description: Query Service SQL已擴充為提供衍生屬性的緊密支援。 瞭解如何使用此SQL擴充功能建立針對設定檔啟用的衍生屬性，以及如何將屬性用於即時客戶設定檔和細分服務。
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 6202b1a5956da83691eeb5422d3ebe7f3fb7d974
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# 衍生屬性的無縫SQL流程

Query Service SQL已擴充為提供衍生屬性的緊密支援。 這為您Real-Time Customer Profile業務使用案例建立衍生屬性的有效替代方法。

本檔案概述各種方便使用的SQL擴充功能，這些擴充功能會產生衍生屬性，以與即時客戶設定檔搭配使用。 工作流程簡化了原本您必須透過各種API呼叫或Platform UI互動完成的程式。

通常，產生和發佈即時客戶個人檔案的屬性會涉及以下步驟：

* 建立身分名稱空間（如果尚未存在）。
* 如有必要，建立資料型別以儲存衍生屬性。
* 使用該資料型別建立欄位群組以儲存衍生的屬性資訊。
* 使用先前建立的名稱空間建立或指派主要身分資料行。
* 使用先前建立的欄位群組和資料型別建立結構描述。
* 使用您的結構描述建立新資料集，並視需要為設定檔啟用它。
* 選擇性地將資料集標示為已啟用設定檔。

完成上述步驟後，您就可以填入資料集。 如果您為設定檔啟用資料集，您也可以建立參照新屬性的區段，並開始產生深入分析。

「查詢服務」可讓您使用SQL查詢來執行上述所有動作。 這包括視需要變更資料集和欄位群組。

## 使用為設定檔啟用它的選項來建立表格 {#enable-dataset-for-profile}

>[!NOTE]
>
>下面提供的SQL查詢假設使用預先存在的名稱空間。

使用「建立表格為選取」(CTAS)查詢來建立資料集、指派資料型別、設定主要身分、建立結構描述，以及將其標籤為已啟用設定檔。 以下範例SQL陳述式會建立屬性，並讓它可用於即時客戶資料設定檔(Real-Time CDP)。 您的SQL查詢將遵循以下範例中顯示的格式：

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

支援的資料型別為：布林值、日期、日期時間、文字、浮點數、bigint、整數、對應、陣列和結構/列。

下列SQl程式碼區塊提供定義結構/列、對應和陣列資料型別的範例。 第一行示範列語法。 第二行示範對應語法，第三行示範陣列語法。

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

或者，也可以透過Platform UI為設定檔啟用資料集。 如需將資料集標示為已啟用設定檔的詳細資訊，請參閱 [啟用即時客戶個人檔案檔案的資料集](../../../catalog/datasets/user-guide.md#enable-profile).

在以下範例查詢中， `decile_table` 資料集建立方式 `id` 作為主要身分資料行，並具有名稱空間 `IDFA`. 它還有一個欄位，名為 `decile1Month` 對應資料型別的底層。 建立的表格(`decile_table`)已針對設定檔啟用。

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

成功執行查詢後，資料集ID會傳回至主控台，如下列範例所示。

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

使用 `label='PROFILE'` 於 `CREATE TABLE` 命令以建立啟用設定檔的資料集。 此 `upsert` 功能預設為開啟。 此 `upsert` 功能可使用以下專案覆寫： `ALTER` 命令，如下列範例所示。

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

請參閱SQl語法檔案，以瞭解如何使用 [變更表格](../../sql/syntax.md#alter-table) 命令和 [標籤做為CTAS查詢的一部分](../../sql/syntax.md#create-table-as-select).

## 協助透過SQL管理衍生屬性的建構

透過SQL管理衍生屬性時，以下說明的功能非常有用。

### 變更要針對設定檔啟用的現有資料集 {#enable-existing-dataset-for-profile}

ALTER TABLE SQL建構可用來讓現有的資料集為設定檔啟用。 這要求架構和對應的資料集都要新增已啟用設定檔的標籤。

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>成功執行 `ALTER TABLE` 命令，主控台會傳回 `ALTER SUCCESS`.

### 將主要身分新增至現有資料集 {#add-primary-identity}

將資料集中的現有欄標示為主要身分集，否則會導致錯誤。 若要使用SQL設定主要身分，請使用下面顯示的查詢格式。

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

例如：

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

在提供的範例中， `id2` 是中現有的欄 `test1_dataset`.

### 停用設定檔的資料集 {#disable-dataset-for-profile}

如果您想要針對設定檔用途停用表格，則必須使用DROP指令。 使用的SQL陳述式範例 `DROP` 如下所示。

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

例如：

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

此SQL陳述式提供使用API呼叫的有效替代方法。 如需詳細資訊，請參閱如何操作的檔案 [使用資料集API停用資料集以與Real-Time CDP搭配使用](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### 允許資料集的更新和插入功能 {#enable-upsert-functionality-for-dataset}

UPSERT指令可讓您插入新記錄或更新表格中的現有資料。 具體來說，如果表格中已存在指定的值，它可讓您更新現有列，或者如果指定的值尚未存在，則插入新列。

以下是使用正確格式的範例陳述式。

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

此SQL陳述式提供使用API呼叫的有效替代方法。 如需詳細資訊，請參閱如何操作的檔案 [啟用資料集，以搭配使用資料集API的Real-Time CDP和UPSERT使用](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### 停用資料集的更新和插入功能 {#disable-upsert-functionality-for-dataset}

此命令會停用更新資料集並將資料列插入資料集中的功能。

以下是使用正確格式的範例陳述式。

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### 顯示與每個表格關聯的其他表格資訊 {#show-labels-for-tables}

會為啟用設定檔的資料集保留其他中繼資料。 使用 `SHOW TABLES` 顯示額外內容的命令 `labels` 欄提供與表格相關聯之任何標籤的資訊。

此命令的輸出範例如下所示：

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

您可從範例中看出 `table_with_a_decile` 已為設定檔啟用並套用標籤，例如 [&#39;更新插入&#39;](#enable-upsert-functionality-for-dataset)， [&#39;設定檔&#39;](#enable-existing-dataset-for-profile) 如先前所述。

### 使用SQL建立欄位群組

現在可以透過使用SQL來建立欄位群組。 除了在Platform UI中使用結構描述編輯器，或向結構描述登入進行API呼叫以外，此功能提供了替代方法。

建立欄位群組的範例陳述式如下所示。

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>若發生下列情況，透過SQL建立欄位群組將會失敗： `label` 陳述式中未提供標幟，或欄位群組已存在。
>確保查詢包含 `IF NOT EXISTS` 子句以避免查詢失敗，因為欄位群組已存在。

真實世界的範例看起來可能類似於下面所示的範例。

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

成功執行此陳述式會傳回建立的欄位群組ID。 例如：`c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`。

請參閱檔案，瞭解如何 [在結構描述編輯器中建立新的欄位群組](../../../xdm/ui/resources/field-groups.md#create) 或使用 [結構描述登入API](../../../xdm/api/field-groups.md#create) 以取得替代方法的詳細資訊。

### 放置欄位群組

有時可能需要從結構描述登入中移除欄位群組。 這是透過執行 `DROP FIELDGROUP` 具有欄位群組ID的命令。

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

例如：

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>如果欄位群組不存在，則透過SQL刪除欄位群組將會失敗。 確定陳述式包含 `IF EXISTS` 子句以避免查詢失敗。

### 顯示表格的所有欄位群組名稱和ID

此 `SHOW FIELDGROUPS` command會傳回包含表格名稱、fieldgroupId和擁有者的表格。

此命令的輸出範例如下所示：

```sql
       name                      |        fieldgroupId                             |     owner      |
---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## 后续步骤

閱讀本檔案後，您對於如何使用SQL建立設定檔及根據衍生屬性啟用更新插入的資料集有了更深入的瞭解。 您現在已準備好將此資料集與批次擷取工作流程搭配使用，以更新您的設定檔資料。 若要進一步瞭解如何將資料擷取至Adobe Experience Platform，請先閱讀 [資料擷取概觀](../../../ingestion/home.md).
