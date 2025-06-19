---
source-git-commit: 1ab56cf2495238385d726277f6409d2e0c0cb017
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---
# 片段

## 配额和处理时间线 {#quotas}

记录删除请求受每天和每月标识符提交限制的约束，具体取决于贵组织的许可证权利。 这些限制同时适用于基于UI和基于API的删除请求。

>[!NOTE]
>
>您每天最多可以提交&#x200B;**1,000,000个标识符**，但前提是剩余的每月配额允许这样做。 如果每月上限不到100万，则每日提交内容不能超过该上限。

### 按产品显示的每月提交权利 {#quota-limits}

下表概述了按产品和权利级别划分的标识符提交限制。 对于每个产品，每月上限是两个值中的较小值：固定标识符上限或与许可数据量绑定的基于百分比的阈值。

| 产品 | 权利描述 | 每月上限（以较小者为准） |
|----------|-------------------------|---------------------------------|
| Real-Time CDP或Adobe Journey Optimizer | 不带Privacy and Security Shield或Healthcare Shield附加组件 | 2,000,000个标识符或可寻址受众的5% |
| Real-Time CDP或Adobe Journey Optimizer | 带有Privacy and Security Shield或Healthcare Shield附加组件 | 15,000,000个标识符或10%的可寻址受众 |
| Customer Journey Analytics | 不带Privacy and Security Shield或Healthcare Shield附加组件 | 2,000,000个标识符或每百万CJA权利行有100个标识符 |
| Customer Journey Analytics | 带有Privacy and Security Shield或Healthcare Shield附加组件 | 15,000,000个标识符或每百万CJA权利行有200个标识符 |

>[!NOTE]
>
> 根据大多数组织的实际可寻址受众或CJA行授权，其每月限制较低。

配额在每个日历月的第一天重置。 未使用的配额&#x200B;**未**&#x200B;延期。

>[!NOTE]
>
>配额基于贵组织为&#x200B;**提交的标识符**&#x200B;授予的每月授权。 系统护栏不强制执行这些操作，但可以对其进行监控和审查。
>
>记录删除是&#x200B;**共享服务**。 您的每月上限反映了Real-Time CDP、Adobe Journey Optimizer、Customer Journey Analytics和任何适用的Shield加载项中的最高权限。

### 处理标识符提交的时间表 {#sla-processing-timelines}

提交后，记录删除请求将根据您的权利级别进行排队和处理。

| 产品和权利描述 | 队列持续时间 | 最长处理时间(SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| 不带Privacy and Security Shield或Healthcare Shield附加组件 | 长达15天 | 30 天 |
| 带有Privacy and Security Shield或Healthcare Shield附加组件 | 通常为24小时 | 15 天 |

如果贵组织需要更高的限制，请联系您的Adobe代表进行权利审查。
