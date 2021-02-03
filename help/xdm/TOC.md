---
product: experience-platform
audience: user
user-guide-title: Experience Data Model (XDM) 系统帮助
breadcrumb-title: Experience Data Model (XDM) 指南
user-guide-description: 使用 Experience Data Model (XDM) 类和混合 (mixin) 来标准化体验数据。
translation-type: tm+mt
source-git-commit: cbdeb7529d27cb8b1cacc4a64b90637bb80f514d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 23%

---


# 体验数据模型(XDM)系统{#xdm}

* [XDM系统概述](home.md)
* 模式 (Schema){#schema}
   * [模式合成基础](schema/composition.md)
   * [数据建模的最佳实践](schema/best-practices.md)
   * [XDM字段类型约束](schema/field-constraints.md)
   * [XDM字段字典](schema/field-dictionary.md)
* 类 {#classes}
   * [XDM个人用户档案](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Mixins {#mixins}
   * 用户档案混音{#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [人口统计详细信息](./mixins/profile/person-details.md)
      * [个人联系人详细信息](./mixins/profile/personal-details.md)
      * [细分会员资格详细信息](./mixins/profile/segmentation.md)
      * [工作联系人详细信息](./mixins/profile/work-details.md)
   * 事件混音{#event}
      * [最终用户ID详细信息](./mixins/event/enduserids.md)
      * [环境详细信息](./mixins/event/environment-details.md)
   * [混合名称更新](./mixins/name-updates.md)
* 数据类型 {#data-types}
   * [应用程序](./data-types/application.md)
   * [信标](./data-types/beacon.md)
   * [浏览器详细信息](./data-types/browser-details.md)
   * [同意和首选项](./data-types/consents.md)
   * [设备](./data-types/device.md)
   * [电子邮件地址](./data-types/email-address.md)
   * [环境](./data-types/environment.md)
   * [地域](./data-types/geo.md)
   * [地理圈](./data-types/geo-circle.md)
   * [地理坐标](./data-types/geo-coordinates.md)
   * [地理交互详细信息](./data-types/geo-interaction-details.md)
   * [地理形状](./data-types/geo-shape.md)
   * [身份](./data-types/identity.md)
   * [度量](./data-types/measure.md)
   * [人员](./data-types/person.md)
   * [人员姓名](./data-types/person-name.md)
   * [电话号码](./data-types/phone-number.md)
   * [放置上下文](./data-types/place-context.md)
   * [POI详细信息](./data-types/poi-details.md)
   * [POI交互](./data-types/poi-interaction.md)
   * [邮政地址](./data-types/postal-address.md)
   * [ 搜索](./data-types/search.md)
   * [订阅](./data-types/subscription.md)
   * [Web交互](./data-types/web-interactions.md)
   * [网页详细信息](./data-types/webpage-details.md)
* [!UICONTROL 架] 构UI  {#ui}
   * [概述](./ui/overview.md)
   * [浏览XDM资源](./ui/explore.md)
   * 创建和编辑资源{#resources}
      * [模式 (Schema)](./ui/resources/schemas.md)
      * [类](./ui/resources/classes.md)
      * [Mixins](./ui/resources/mixins.md)
      * [数据类型](./ui/resources/data-types.md)
   * 定义字段{#fields}
      * [概述](./ui/fields/overview.md)
      * [必填字段](./ui/fields/required.md)
      * [对象字段](./ui/fields/object.md)
      * [数组字段](./ui/fields/array.md)
      * [枚举字段](./ui/fields/enum.md)
      * [标识字段](./ui/fields/identity.md)
      * [关系字段](./ui/fields/relationship.md)
* 模式注册表API {#api}
   * [概述](api/overview.md)
   * [入门指南](api/getting-started.md)
   * [模式 (Schema)](api/schemas.md)
   * [行为](api/behaviors.md)
   * [类](api/classes.md)
   * [Mixins](api/mixins.md)
   * [数据类型](api/data-types.md)
   * [描述符](api/descriptors.md)
   * [合并](api/unions.md)
   * [导出／导入](api/export-import.md)
   * [样本数据](api/sample-data.md)
   * [审核日志](api/audit-log.md)
   * [临时模式](api/ad-hoc.md)
   * [附录](api/appendix.md)
* 教程 {#tutorials}
   * [创建模式(API)](tutorials/create-schema-api.md)
   * [创建模式(UI)](tutorials/create-schema-ui.md)
   * [定义两个模式(API)之间的关系](tutorials/relationship-api.md)
   * [定义两个模式(UI)之间的关系](tutorials/relationship-ui.md)
   * [创建点对点模式(API)](tutorials/ad-hoc.md)
* [疑难解答指南](troubleshooting-guide.md)
* [API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [平台发行说明](https://www.adobe.com/go/platform-release-notes-en)