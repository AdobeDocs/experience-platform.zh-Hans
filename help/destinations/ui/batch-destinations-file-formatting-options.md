---
description: 瞭解在啟用以檔案為基礎的目的地資料時，如何設定檔案格式選項
title: （測試版）設定檔案型目的地的檔案格式選項
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: b1e9b781f3b78a22b8b977fe08712d2926254e8c
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 19%

---

# （測試版）設定檔案型目的地的檔案格式選項

>[!IMPORTANT]
>
>此 **[!UICONTROL 檔案格式選項]** Adobe Experience Platform中的功能目前為Beta版。 檔案和功能可能會有所變更。
>請聯絡您的Adobe代表以取得此功能的存取權。
> 
>本檔案中說明的檔案格式選專案前僅適用於CSV檔案。

當您使用時，可以使用選項為匯出的檔案設定各種檔案格式選項 [connect](/help/destinations/ui/connect-destination.md) 至檔案型目的地，例如 [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect)， [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)，或 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

您可以使用Experience PlatformUI為匯出的檔案設定各種檔案格式選項。 您可以修改匯出檔案的多個屬性，以符合您這邊檔案接收系統的需求，以便以最佳方式讀取和解譯從Experience Platform接收的檔案。

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## CSV檔案的檔案格式設定 {#file-configuration}

若要顯示檔案格式選項，請啟動 [連線到目的地](/help/destinations/ui/connect-destination.md) 工作流程。 選取 **資料型別：區段** 和 **檔案型別： CSV** 顯示可用於匯出的檔案格式設定 `CSV` 檔案。

>[!IMPORTANT]
>
>您連線的目的地可能沒有所有這些可用選項。 由目的地開發人員決定他們要在目的地支援哪些檔案格式選項。 目的地開發人員可決定連線至目的地時可用的選項。 在Experience PlatformUI中，必要選項會以星號標示。
> 
>新的雲端儲存空間目的地 —  [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)， [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md)， [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md)， [(Beta)資料登陸區域](/help/destinations/catalog/cloud-storage/data-landing-zone.md)， [(Beta) Google雲端儲存空間](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)， [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md)  — 目前僅支援下面醒目提示的六個CSV選項。

