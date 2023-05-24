---
title: 稽核記錄概觀
description: 了解如何通过审核日志查看谁在 Adobe Experience Platform 中执行了哪些操作。
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 48%

---

# 审核日志 {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="热门操作"
>abstract="此小部件显示在选定时间范围内在 Experience Platform 中执行的最常见操作类型。要查看 Platform 中记录的操作的完整列表，请选择左侧导航中的&#x200B;**审计**。"

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="热门用户"
>abstract="此小部件显示在所选时间段内在 Experience Platform 中执行的操作最多的用户。要查看 Platform 中记录的操作的完整列表，请选择左侧导航中的&#x200B;**审计**。"

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="在 Platform 中监测用户活动"
>abstract="<h2>描述</h2><p>可按审核日志的形式监测多种 Platform 服务和功能的用户活动。这些日志组成一条审核线索，其中记录<b>谁</b><b>何时</b>执行了<b>什么</b>。审核日志可帮助解决 Platform 上的问题以及帮助您的企业有效地遵守公司数据管理政策和监管要求。</p>"

為了提高系統中所執行活動的透明度和可見度，Adobe Experience Platform可讓您以「稽核記錄」的形式，稽核各種服務和功能的使用者活動。 這些記錄形成稽核軌跡，可協助疑難排解Platform上的問題，並幫助您的企業有效遵守公司資料管理政策和法規要求。

从基本意义上讲，审核日志将说明&#x200B;**谁**&#x200B;执行了&#x200B;**什么**&#x200B;操作，以及在&#x200B;**什么时候**&#x200B;执行的。日志中记录的每个操作都包含元数据，这些元数据可指示操作类型、日期和时间、执行操作的用户的电子邮件 ID 以及与操作类型相关的其他属性。

本檔案涵蓋Platform中的稽核記錄，包括如何在UI或API中檢視和管理它們。

## 审核日志记录的事件类型 {#category}

下表概述稽核記錄針對哪些資源所記錄的動作：

