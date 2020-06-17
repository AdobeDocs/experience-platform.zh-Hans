---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service发行说明
topic: release notes
translation-type: tm+mt
source-git-commit: 580cce74ab7da9547417a9e74e88b5ddab52171f
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 5%

---


# Privacy Service发行说明

本文档包含有关Adobe Experience Platform Privacy Service新增功能、增强功能和重要错误修复的信息。

>[!NOTE] 有关其他Experience Platform服务的最新发行说明，请 [访问](../release-notes/latest/latest.md)。

## 2020 年 4 月 8 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | 现在，可以根据泰国的个人数据保护法(PDPA)创建和跟踪隐私请求。 在API中发出隐私请求时， `regulation` 阵列接受值“pdpa_tha”。 |
| UI中的命名空间类型 | 您现在可以在命名空间UI的请求生成器中指定不同的Privacy Service类型。 有关详细 [信息](ui/user-guide.md) ，请参阅用户指南。 |
| 旧端点弃用 | 旧API端点(`data/privacy/gdpr`)已弃用。 |

## 2020 年 1 月 14 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| Privacy Service品牌重塑 | 由于服务已发展为支持除GDPR外的其他法规，先前被命名为“GDPR服务”已重新更名为Privacy Service。 |
| 新的API端点 | Privacy ServiceAPI的基本路径已从更新 `/data/privacy/gdpr` 到 `/data/core/privacy/jobs` |
| 新的必需 `regulation` 属性 | 在Privacy ServiceAPI中创建新作业时，必须在请 `regulation` 求有效负荷中提供一个属性，以指示要跟踪作业的法规。 接受的值 `gdpr` 是和 `ccpa`。 有关详细信息，请 [参阅Privacy Service开](api/privacy-jobs.md) 发人员指南中有关隐私工作的文档。 |
| 支持Adobe Primetime身份验证 | Privacy Service现在接受来自Adobe Primetime身份验证的访问／删除请求， `primetimeAuthentication` 并将其作为产品价值。 See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### 增强功能

* Privacy ServiceUI增强：
   * 为GDPR和CCPA规定分别设置工作跟踪页面。
   * 新的 _规章类_ 型下拉菜单，用于在GDPR和CCPA的跟踪数据之间切换。

## 2019 年 7 月 25 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 请求度量仪表板 | Privacy ServiceUI中的新指标仪表板可以查看已提交、出错和完成的GDPR请求。 |
| 请求生成器 | 为同时具有提交GDPR请求的技术用户和非技术用户的组织提供服务，UI中已添加“创建请求”功能。 对于希望继续使用JSON文件的组织，Privacy ServiceUI中仍提供JSON文件提交功能。 |
| GDPR工作事件通知 | 关于GDPR工作状态的事件通知对许多工作流来说是一个关键元素。 虽然以前通知是使用单独的电子邮件通知发送的，但GDPR事件通知是利用Adobe I/O事件的消息，这些通知会发送到已配置的Webhook，以促进作业请求自动化。 Privacy ServiceUI用户可以订阅Adobe I/O GDPR事件，以便在产品或GDPR作业完成后接收更新。 |

## 2019 年 18 月 4 日

### 增强功能

* Privacy ServiceUI中状态表的默认范围已修改为7天。
* 更好的内部异常处理。
* 通过为低数据更改率的常见内部调用引入缓存，提高了性能。

### 错误修复

* 在查询API中为端点添加了筛选Privacy Service `GET /` 的缺失日志记录信息。

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

* 在每次 `include` POST提交中强制执行此字段。
* 上传JSON `include` 时强制执行此字段。

### 错误修复

* 修复了客户无法加载Privacy ServiceUI的问题。