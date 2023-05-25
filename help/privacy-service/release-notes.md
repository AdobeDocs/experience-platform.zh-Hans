---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service发行说明
description: Adobe Experience Platform Privacy Service的最新发行说明。
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 5%

---

# [!DNL Privacy Service] 发行说明

本文档包含有关Adobe Experience Platform新增功能的信息 [!DNL Privacy Service]以及增强功能和重大错误修复。

>[!NOTE]
>
>其他产品的最新发行说明 [!DNL Experience Platform] 可以找到服务 [此处](../release-notes/latest/latest.md).

## 2020 年 9 月 9 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 支持LGPD（巴西） | 现在，隐私工作可以在巴西的 [!DNL Lei Geral de Proteção de Dados] (LGPD)法规。 这些作业根据法规代码进行跟踪 `lgpd_bra`. |

## 2020 年 4 月 8 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | [!DNL Privacy] 现在可以根据泰国的《个人数据保护法》(PDPA)创建和跟踪请求。 在API中提出隐私请求时， `regulation` 数组接受值“pdpa_tha”。 |
| UI中的命名空间类型 | 现在，您可以在的请求生成器中指定不同的命名空间类型 [!DNL Privacy Service] UI。 请参阅 [用户指南](ui/user-guide.md) 了解更多信息。 |
| 弃用旧端点 | 旧API端点(`data/privacy/gdpr`)已被弃用。 |

## 2020年1月14日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| [!DNL Privacy Service] 品牌再造 | 之前称为“GDPR服务”的服务已更名为 [!DNL Privacy Service] 随着服务的发展，除了GDPR之外，还支持其他法规。 |
| 新API端点 | 的基本路径 [!DNL Privacy Service] API更新自 `/data/privacy/gdpr` 到 `/data/core/privacy/jobs` |
| 需要新增 `regulation` 属性 | 在中创建新作业时 [!DNL Privacy Service] API， a `regulation` 必须在请求有效负载中提供属性，以指示要跟踪作业的法规。 接受的值包括 `gdpr` 和 `ccpa`. 查看文档 [隐私作业](api/privacy-jobs.md) 在 [!DNL Privacy Service] API指南，以了解更多信息。 |
| 支持Adobe Primetime身份验证 | [!DNL Privacy Service] 现在接受来自Adobe Primetime身份验证的访问/删除请求，使用 `primetimeAuthentication` 作为其产品价值。 请参阅 [Primetime身份验证文档](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) 了解更多信息。 |

### 增强功能

* [!DNL Privacy Service] UI增强：
   * GDPR和CCPA法规的单独作业跟踪页面。
   * 新 *法规类型* 下拉列表，用于在GDPR和CCPA的跟踪数据之间切换。

## 2019年7月25日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 请求量度仪表板 | 中的新指标仪表板 [!DNL Privacy Service] UI提供了已提交、有错误和已完成的GDPR请求的可见性。 |
| 请求生成器 | 为了向具有提交GDPR请求的技术和非技术用户的组织提供服务，UI中添加了“创建请求”功能。 JSON文件提交功能在以下位置仍然可用： [!DNL Privacy Service] 适用于那些希望继续使用它的组织的UI。 |
| GDPR作业事件通知 | 关于GDPR作业状态的事件通知是许多工作流程的关键元素。 虽然通知以前是使用单独的电子邮件通知提供的，但GDPR事件通知是利用Adobe I/O事件的消息，这些通知将发送到配置的webhook以促进作业请求自动化。 [!DNL Privacy Service] UI用户可以订阅Adobe I/OGDPR事件，以便在产品或GDPR作业完成后接收更新。 |

## 2019 年 4 月 18 日

### 增强功能

* 中状态表的默认范围 [!DNL Privacy Service] UI已修改为7天。
* 更好的内部异常处理。
* 通过在低数据更改率下为常见内部调用引入缓存来提高性能。

### 错误修复

* 为筛选的查询添加了缺失的日志记录信息 `GET /` 中的端点 [!DNL Privacy Service] API。

## 2019 年 4 月 11 日

### 增强功能

* 更新了UI以支持测试版客户的新功能
* 新量度API支持测试版中的UI 2.0功能

## 2019 年 4 月 9 日

### 增强功能

* 将所有查找(GET) API调用更新为默认的30天回顾范围
* 限制了API的使用，最大回顾范围为45天

## 2019年2月14日

### 增强功能

* 强制 `include` POST字段。
* 强制 `include` 上传JSON时的字段。

### 错误修复

* 修复了客户无法加载 [!DNL Privacy Service] UI。