| 资源 | 操作 |
| --- | --- |
| [存取控制原則（以屬性為基礎的存取控制）](../../../access-control/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [帳戶(Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [Attribution AI執行個體](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>停用</li></ul> |
| [审核日志](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>导出</li></ul> |
| [类](../../../xdm/schema/composition.md#class) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| 計算屬性 | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [Customer AI執行個體](../../../intelligent-services/customer-ai/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>停用</li></ul> |
| [数据集](../../../catalog/datasets/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>啟用對象 [即時客戶個人檔案](../../../profile/home.md)</li><li>為設定檔停用</li><li>新增資料</li><li>刪除批次</li></ul> |
| [資料流](../../../edge/datastreams/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>停用</li><li>[编辑映射](../../../edge/datastreams/data-prep.md)</li></ul> |
| [数据类型](../../../xdm/schema/composition.md#data-type) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [目标](../../../destinations/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>停用</li><li>資料集啟動</li><li>資料集移除</li><li>設定檔啟動</li><li>設定檔移除</li></ul> |
| [字段组](../../../xdm/schema/composition.md#field-group) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [身份图](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>视图</li></ul> |
| [身分名稱空間](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>创建</li><li>更新</li></ul> |
| [合併原則](../../../profile/merge-policies/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [产品配置文件](../../../access-control/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [查询](../../../query-service/ui/overview.md) | <ul><li>Execute</li></ul> |
| [查詢範本](../../../query-service/ui/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [角色（以屬性為基礎的存取控制）](../../../access-control/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>添加用户</li><li>移除使用者</li></ul> |
| [沙盒](../../../sandboxes/home.md) | <ul><li>创建</li><li>更新</li><li>重置</li><li>Delete</li></ul> |
| [排定的查詢](../../../query-service/ui/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [架构](../../../xdm/schema/composition.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>為設定檔啟用</li></ul> |
| [区段](../../../segmentation/home.md) | <ul><li>创建</li><li>Delete</li><li>區段啟用</li><li>區段移除</li></ul> |
| [來源資料流程](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>停用</li><li>資料集啟用</li><li>資料集移除</li><li>設定檔啟用</li><li>設定檔移除</li></ul> |
| [工單](../../../hygiene/home.md) | <ul><li>创建</li></ul> |

## 访问审核日志

为您的组织启用该功能后，系统会在活动发生时自动收集审核日志。您无需手动启用日志收集。

若要檢視和匯出稽核記錄，您必須擁有 **[!UICONTROL 檢視使用者活動記錄]** 已授予存取控制許可權(可在 [!UICONTROL 資料控管] 類別)。 若要瞭解如何管理Platform功能的個別許可權，請參閱 [存取控制檔案](../../../access-control/home.md).

## 在UI中管理稽核記錄 {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="说明"
>abstract="<ul><li>在左侧导航中选择<b>审核</b>。“审核”工作区显示记录日志的列表，默认按最新到最旧排序。</li>   <li> 注意：将审核日志保留 365 天，此后将从系统中删除审核日志。因此，只能回溯最长为期 365 天。如果需要回溯超过 365 天之前的数据，则应定期导出日志以满足您的内部政策要求。 </li><li>从列表中选择一个事件以在右边栏中查看其详细信息。 </li><li>选择漏斗图标以显示过滤器控件的列表，帮助缩小结果范围。无论选择什么过滤器，都仅显示最后 1000 条记录。 </li><li>要导出审核日志的当前列表，请选择&#x200B;**下载日志**。</li><li>有关此功能的更多帮助，请参阅 Experience League 上的<a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=zh-Hans">审核日志概述</a>。</li></ul>"

您可以在中檢視不同Experience Platform功能的稽核記錄 **[!UICONTROL 稽核]** Platform UI中的工作區。 工作區會顯示記錄日誌的清單，預設情況下會從最近到最近排序。

![稽核記錄儀表板](../../images/audit-logs/audits.png)

稽核記錄會保留365天，之後會從系統中刪除它們。 因此，只能回溯最长为期 365 天。如果您需要超過365天的資料，您應定期匯出記錄檔，以符合內部原則需求。

从列表中选择一个事件以在右边栏中查看其详细信息。

![事件詳細資料](../../images/audit-logs/select-event.png)

### 筛选审核日志

>[!NOTE]
由於這是一項新功能，顯示的資料僅追溯至2022年3月。 根據選取的資源，從2022年1月起，可能會提供舊版資料。


選取漏斗圖示(![篩選圖示](../../images/audit-logs/icon.png))來顯示篩選控制項清單，以協助縮小結果範圍。 僅顯示最後1000筆記錄，無論選擇的各種篩選器為何。

![筛选器](../../images/audit-logs/filters.png)

在 UI 中有以下过滤器可用于审核事件：

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 类别] | 使用下拉式選單，依以下條件篩選顯示的結果 [類別](#category). |
| [!UICONTROL 操作] | 依動作篩選。 目前僅適用 [!UICONTROL 建立] 和 [!UICONTROL 刪除] 可以篩選動作。 |
| [!UICONTROL 用户] | 輸入完整的使用者ID (例如， `johndoe@acme.com`)，依使用者篩選。 |
| [!UICONTROL 状态] | 篩選條件為允許（完成）動作或因缺少動作而拒絕動作 [存取控制](../../../access-control/home.md) 許可權。 |
| [!UICONTROL 日期] | 選取開始日期和/或結束日期，以定義篩選結果的日期範圍。 可匯出90天回顧期間的資料（例如，2021-12-15到2022-03-15）。 這可能因事件型別而異。 |

若要移除篩選條件，請針對有問題的篩選條件，選取藥丸圖示上的「X」，或選取 **[!UICONTROL 全部清除]** 以移除所有篩選器。

![清除篩選器](../../images/audit-logs/clear-filters.png)

### 匯出稽核記錄

要导出审核日志的当前列表，请选择&#x200B;**[!UICONTROL 下载日志]**。

![下載記錄](../../images/audit-logs/download.png)

在出現的對話方塊中，選取您偏好的格式 **[!UICONTROL CSV]** 或 **[!UICONTROL JSON]**)，然後選取 **[!UICONTROL 下載]**. 瀏覽器會下載產生的檔案，並將其儲存到您的電腦。

![選取下載格式](../../images/audit-logs/select-download-format.png)

## 管理API中的稽核記錄

您在 UI 中可以执行的所有操作也可以使用 API 调用来完成。有关详细信息，请参阅 [ API 参考文档](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 管理Adobe Admin Console的稽核記錄

若要瞭解如何管理Adobe Admin Console活動的稽核記錄，請參閱下列內容 [檔案](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## 後續步驟和其他資源

本指南說明如何管理Experience Platform稽核記錄。 如需如何監視Platform活動的詳細資訊，請參閱以下檔案： [可觀察性深入分析](../../../observability/home.md) 和 [監控資料擷取](../../../ingestion/quality/monitor-data-ingestion.md).

若要加深您對Experience Platform稽核記錄的瞭解，請觀看以下影片：

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
