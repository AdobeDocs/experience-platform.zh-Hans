---
keywords: Experience Platform；首页；热门话题
solution: Experience Platform
title: Privacy Service 发行说明
description: Adobe Experience Platform Privacy Service 的最新发行说明。
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# [!DNL Privacy Service] 发行说明

本文档包含有关 Adobe Experience Platform [!DNL Privacy Service] 的新功能以及增强功能和重大错误修复的信息。

>[!NOTE]
>
>其他 [!DNL Experience Platform] 服务的最新发行说明可在[此处](../release-notes/latest/latest.md)找到。

## 2020 年 9 月 9 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 支持 LGPD（巴西） | 现在可以根据巴西 [!DNL Lei Geral de Proteção de Dados] (LGPD) 法规创建隐私作业。这些任务会根据监管代码 `lgpd_bra` 进行追踪。 |

## 2020 年 4 月 8 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| PDPA 支持 | 现在可以根据泰国的《个人数据保护法》（PDPA）创建和跟踪 [!DNL Privacy] 请求。在 API 中发出隐私请求时，`regulation` 数组接受值“pdpa_tha”。 |
| UI 中的命名空间类型 | 您现在可以在 [!DNL Privacy Service] UI 中的请求构建器中指定不同的命名空间类型。请参阅[用户指南](ui/user-guide.md)，获取更多信息。 |
| 旧端点弃用 | 已弃用旧的 API 端点 (`data/privacy/gdpr`)。 |

## 2020 年 1 月 14 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| [!DNL Privacy Service] 品牌重塑 | 之前的“GDPR 服务”现已更名为 [!DNL Privacy Service]，因为该服务经过发展现在支持 GDPR 之外的其他法规。 |
| 新的 API 端点 |  [!DNL Privacy Service] API 的基本路径已从 `/data/privacy/gdpr` 更新为 `/data/core/privacy/jobs` |
| 新的必需 `regulation` 属性 | 在 [!DNL Privacy Service] API 中创建新作业时，必须在请求负载中提供 `regulation` 属性，以指示根据哪条规定跟踪该作业。接受的值包括 `gdpr` 和 `ccpa`。如需了解更多信息，请参阅 [API 指南中有关](api/privacy-jobs.md)隐私作业[!DNL Privacy Service]的文档。 |
| 支持 Adobe Primetime 身份验证 | [!DNL Privacy Service] 现在接受来自 Adobe Primetime 身份验证的访问/删除请求，其中使用 `primetimeAuthentication` 作为其产品值。要了解更多信息，请参阅[ Primetime 身份验证文档](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)。 |

### 增强功能

* [!DNL Privacy Service] UI 增强功能
   * 针对 GDPR 和 CCPA 法规设置单独的作业跟踪页面。
   * 新的&#x200B;*法规类型*&#x200B;下拉菜单可在 GDPR 和 CCPA 的跟踪数据之间切换。

## 2019 年 7 月 25 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 请求量度仪表板 | 通过 [!DNL Privacy Service] UI 中的新量度仪表板可查看已提交、出现错误的和已完成的 GDPR 请求。 |
| 请求生成器 | 为了支持由技术型和非技术型用户提交 GDPR 请求的组织，UI 中添加了“创建请求”功能。对于希望继续使用 JSON 文件提交功能的组织，[!DNL Privacy Service] UI 中仍然提供该功能。 |
| GDPR 作业事件通知 | 有关 GDPR 作业状态的事件通知是许多工作流的关键要素。虽然以前使用单独的电子邮件通知来提供通知，但 GDPR 事件通知功能是利用 Adobe I/O 事件的消息，这些事件会被发送到经过配置的 webhook，以促进作业请求自动化。[!DNL Privacy Service] UI 用户可以订阅 Adobe I/O GDPR 事件，以便在产品或 GDPR 作业完成时接收更新。 |

## 2019 年 4 月 18 日

### 增强功能

*  [!DNL Privacy Service] UI 中状态表的默认范围已修改为 7 天的跨度。
* 提升了内部异常处理能力。
* 通过对数据变化率较低的常见内部调用引入缓存来提高性能。

### 错误修复

* 为 [!DNL Privacy Service] API 中的 `GET /` 端点的过滤查询添加了缺失的记录信息。

## 2019 年 4 月 11 日

### 增强功能

* 更新 UI 以支持为 Beta 客户提供的新功能
* 添加了新量度 API，以支持 Beta 版的 UI 2.0 功能

## 2019 年 4 月 9 日

### 增强功能

* 更新了所有查找 (GET) API 调用，将默认查找范围设置为 30 天
* 限制了 API 的使用，将最大查找范围设为 45 天

## 2019 年 2 月 14 日

### 增强功能

* 在每次 POST 提交中强制执行 `include` 字段。
* 上传 JSON 时强制执行 `include` 字段。

### 错误修复

* 修复了客户无法加载 [!DNL Privacy Service] UI 的问题。
