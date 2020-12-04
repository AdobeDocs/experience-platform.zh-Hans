---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service发行说明
topic: release notes
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 6%

---


# [!DNL Privacy Service] 发行说明

本文档包含有关Adobe Experience Platform的新增功 [!DNL Privacy Service]能、增强和重要错误修复的信息。

>[!NOTE]
>
>其他服务的最新 [!DNL Experience Platform] 发行说明可在此 [找到](../release-notes/latest/latest.md)。

## 2020 年 9 月 9 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 支持LGPD（巴西） | 如今，隐私工作可以根据巴西的(LGPD) [!DNL Lei Geral de Proteção de Dados] 法规创造。 这些工作是根据监管法规进行跟踪的 `lgpd_bra`。 |

## 2020 年 4 月 8 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | [!DNL Privacy] 现在，可以根据泰国的个人数据保护法(PDPA)创建和跟踪请求。 在API中发出隐私请求时， `regulation` 阵列接受值“pdpa_tha”。 |
| UI中的命名空间类型 | 您现在可以在UI的Request Builder中指定不同的命名空间 [!DNL Privacy Service] 类型。 有关详细 [信息](ui/user-guide.md) ，请参阅用户指南。 |
| 旧端点弃用 | 旧API端点(`data/privacy/gdpr`)已弃用。 |

## 2020 年 1 月 14 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| [!DNL Privacy Service] 重新品牌 | 由于服务已发展为支持除GDPR外的其 [!DNL Privacy Service] 他法规，先前命名的“GDPR服务”已重新命名为。 |
| 新的API端点 | API的基本路 [!DNL Privacy Service] 径已从更新 `/data/privacy/gdpr` 到 `/data/core/privacy/jobs` |
| 新的必需 `regulation` 属性 | 在API中创建新作业时，必 [!DNL Privacy Service] 须在请求 `regulation` 有效负荷中提供一个属性，以指示要跟踪作业的法规。 接受的值 `gdpr` 是和 `ccpa`。 有关详细信息， [请参阅](api/privacy-jobs.md) “开发 [!DNL Privacy Service] 人员指南”中的隐私工作文档。 |
| 支持Adobe Primetime身份验证 | [!DNL Privacy Service] 现在接受来自Adobe Primetime身份验证的访问／删除请 `primetimeAuthentication` 求，并将其用作产品值。 See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### 增强功能

* [!DNL Privacy Service] UI增强：
   * 为GDPR和CCPA规定分别设置工作跟踪页面。
   * 新的 *规章类* 型下拉菜单，用于在GDPR和CCPA的跟踪数据之间切换。

## 2019 年 7 月 25 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 请求度量仪表板 | UI中的新指标仪表板 [!DNL Privacy Service] 可以查看已提交、出错和完成的GDPR请求。 |
| 请求生成器 | 为同时具有提交GDPR请求的技术用户和非技术用户的组织提供服务，UI中已添加“创建请求”功能。 对于希望继续使用JSON文件的组织， [!DNL Privacy Service] UI中仍提供JSON文件提交功能。 |
| GDPR工作事件通知 | 关于GDPR工作状态的事件通知对许多工作流来说是一个关键元素。 虽然以前通知是使用单个电子邮件通知发送的，但GDPR事件通知是利用Adobe I/O事件发送的消息，这些消息将发送到已配置的Webhook，以促进作业请求自动化。 [!DNL Privacy Service] UI用户可订阅Adobe I/OGDPR事件，在产品或GDPR作业完成后接收更新。 |

## 2019 年 18 月 4 日

### 增强功能

* UI中状态表的默认 [!DNL Privacy Service] 范围已修改为7天。
* 更好的内部异常处理。
* 通过为低数据更改率的常见内部调用引入缓存，提高了性能。

### 错误修复

* 为API中的端点的筛选查询添加 `GET /` 了缺失的日志 [!DNL Privacy Service] 记录信息。

## 2019 年 11 月 4 日

### 增强功能

* 更新的UI可支持面向测试版客户的新功能
* 支持测试版UI 2.0功能的新指标API

## 2019 年 4 月 9 日

### 增强功能

* 将所有查找(GET)API调用更新为默认的30天回顾范围
* 限制的API使用最大回顾范围为45天

## 2019 年 2 月 14 日

### 增强功能

* 在每次POST `include` 提交时强制执行此字段。
* 上传JSON `include` 时强制执行此字段。

### 错误修复

* 修复了客户无法加载UI的 [!DNL Privacy Service] 问题。