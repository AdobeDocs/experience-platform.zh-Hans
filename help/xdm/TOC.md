---
product: experience-platform
audience: user
user-guide-title: Experience Data Model (XDM) 系统帮助
breadcrumb-title: Data Model (XDM) 指南
user-guide-description: 使用 Experience Data Model (XDM) 类和混合来标准化体验数据。
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 20%

---


# Experience Data Model (XDM) System {#xdm}

* [XDM系统概述](home.md)
* 模式 {#schema}
   * [模式合成基础](schema/composition.md)
   * [XDM字段类型约束](schema/field-constraints.md)
   * [XDM字段字典](schema/field-dictionary.md)
   * 模式使用案例 {#use-cases}
      * [隐私同意混合](schema/privacy-consent.md)
* 类 {#classes}
   * [XDM个人用户档案](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Mixins {#mixins}
   * 用户档案混合 {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [用户档案人详细信息](./mixins/profile/person-details.md)
      * [用户档案个人详细信息](./mixins/profile/personal-details.md)
      * [用户档案细分](./mixins/profile/segmentation.md)
      * [用户档案工作详细信息](./mixins/profile/work-details.md)
   * 事件混合 {#event}
      * [ExperienceEvent EndUserID](./mixins/event/enduserids.md)
      * [体验活动环境详细信息](./mixins/event/environment-details.md)
* 数据类型 {#data-types}
   * [信标](./data-types/beacon.md)
   * [浏览器详细信息](./data-types/browser-details.md)
   * [设备](./data-types/device.md)
   * [电子邮件地址](./data-types/email-address.md)
   * [环境](./data-types/environment.md)
   * [地域](./data-types/geo.md)
   * [地理圈](./data-types/geo-circle.md)
   * [地理坐标](./data-types/geo-coordinates.md)
   * [地理交互详细信息](./data-types/geo-interaction-details.md)
   * [地理形状](./data-types/geo-shape.md)
   * [身份](./data-types/identity.md)
   * [人员姓名](./data-types/person-name.md)
   * [电话号码](./data-types/phone-number.md)
   * [放置上下文](./data-types/place-context.md)
   * [POI详细信息](./data-types/poi-details.md)
   * [POI交互](./data-types/poi-interaction.md)
   * [邮政地址](./data-types/postal-address.md)
* 模式注册表API {#api}
   * [入门指南](api/getting-started.md)
   * [列表资源](api/list-resources.md)
   * [查找资源](api/look-up-resource.md)
   * [更新资源](api/update-resource.md)
   * [替换资源](api/replace-resource.md)
   * [删除资源](api/delete-resource.md)
   * [创建类](api/create-class.md)
   * [创建混音](api/create-mixin.md)
   * [创建数据类型](api/create-data-type.md)
   * [创建模式](api/create-schema.md)
   * [合并](api/unions.md)
   * [描述符](api/descriptors.md)
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