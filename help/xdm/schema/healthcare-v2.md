---
title: 医疗保健数据模型V2
description: 了解一些常见医疗保健用例以及要使用的最佳类、相关字段组和数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 4d4e68376af914fbfcb005ad950e643f9407ad47
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 12%

---

# [!UICONTROL 医疗保健]数据模型V2

## 字段组和类 {#field-groups}

下表概述了多个常见医疗保健用例的推荐类和架构字段组。

<table>
  <thead>
    <tr>
      <th>用例</th>
      <th>字段组</th>
      <th>兼容类</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>创建/更新患者</strong>：当患者到达医院前台时，将建立患者记录，包括诸如标识符（可选）、患者姓名、出生日期、性别和地址等人口统计详细信息。 这是医疗保健IT的重要组成部分。</td>
      <td><a href="../field-groups/profile/healthcare-patient.md">患者</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="6"><strong>疫苗接种</strong>：促进疫苗接种过程，管理患者免疫记录，并将EMR与疫苗管理系统集成。</td>
      <td><a href="../field-groups/event/healthcare-immunization.md">免疫</a></td>
      <td>
        <li><a href="../classes/experienceevent.md">XDM体验事件</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-patient.md">患者</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">位置</a></td>
      <td>
        <li><a href="../classes/location.md">位置</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-v2.md">药物</a></td>
      <td>
        <li><a href="../classes/medication.md">药物</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-dispense.md">药物分配</a></td>
      <td>
        <li><a href="../classes/medication.md">药物</a></li>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
        <li><a href="../classes/provider.md">提供商</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-request.md">药物请求</a></td>
      <td>
        <li><a href="../classes/medication.md">药物</a></li>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
        <li><a href="../classes/provider.md">提供商</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="4"><strong>后期护理遵守情况</strong>：激励病人和护理人员完成他们的治疗计划并降低汇款率。</td>
      <td><a href="../field-groups/profile/healthcare-patient.md">患者</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">位置</a></td>
      <td>
        <li><a href="../classes/location.md">位置</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-care-plan.md">保护计划</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-goal.md">目标</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
        <li><a href="../classes/provider.md">提供商</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="7"><strong>保险的消费者体验</strong>：改善购买保险的消费者的数字获取和体验。 示例包括： 
        <li> 了解消费者向访问包含常规信息（如计划、计划名称/层、Medicaid或健康计划）页面的用户发送促销电子邮件或定向第三方广告的行为
        </li> 
        <li> 向寻找心脏健康和疫苗信息的人发送有关心脏健康的疫苗信息，以建立品牌意识，或请求安排疫苗接种时间。
        </li>
      </td>
      <td><a href="../field-groups/profile/healthcare-patient.md">患者</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/plan/healthcare-coverage.md">覆盖率</a></td>
      <td>
        <li><a href="../classes/plan.md">计划</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-account.md">帐户</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
        <li><a href="../classes/provider.md">提供商</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">位置</a></td>
      <td>
        <li><a href="../classes/location.md">位置</a></li>
      </td>
    </tr>
      <tr>
      <td><a href="../field-groups/medication/healthcare-medication-v2.md">药物</a></td>
      <td>
        <li><a href="../classes/medication.md">药物</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-dispense.md">药物分配</a></td>
      <td>
        <li><a href="../classes/medication.md">药物</a></li>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
        <li><a href="../classes/provider.md">提供商</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-request.md">药物请求</a></td>
      <td>
        <li><a href="../classes/medication.md">药物</a></li>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
        <li><a href="../classes/provider.md">提供商</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="5"><strong>增强的提供程序体验</strong>：使用EMR系统中的提供程序数据根据约会可用性、位置和专业建议替代提供程序。 <br> <br>改进提供程序搜索以显示具有所需可用性的结果，验证所选提供程序是否为付款人网络的一部分，并提供成本估算。
      </td>
      <td><a href="../field-groups/profile/healthcare-patient.md">患者</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">位置</a></td>
      <td>
        <li><a href="../classes/location.md">位置</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-organization.md">组织</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
        <li><a href="../classes/provider.md">提供商</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-practioner.md">从业者</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
        <li><a href="../classes/provider.md">提供商</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-schedule.md">计划</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">XDM 轮廓</a></li>
        <li><a href="../classes/provider.md">提供商</a></li>
      </td>
    </tr>
  </tbody>
</table>

## 数据类型 {#data-types}

下表概述了根据[!DNL HL7 FHIR Release 5]规范创建的数据类型。

| 名称 | 描述 |
| --- | --- |
| [[!UICONTROL 地址]](../data-types/healthcare/address.md) | 描述使用邮政惯例表示的地址（与GPS或其他位置定义格式不同）。 |
| [[!UICONTROL 批注]](../data-types/healthcare/annotation.md) | 归因于作者的文本节点。 |
| [[!UICONTROL 可用性]](../data-types/healthcare/availability.md) | 项目的可用性数据。 |
| [[!UICONTROL 可编码的概念]](../data-types/healthcare/codeable-concept.md) | 从一个资源到另一个资源的引用。 |
| [[!UICONTROL 可编码引用]](../data-types/healthcare/codeable-reference.md) | 对资源或概念的引用。 |
| [[!UICONTROL 编码]](../data-types/healthcare/coding.md) | 对术语系统定义的代码的引用。 |
| [[!UICONTROL 联系点]](../data-types/healthcare/contact-point.md) | 人员的联系详细信息。 |
| [[!UICONTROL 剂量]](../data-types/healthcare/dosage.md) | 服药方式或应服药方式。 |
| [[!UICONTROL 持续时间]](../data-types/healthcare/duration.md) | 时间长度。 |
| [[!UICONTROL 扩展的联系人详细信息]](../data-types/healthcare/extended-contact-detail.md) | 扩展联系人的信息。 |
| [[!UICONTROL 人名]](../data-types/healthcare/human-name.md) | 有关人类或其他生命实体的名称的信息。 |
| [[!UICONTROL 标识符]](../data-types/healthcare/identifier.md) | 用于计算的标识符。 |
| [[!UICONTROL 钱]](../data-types/healthcare/money.md) | 以某种公认货币表示的经济效用金额。 |
| [[!UICONTROL 周期]](../data-types/healthcare/period.md) | 由开始和结束日期/时间定义的时间段。 |
| [[!UICONTROL 人员]](../data-types/healthcare/person.md) | 有关一般人员记录的信息。 |
| [[!UICONTROL 数量]](../data-types/healthcare/quantity.md) | 可衡量的金额。 |
| [[!UICONTROL Range]](../data-types/healthcare/range.md) | 由低值和高值绑定的一组值。 |
| [[!UICONTROL 比率]](../data-types/healthcare/ratio.md) | 通过分子和分母两个[[!UICONTROL 数量]](../data-types/healthcare/quantity.md)值的比率。 |
| [[!UICONTROL 引用]](../data-types/healthcare/reference.md) | 从一个资源到另一个资源的引用。 |
| [[!UICONTROL 重复]](../data-types/healthcare/repeat.md) | 描述事件计划时间的一组规则。 |
| [[!UICONTROL 简单数量]](../data-types/healthcare/simple-quantity.md) | 可衡量的金额。 |
| [[!UICONTROL 计时]](../data-types/healthcare/timing.md) | 有关可能发生多次的事件的信息。 |
| [[!UICONTROL 虚拟服务详细信息]](../data-types/healthcare/virtual-service-detail.md) | 虚拟服务联系人详细信息。 |
