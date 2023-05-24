---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；個別設定檔；欄位；結構描述；結構描述；identityMap；身分對應；身分對應；結構描述設計；對應；聯合結構描述；聯合
solution: Experience Platform
title: XDM個別設定檔類別
description: 本檔案提供XDM個別設定檔類別的概觀。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 是標準的體驗資料模型(XDM)類別，可形成個人的單一代表（或「個人檔案」）。 具體來說，類別（及其相容的欄位群組）會擷取與您品牌互動的已識別和部分識別個人的屬性和興趣。

設定檔的範圍包括匿名行為訊號（例如瀏覽器Cookie），以及包含詳細資訊（例如姓名、出生日期、地點和電子郵件地址）的高度識別設定檔。 隨著個人檔案成長，它會成為個人資訊、身分、聯絡詳細資料和個人通訊偏好設定的強大存放庫。 如需有關在平台生態系統中使用此類別的詳細資訊，請參閱 [XDM概觀](../home.md#data-behaviors).

此 [!DNL XDM Individual Profile] 類別本身提供了數個系統產生的值，這些值會在擷取資料時自動填入，而所有其他欄位則必須透過使用來新增 [相容的結構描述欄位群組](#field-groups)：

![](../images/classes/individual-profile.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | 包含下列專案的物件 [!UICONTROL 日期時間] 欄位： <ul><li>`createDate`：在資料存放區中建立資源的日期和時間，例如首次擷取資料的時間。</li><li>`modifyDate`：上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。 某些情況下， `_id` 可以是 [通用唯一識別碼(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全域唯一識別碼(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>如果您要從來源連線串流資料，或直接從Parquet檔案擷取資料，您應串連特定欄位組合（例如主要ID、時間戳記、記錄型別等）來產生此值。 串連值必須是 `uri-reference` 格式化字串，表示必須移除任何冒號字元。 之後，應該使用SHA-256或您選擇的其他演演算法來雜湊串連值。<br><br>請務必區分 **此欄位不代表與個人相關的身分**&#x200B;而是資料本身的記錄。 與個人相關的身分資料應委派至 [身分欄位](../schema/composition.md#identity) 由相容的欄位群組所提供。 |
| `createdByBatchID` | 導致建立記錄之擷取批次的ID。 |
| `modifiedByBatchID` | 導致記錄更新的上次擷取批次的ID。 |
| `personID` | 此記錄相關個人的唯一識別碼。 此欄位不一定代表與個人相關的身分，除非也指定為個人身分 [身分欄位](../schema/composition.md#identity). |
| `repositoryCreatedBy` | 建立記錄的使用者ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的使用者ID。 |

{style="table-layout:auto"}

## 相容的欄位群組 {#field-groups}

>[!NOTE]
>
>數個欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../field-groups/name-updates.md) 以取得詳細資訊。

Adobe提供數個標準欄位群組，可搭配使用 [!DNL XDM Individual Profile] 類別。 以下是類別的一些常用欄位群組清單：

* [[!UICONTROL 同意和偏好設定]](../field-groups/profile/consents.md)
* [[!UICONTROL 人口統計細節]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL 身分對應]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 熟客方案細節]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL 個人聯絡詳細資訊]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 區段會籍細節]](../field-groups/profile/segmentation.md)
* [[!UICONTROL 電信訂閱]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL 工作聯絡詳細資訊]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL XDM商業人士要素]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL XDM商業人士詳細資料]](../field-groups/profile/business-person-details.md)\*

*\*此欄位群組僅適用於可存取Adobe Real-time Customer Data Platform B2B版本的組織。*

如需以下專案的所有相容欄位群組的完整清單： [!DNL XDM Individual Profile]，請參閱 [XDM GitHub存放庫](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
