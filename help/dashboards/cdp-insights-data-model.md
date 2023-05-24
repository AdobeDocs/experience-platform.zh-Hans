---
title: Real-time Customer Data Platform Insights資料模型
description: 瞭解如何搭配Real-time Customer Data Platform Insights資料模型使用SQL查詢，以根據您的行銷和KPI使用案例自訂您自己的Real-Time CDP報表。
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 2%

---

# Real-time Customer Data Platform Insights資料模型

Real-time Customer Data Platform Insights資料模型功能可公開支援各種設定檔、目的地和分段Widget深入分析的資料模型和SQL。 您可以自訂這些SQL查詢範本，為您的行銷和關鍵績效指標(KPI)使用案例建立Real-Time CDP報表。 這些見解然後可用作使用者定義儀表板的自訂Widget。 如需瞭解，請參閱query accelerated store reporting insights檔案 [如何透過Query Service建立報告見解資料模型，以便與加速商店資料和使用者定義的儀表板搭配使用](../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md).

## 先决条件

本指南需要您對 [使用者定義儀表板功能](./user-defined-dashboards.md). 請先閱讀檔案，再繼續閱讀本指南。

## Real-Time CDP深入分析報表與使用案例

Real-Time CDP報表可讓您深入瞭解設定檔資料，以及資料與區段和目的地的關係。 各種星形結構描述模型已開發來回答各種常見行銷使用案例，每個資料模型可支援多個使用案例。

>[!IMPORTANT]
>
>用於Real-Time CDP報表的資料對於所選的合併原則和最近的每日快照而言是準確的。

### 設定檔模型 {#profile-model}

設定檔模型包含三個資料集：

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

下圖包含每個資料集中的相關資料欄位。

![輪廓模型的ERD。](./images/cdp-insights/profile-model.png)

#### 設定檔計數使用案例

