---
title: 在臨時資料集中設定主要身分
description: Adobe Experience Platform查詢服務可讓您直接透過SQL ALTER TABLE命令，為臨機架構資料集欄位設定身分或主要身分。 本檔案說明如何使用ALTER TABLE指令來設定主要身分或次要身分。
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: d9c3ccdf0c0e191af1ab18e894688f301378156d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# 在臨時資料集中設定主要身分

Adobe Experience Platform查詢服務可讓您使用SQL的限制將資料集欄標示為主要或次要身分 `ALTER TABLE` 命令。 您可以使用此功能來確保標幟的欄位符合資料隱私權要求。 這個命令可讓您直接透過SQL新增或刪除主要和次要識別資料表資料行的限制。

## 快速入门

將資料集欄標示為主要或次要身分時，必須瞭解 `ALTER TABLE` SQL命令，並充分瞭解資料隱私權需求。 在繼續本檔案之前，請先檢閱下列檔案：

* [的SQL語法指南 `ALTER TABLE` 命令](../sql/syntax.md).
* [資料控管概觀](../../data-governance/home.md) 以取得詳細資訊。

## 添加约束 {#add-constraints}

此 `ALTER TABLE` command可讓您將資料集欄標示為個人的身分，然後使用SQL更新關聯的中繼資料，將該標籤作為主要身分使用。 當資料集是透過SQL建立的，而非直接透過平台UI從結構描述建立時，此功能特別有用。 命令可用來確保您在Platform中的資料作業符合資料使用原則。

**示例**

下列範例會將限制新增至現有 `t1` 表格。 的值 `id` 欄現在標籤為「 」下的主要身分 `IDFA` 名稱空間。 身分名稱空間是關鍵字，可宣告欄位代表的身分資料型別。

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

第二個範例會確保 `id` 欄會標示為次要身分。

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## 卸除限制 {#drop-constraints}

您也可使用從表格欄移除限制 `ALTER TABLE` 命令。

**示例**

以下範例取消要求 `c1` 欄中標籤為主要身分 `t1` 表格。

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

如下所示，移除身分限制時，會使用相同的語法。

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## 顯示身分

使用中繼資料命令 `show identities` 從命令列介面顯示表格，其中包含指派為身分識別的每個屬性。

```shell
> show identities;
```

以下顯示傳回表格的範例。

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM限制 {#limitations}

以下清單說明使用XDM時更新現有資料集中身分的重要考量事項。

* 若要將欄指定為身分，您可以 **必須** 也會定義要保留為欄中繼資料的名稱空間。
* XDM不支援在名稱空間屬性中指定欄名稱。
* 如果您的結構描述使用 `identityMap` XDM欄位，根或頂層 `identityMap` 物件 **必須** 標籤為身分或主要身分。