![顯示部分可用檔案格式選項的影像。](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### 分隔符 {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="分隔符"
>abstract="使用此控件为每个字段和值设置分隔符。查看每个选择的示例文档。"

使用此控制項為匯出的CSV檔案中的每個欄位和值設定分隔符號。 可用选项包括：

* 冒号 `(:)`
* 逗号 `(,)`
* 竖线 `(|)`
* 分号 `(;)`
* Tab `(\t)`

#### 示例

檢視以下匯出的CSV檔案中的內容範例，其中包含UI中的每個選項。

* 範例輸出為 **[!UICONTROL 冒號`(:)`]** 已選取： `male:John:Doe`
* 範例輸出為 **[!UICONTROL 逗號`(,)`]** 已選取： `male,John,Doe`
* 範例輸出為 **[!UICONTROL 垂直號`(|)`]** 已選取： `male|John|Doe`
* 範例輸出為 **[!UICONTROL 分號`(;)`]** 已選取： `male;John;Doe`
* 範例輸出為 **[!UICONTROL 標籤`(\t)`]** 已選取： `male \t John \t Doe`

### 引号字符 {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="引号字符"
>abstract="如果要从导出的字符串中删除双引号，请使用此选项。查看每个选择的示例文档。"

如果要从导出的字符串中删除双引号，请使用此选项。可用选项包括：

* **[!UICONTROL Null字元(\0000)]**. 使用此選項可從匯出的CSV檔案中移除雙引號。
* **[!UICONTROL 雙引號(&quot;)]**. 使用此選項可在匯出的CSV檔案中保留雙引號。

#### 示例

檢視以下匯出的CSV檔案中內容的範例，其中包含UI中的每個選項。

* 範例輸出為 **[!UICONTROL Null字元(\0000)]** 已選取： `Test,John,LastName`
* 範例輸出為 **[!UICONTROL 雙引號(&quot;)]** 已選取： `"Test","John","LastName"`

### 转义字符 {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="转义字符"
>abstract="设置一个用于在已被引号引起的值中将引号转义的字符。查看每个选择的示例文档。"

使用此選項可設定在已引號值內逸出引號的單一字元。 例如，當字串包含在雙引號中時，此選項非常有用，因為部分字串已包含在雙引號中。 此選項會決定要用哪個字元來取代內部雙引號。 可用选项包括：

* 反斜線 `(\)`
* 單引號 `(')`

#### 示例

檢視以下匯出的CSV檔案中內容的範例，其中包含UI中的每個選項。

* 範例輸出為 **[!UICONTROL 反斜線`(\)`]** 已選取： `"Test,\"John\",LastName"`
* 範例輸出為 **[!UICONTROL 單引號`(')`]** 已選取： `"Test,'"John'",LastName"`

### 空值输出 {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="空值输出"
>abstract="使用此选项设置应如何在导出的 CSV 文件中表示空值。查看每个选择的示例文档。"

使用此控制項可設定空值的字串表示法。 此選項會決定空值在匯出的CSV檔案中的表示方式。 可用选项包括：

* **[!UICONTROL null]**
* **&quot;&quot;**
* **[!UICONTROL 空字串]**

#### 示例

檢視以下匯出的CSV檔案中內容的範例，其中包含UI中的每個選項。

* 範例輸出為 **[!UICONTROL null]** 已選取： `male,NULL,TestLastName`. 在此案例中，Experience Platform會將空值轉換為null值。
* 範例輸出為 **&quot;&quot;** 已選取： `male,"",TestLastName`. 在此案例中，Experience Platform會將空白值轉換為雙引號。
* 範例輸出為 **[!UICONTROL 空字串]** 已選取： `male,,TestLastName`. 在此情況下，Experience Platform會維護空白值並依原樣匯出（不含雙引號）。

>[!TIP]
>
>以下區段中的空白值輸出與null值輸出之間的差異在於空白值具有空白的實際值。 NULL值沒有任何值。 將空白值視為表格上的空白玻璃，將null值視為表格上沒有任何玻璃。

### null 值输出 {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="null 值输出"
>abstract="使用此选项设置应如何在导出的文件中表示 null 值。查看每个选择的示例文档。"

使用此选项设置应如何在导出的文件中表示 null 值。此選項會決定Null值在匯出的CSV檔案中的表示方式。 可用选项包括：

* **[!UICONTROL null]**
* **&quot;&quot;**
* **[!UICONTROL 空字串]**

#### 示例

檢視以下匯出的CSV檔案中內容的範例，其中包含UI中的每個選項。

* 範例輸出為 **[!UICONTROL null]** 已選取： `male,NULL,TestLastName`. 在此情況下，不會發生轉換，且CSV檔案包含null值。
* 範例輸出為 **&quot;&quot;** 已選取： `male,"",TestLastName`. 在此案例中，Experience Platform會在空字串周圍以雙引號取代null值。
* 範例輸出為 **[!UICONTROL 空字串]** 已選取： `male,,TestLastName`. 在這種情況下，Experience Platform會以空字串取代null值（不含雙引號）。

### 压缩格式 {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="压缩格式"
>abstract="设置在将数据保存到文件时要使用何种压缩类型。支持的选项为 GZIP 和 NONE。查看每个选择的示例文档。"

设置在将数据保存到文件时要使用何种压缩类型。支持的选项为 GZIP 和 NONE。此選項會決定您是否要匯出壓縮檔案。

### 编码

*未顯示在UI熒幕擷圖中*. 指定已儲存CSV檔案的編碼（字元集）。 選項為UTF-8或UTF-16。

### 用於逸出引號的字元

*未顯示在UI熒幕擷圖中*. 此旗標可指出是否應該將包含引號的值一律括在引號中。

預設為逸出包含引號字元的所有值。

### 行分隔符號

*未顯示在UI熒幕擷圖中*. 定義用於書寫的線段分隔符號。 長度上限為1個字元。

### 忽略開頭空格

*未顯示在UI熒幕擷圖中*. 指出是否應該略過匯出值前導空白的旗標。

範例輸出為 **[!UICONTROL True]** 已選取： `"male","John","TestLastName"`
範例輸出為 **[!UICONTROL False]** 已選取： `" male","John","TestLastName"`

### 忽略結尾的空格

未顯示在UI熒幕擷圖中。 此旗標可指出是否應該略過要匯出之值的結尾空格。

範例輸出為 **[!UICONTROL True]** 已選取： `"male","John","TestLastName"`
範例輸出為 **[!UICONTROL False]** 已選取： `"male ","John","TestLastName"`

### 后续步骤 {#next-steps}

閱讀本檔案後，您現在瞭解如何設定CSV資料檔案的檔案匯出選項，以根據下游檔案接收系統的需求量身打造檔案內容。 接下來，您可以閱讀 [檔案型目的地啟用教學課程](/help/destinations/ui/activate-batch-profile-destinations.md) 以開始將檔案匯出至您偏好的雲端儲存位置。