用於設定檔計數Widget的邏輯會傳回拍攝快照時設定檔存放區中合併的設定檔總數。 請參閱 [[!UICONTROL 設定檔計數] Widget檔案](./guides/profiles.md#profile-count) 以取得詳細資訊。

產生「 」的SQL [!UICONTROL 設定檔計數] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_profiles) CNT
FROM qsaccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
AND adwh_fact_profile.merge_policy_id=${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

#### 單一身分設定檔使用案例

用於的邏輯 [!UICONTROL 單一身分設定檔] widget會提供貴組織設定檔的計數，而這些設定檔只有一種建立其身分識別的ID型別。 請參閱[[!UICONTROL 單一身分設定檔] Widget檔案](./guides/profiles.md#single-identity-profiles) 以取得詳細資訊。

產生「 」的SQL [!UICONTROL 單一身分設定檔] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_Single_Identity_profiles) CNT
FROM QSAccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN QSAccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
  AND adwh_fact_profile.merge_policy_id =${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

### 名稱空間模型 {#namespace-model}

名稱空間模型由下列資料集組成：

- `adwh_dim_date`
- `adwh_fact_profile_by_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`

下圖包含每個資料集中的相關資料欄位。

![名稱空間模型的ERD。](./images/cdp-insights/namespace-model.png)

#### 依身分使用案例區分的設定檔

此 [!UICONTROL 依身分割槽分的設定檔] widget會顯示您的個人資料存放區中所有合併個人資料的身分劃分。 請參閱 [[!UICONTROL 依身分割槽分的設定檔] Widget檔案](./guides/profiles.md#profiles-by-identity) 以取得詳細資訊。

產生「 」的SQL [!UICONTROL 依身分割槽分的設定檔] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT adwh_dim_namespaces.namespace_description,
    sum(adwh_fact_profile_by_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
JOIN qsaccel.profile_agg.adwh_dim_namespaces ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_namespace.merge_policy_id =${mergePolicyId}
AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
GROUP BY adwh_fact_profile_by_namespace.date_key,
        adwh_fact_profile_by_namespace.merge_policy_id,
        adwh_dim_namespaces.namespace_description
ORDER BY count_of_profiles DESC
LIMIT 5;
```

+++

#### 依身分使用案例區分的單一身分設定檔

用於的邏輯 [!UICONTROL 依身分割槽分的單一身分設定檔] widget會說明僅以單一唯一識別碼識別的設定檔總數。 請參閱 [依身分Widget檔案的單一身分設定檔](./guides/profiles.md#single-identity-profiles-by-identity) 以取得詳細資訊。

產生「 」的SQL [!UICONTROL 依身分割槽分的單一身分設定檔] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT
  adwh_dim_namespaces.namespace_description,
  sum(adwh_fact_profile_by_namespace.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_namespace
  LEFT OUTER JOIN
    qsaccel.profile_agg.adwh_dim_namespaces
    ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE
  adwh_fact_profile_by_namespace.merge_policy_id=${mergePolicyId}
  AND adwh_fact_profile_by_namespace.date_key='${lastProcessDate}'
GROUP BY
  adwh_fact_profile_by_namespace.date_key,
  adwh_fact_profile_by_namespace.merge_policy_id,
  adwh_dim_namespaces.namespace_description;
```

+++

### 區段模型 {#segment-model}

區段模型包含下列資料集：

- `adwh_dim_date`
- `adwh_fact_profile_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下圖包含每個資料集中的相關資料欄位。

![區段模型的ERD。](./images/cdp-insights/segment-model.png)

#### 對象人數使用案例

用於的邏輯 [!UICONTROL 對象人數] widget會傳回在最近的快照集執行時所選區段內的合併設定檔總數。 請參閱 [[!UICONTROL 對象人數] Widget檔案](./guides/segments.md#audience-size) 以取得詳細資訊。

產生「 」的SQL [!UICONTROL 對象人數] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT adwh_fact_profile_by_segment.date_key,
       adwh_dim_merge_policies.merge_policy_name,
       adwh_dim_segments.segment,
       adwh_dim_segments.segment_name,
       sum(adwh_fact_profile_by_segment.count_of_profiles)count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE adwh_fact_profile_by_segment.date_key ='${lastProcessDate}'
  AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY adwh_fact_profile_by_segment.date_key,
         adwh_dim_merge_policies.merge_policy_name,
         adwh_dim_segments.segment,
         adwh_dim_segments.segment_name
ORDER BY count_of_profiles DESC
LIMIT 20;
```

+++

#### 對象人數變化趨勢使用案例

用於的邏輯 [!UICONTROL 對象人數變化趨勢] Widget提供線圖，說明最近每日快照之間符合指定區段資格的設定檔總數差異。 請參閱 [[!UICONTROL 對象人數變化趨勢] Widget檔案](./guides/segments.md#audience-size-change-trend) 以取得詳細資訊。

產生「 」的SQL [!UICONTROL 對象人數變化趨勢] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT DISTINCT cast(adwh_dim_segments.create_date AS Date) Date_key, adwh_dim_merge_policies.merge_policy_name,
  count(DISTINCT adwh_dim_segments.segment_id)Segments_Added
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE Cast(adwh_dim_segments.create_date AS date) >= dateadd(DAY, - ${dayRange}, '${lastProcessDate}')
AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY cast(adwh_dim_segments.create_date AS date), adwh_dim_merge_policies.merge_policy_name ;
```

+++

#### 最常用的目的地使用案例

中使用的邏輯 [!UICONTROL 最常使用的目的地] Widget會根據對應至您組織最常用目的地的區段數，列出這些目的地。 此排名可讓您深入瞭解正在使用的目的地，同時可能還會顯示那些可能未充分利用的目的地。 請參閱以下說明檔案： [[!UICONTROL 最常使用的目的地] Widget](./guides/destinations.md#most-used-destinations) 以取得詳細資訊。

產生「 」的SQL [!UICONTROL 最常使用的目的地] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT
   adwh_dim_destination.destination_name, adwh_dim_destination.destination_id,
   count( distinct adwh_dim_br_segment_destinations.segment_id ) segment_count
FROM
   qsaccel.profile_agg.adwh_dim_destination
   join qsaccel.profile_agg.adwh_dim_br_segment_destinations
 ON
   adwh_dim_destination.destination_id = adwh_dim_br_segment_destinations.destination_id
 WHERE
   adwh_dim_destination.destination_name is not null
 group by
   adwh_dim_destination.destination_name,
   adwh_dim_destination.destination_id
   order by segment_count desc limit 5;
```

+++

#### 最近啟用的區段使用案例

的邏輯 [!UICONTROL 最近啟用的區段] Widget提供最近對應至目的地的區段清單。 此列表提供系统中正使用的区段和目标的快照，并且可以帮助纠正任何错误的映射。請參閱 [[!UICONTROL 最近啟用的區段] Widget檔案](./guides/destinations.md#recently-activated-segments) 以取得詳細資訊。

產生「 」的SQL [!UICONTROL 最近啟用的區段] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT segment_name, segment, destination_name, a.create_time create_time
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY create_time desc, segment LIMIT 5;
```

+++

### 名稱空間 — 區段模型

namespace-segment模型由下列資料集組成：

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下圖包含每個資料集中的相關資料欄位。

![名稱空間 — 區段模型的ERD。](./images/cdp-insights/namespace-segment-model.png)

#### 區段使用案例的依身分割槽分的設定檔

中使用的邏輯 [!UICONTROL 依身分割槽分的設定檔] widget會針對指定區段，提供個人資料存放區中所有合併個人資料的身分劃分。 請參閱 [[!UICONTROL 依身分割槽分的設定檔] Widget檔案](./guides/segments.md#profiles-by-identity) 以取得詳細資訊。

產生「 」的SQL [!UICONTROL 依身分割槽分的設定檔] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT adwh_dim_namespaces.namespace_description,
  sum( adwh_fact_profile_by_segment_and_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces
ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_segment_and_namespace.segment_id = {segment_id}
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = {merge_policy_id}
AND adwh_fact_profile_by_segment_and_namespace.date_key = '{date}'
GROUP BY adwh_dim_namespaces.namespace_description;
```

+++

### 重疊名稱空間模型

重疊名稱空間模型由下列資料集組成：

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

下圖包含每個資料集中的相關資料欄位。

![重疊名稱空間模型的ERD。](./images/cdp-insights/overlap-namespace-model.png)

#### 身分重疊（設定檔）使用案例

中使用的邏輯 [!UICONTROL 身分重疊] Widget會顯示您的設定檔中的重疊專案 **設定檔存放區** 包含兩個選取的身分識別。 如需詳細資訊，請參閱 [[!UICONTROL 身分重疊] 的widget區段 [!UICONTROL 設定檔] 儀表板檔案](./guides/profiles.md#identity-overlap).

產生「 」的SQL [!UICONTROL 身分重疊] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT Sum(overlap_col1) overlap_col1,
       Sum(overlap_col2) overlap_col2,
       coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
     WHERE adwh_fact_profile_overlap_of_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_overlap_of_namespace.date_key = '${lastProcessDate}'
       AND adwh_fact_profile_overlap_of_namespace.overlap_id IN
         (SELECT adwh_dim_overlap_namespaces.overlap_id
          FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
          WHERE adwh_dim_overlap_namespaces.merge_policy_id=${mergePolicyId}
            AND adwh_dim_overlap_namespaces.overlap_namespaces IN ('${namespace1}',
                                                                   '${namespace2}')
          GROUP BY adwh_dim_overlap_namespaces.overlap_id
          HAVING Count(*) > 1)
     UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace1}'
     UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace2}' ) a;
```

+++

### 依區段模型重疊名稱空間

依區段模型的重疊名稱空間是由下列資料集組成：

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下圖包含每個資料集中的相關資料欄位。

![依區段模型的重疊名稱空間ERD。](./images/cdp-insights/overlap-namespace-by-segment-model.png)

#### 身分重疊（區段）使用案例

中使用的邏輯 [!UICONTROL 區段] 儀表板 [!UICONTROL 身分重疊] widget說明包含特定區段之兩個選定身分的設定檔重疊。 如需詳細資訊，請參閱 [[!UICONTROL 身分重疊] 的widget區段 [!UICONTROL 細分] 儀表板檔案](./guides/segments.md#identity-overlap).

產生「 」的SQL [!UICONTROL 身分重疊] 在以下可摺疊區段中可看到Widget。

+++SQL查詢

```sql
SELECT
   Sum(overlap_col1) overlap_col1,
   Sum( overlap_col2) overlap_col2,
   Sum(overlap_count) Overlap_count
FROM
   (
      SELECT
         0 overlap_col1,
         0 overlap_col2,
         Sum(count_of_profiles) Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
      WHERE
         adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = $ {segmentId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '${lastProcessDate}'
         and adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
         (
            SELECT
               adwh_dim_overlap_namespaces.overlap_id
            FROM
               qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE
               adwh_dim_overlap_namespaces.merge_policy_id =$ {mergePolicyId}
               AND adwh_dim_overlap_namespaces.overlap_namespaces IN
               (
                  '${namespace1}',
                  '${namespace2}'
               )
            GROUP BY
               adwh_dim_overlap_namespaces.overlap_id
            HAVING
               Count(*) > 1
         )
      UNION ALL
      SELECT
         count_of_profiles overlap_col1,
         0 overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace1}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
      UNION ALL
      SELECT
         0 overlap_col1,
         count_of_profiles overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace2}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
   )
   a;
```

+++
