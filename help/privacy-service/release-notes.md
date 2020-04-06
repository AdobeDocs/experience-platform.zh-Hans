---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隐私服务发行说明
topic: release notes
translation-type: tm+mt
source-git-commit: 682436b29df4696e98ef96fe5a65ab32221098ba

---


# 隐私服务发行说明

本文档包含有关Adobe Experience Platform Privacy Service新增功能的信息，以及增强功能和重要错误修复。

## 2020 年 8 月 4 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | 现在，可以根据泰国的个人数据保护法(PDPA)创建和跟踪隐私请求。 在API中发出隐私请求时，数 `regulation` 组接受值“pdpa_tha”。 |
| 命名空间UI中的类型 | 您现在可以在隐私服务UI的Request Builder中指定不同的命名空间类型。 有关详细 [信息，请参阅](ui/user-guide.md) 《用户指南》。 |
| 旧端点弃用 | 旧API端点(`data/privacy/gdpr`)已弃用。 |

## 2020 年 1 月 14 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| Privacy Service重新品牌化 | 先前名为“GDPR服务”的服务已更名为隐私服务，因为该服务已发展为支持除GDPR外的其他法规。 |
| 新的API端点 | 隐私服务API的基本路径已从更 `/data/privacy/gdpr` 新为 `/data/core/privacy/jobs` |
| 新的必需 `regulation` 属性 | 在Privacy Service API中创建新作业时，必须在请求有效负荷中提供一个属性，以指示要跟踪作业的规定。 `regulation` 接受的值 `gdpr` 是和 `ccpa`。 有关详细信息，请参 [阅隐私服务](api/privacy-jobs.md) 开发人员指南中有关隐私工作的文档。 |
| 支持Adobe Primetime身份验证 | 隐私服务现在接受Adobe Primetime身份验证的访问／删除请求，并 `primetimeAuthentication` 将其作为产品价值。 See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### 增强功能

* 隐私服务UI增强：
   * 为GDPR和CCPA规定单独分别设置作业跟踪页面。
   * 可在 __ GDPR和CCPA的跟踪数据之间切换的新调整类型下拉菜单。

## 2019 年 7 月 25 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 请求度量仪表板 | 隐私服务UI中的新指标仪表板可以查看已提交、出错和完成的GDPR请求。 |
| Request Builder | 为了为具有提交GDPR请求的技术和非技术用户的组织提供服务，UI中已添加了“创建请求”功能。 对于希望继续使用JSON文件的组织，隐私服务UI中仍提供JSON文件提交功能。 |
| GDPR作业事件通知 | 事件GDPR作业状态通知是许多工作流的关键元素。 虽然以前通知是使用单个电子邮件通知发送的，但GDPR事件通知是利用Adobe I/O事件发送的消息，这些通知会发送到配置的webhook，以便于作业请求自动化。 隐私服务UI用户可以订阅Adobe I/O GDPR事件，以在产品或GDPR作业完成后接收更新。 |

## 2019 年 18 月 4 日

### 增强功能

* 隐私服务UI中状态表的默认范围被修改为7天。
* 更好地处理内部异常。
* 通过为低数据更改率的常见内部调用引入缓存，提高了性能。

### 错误修复

* 在隐私服务API中为端点添加了筛选查询 `GET /` 的缺失日志记录信息。

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

* 在每个POST `include` 提交中强制执行字段。
* 上传JSON `include` 时强制执行该字段。

### 错误修复

* 修复了客户无法加载隐私服务UI的问题。