---
keywords: Experience Platform；主页；热门主题；Marketo Engage;Marketo Engage;Marketo；映射
solution: Experience Platform
title: Marketo Engage源的映射字段
topic-legacy: overview
description: 下表包含Marketo数据集中的字段与其相应XDM字段之间的映射。
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
source-git-commit: be3ec7dc7e2089a8cee0b1577659e1ec0a465044
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 6%

---

# [!DNL Marketo Engage] 字段映射

下表包含九个 [!DNL Marketo] 数据集及其对应的体验数据模型(XDM)字段。

>[!TIP]
>
>全部 [!DNL Marketo] 数据集除外 `Activities` 现在支持 `isDeleted`. 您的现有数据流将自动包含 `isDeleted`，但将仅为新摄取的数据摄取标记。 如果要将标记应用于所有历史数据，则必须停止现有数据流并使用新映射重新创建它们。 请注意，如果您删除 `isDeleted`，则您将无法再访问该功能。 自动填充映射后，必须保留该映射。

## 活动 {#activities}

的 [!DNL Marketo] 源现在支持其他标准活动。 要使用标准活动，您必须使用 [模式自动生成实用程序](../marketo/marketo-namespaces.md) 因为如果您 `activities` 数据流在不更新架构的情况下，映射模板将失败，因为架构中不存在新的目标字段。 如果选择不更新架构，您仍然可以创建新数据流并关闭任何错误。 但是，任何新字段或更新字段将不会摄取到平台中。

| 源数据集 | XDM目标字段 | 注释 |
| -------------- | ---------------- | ----- |
| `_id` | `_id` |
| `"Marketo"` | `personKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `personKey.sourceInstanceID` | 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `personID` | `personKey.sourceID` |
| `concat(personID,"@${MUNCHKIN_ID}.Marketo")` | `personKey.sourceKey` | 主标识。 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `eventType` | `eventType` |
| `producedBy` | `producedBy` |
| `timestamp` | `timestamp` |
| `web.webPageDetails.URL` | `web.webPageDetails.URL` |
| `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |
| `environment.ipV4` | `environment.ipV4` |
| `search.keywords` | `search.keywords` |
| `search.searchEngine` | `search.searchEngine` |
| `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |
| `web.webPageDetails.name` | `web.webPageDetails.name` |
| `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |
| `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |
| `web.webReferrer.URL` | `web.webReferrer.URL` |
| `iif(${listOperations\.listID} != null && ${listOperations\.listID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", ${listOperations\.listID}, "sourceKey", concat(${listOperations\.listID},"@${MUNCHKIN_ID}.Marketo")), null)` | `listOperations.listKey` |
| `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |
| `iif(${opportunityEvent\.opportunityID} != null && ${opportunityEvent\.opportunityID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${opportunityEvent\.opportunityID}, "sourceKey", concat(${opportunityEvent\.opportunityID},"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityEvent.opportunityKey` |
| `opportunityEvent.role` | `opportunityEvent.role` |
| `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |
| `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |
| `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |
| `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |
| `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |
| `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |
| `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |
| `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |
| `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |
| `directMarketing.mailingID` | `directMarketing.mailingID` |
| `directMarketing.mailingName` | `directMarketing.mailingName` |
| `directMarketing.testVariantName` | `directMarketing.testVariantName` |
| `directMarketing.testVariantID` | `directMarketing.testVariantID` |
| `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |
| `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |
| `directMarketing.email` | `directMarketing.email` |
| `device.isMobileDevice` | `device.isMobileDevice` |
| `device.model` | `device.model` |
| `environment.operatingSystem` | `environment.operatingSystem` |
| `directMarketing.linkURL` | `directMarketing.linkURL` |
| `web.webInteraction.linkID` | `web.webInteraction.linkID` |
| `web.fillOutForm.webFormID` | `web.fillOutForm.webFormID` |
| `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |
| `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |
| `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |
| `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |
| `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |
| `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |
| `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |
| `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |
| `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |
| `leadOperation.changeScore.scoreAttributeID` | `leadOperation.changeScore.scoreAttributeID` |
| `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |
| `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |
| `json_to_object(${opportunityEvent\.dataValueChanges})` | `opportunityEvent.dataValueChanges` |
| `iif(${leadOperation\.campaignProgression\.campaignID} != null && ${leadOperation\.campaignProgression\.campaignID} != "" , to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${leadOperation\.campaignProgression\.campaignID}, "sourceKey", concat(${leadOperation\.campaignProgression\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.campaignProgression.campaignKey` |
| `leadOperation.campaignProgression.campaignID` | `leadOperation.campaignProgression.campaignID` |
| `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |
| `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |
| `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |
| `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |
| `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |
| `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |
| `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |
| `leadOperation.interestingMoment.date` | `leadOperation.interestingMoment.date` |
| `leadOperation.interestingMoment.description` | `leadOperation.interestingMoment.description` |
| `leadOperation.interestingMoment.source` | `leadOperation.interestingMoment.source` |
| `leadOperation.interestingMoment.type` | `leadOperation.interestingMoment.type` |
| `iif(${leadOperation\\.callWebhook\\.webhookKey\\.sourceID} != null && ${leadOperation\\.callWebhook\\.webhookKey\\.sourceID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.callWebhook\\.webhookKey\\.sourceID}, \"sourceKey\", concat(${leadOperation\\.callWebhook\\.webhookKey\\.sourceInstanceID},\"@${MUNCHKIN_ID}.Marketo\")), null)"` | `leadOperation.callWebhook.webhookKey` |
| `leadOperation.callWebhook.webhookName` | `leadOperation.callWebhook.webhookName` |
| `leadOperation.callWebhook.responseCode` | `leadOperation.callWebhook.responseCode` |
| `iif(${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceID} != null && ${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceID}, \"sourceKey\", concat(${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceInstanceID},\"@${MUNCHKIN_ID}.Marketo\")), null)"` | `leadOperation.changeCampaignCadence.campaignKey` |
| `leadOperation.changeCampaignCadence.newCadence` | `leadOperation.changeCampaignCadence.newCadence` |
| `leadOperation.changeCampaignCadence.previousCadence` | `leadOperation.changeCampaignCadence.previousCadence` |
| `iif(${leadOperation\.addToCampaign\.campaignID} != null && ${leadOperation\.addToCampaign\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.campaignID}, "sourceKey", concat(${leadOperation\.addToCampaign\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.campaignKey` |
| `iif(${leadOperation\.addToCampaign\.streamID} != null && ${leadOperation\.addToCampaign\.streamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.streamID}, "sourceKey", concat(${leadOperation\.addToCampaign\.streamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.streamKey` |
| `leadOperation.addToCampaign.streamName` | `leadOperation.addToCampaign.streamName` |
| `iif(${leadOperation\.changeCampaignStream\.campaignID} != null && ${leadOperation\.changeCampaignStream\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.campaignID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.campaignKey` |
| `iif(${leadOperation\.changeCampaignStream\.newStreamID} != null && ${leadOperation\.changeCampaignStream\.newStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.newStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.newStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.newStreamKey` |
| `leadOperation.changeCampaignStream.newStreamName` | `leadOperation.changeCampaignStream.newStreamName` |
| `iif(${leadOperation\.changeCampaignStream\.previousStreamID} != null && ${leadOperation\.changeCampaignStream\.previousStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.previousStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.previousStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.previousStreamKey` |
| `leadOperation.changeCampaignStream.previousStreamName` | `leadOperation.changeCampaignStream.previousStreamName` |
| `iif(${leadOperation\.changeRevenueStage\.modelID} != null && ${leadOperation\.changeRevenueStage\.modelID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.modelID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.modelID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.modelKey` |
| `leadOperation.changeRevenueStage.modelName` | `leadOperation.changeRevenueStage.modelName` |
| `iif(${leadOperation\.changeRevenueStage\.newStageID} != null && ${leadOperation\.changeRevenueStage\.newStageID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.newStageID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.newStageID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.newStageKey` |
| `leadOperation.changeRevenueStage.newStageName` | `leadOperation.changeRevenueStage.newStageName` |
| `iif(${leadOperation\\.changeRevenueStage\\.previousStageID} != null && ${leadOperation\\.changeRevenueStage\\.previousStageID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${leadOperation\\.changeRevenueStage\\.previousStageID}, \"sourceKey\", concat(${leadOperation\\.changeRevenueStage\\.previousStageID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeRevenueStage.previousStageKey` |
| `leadOperation.changeRevenueStage.previousStageName` | `leadOperation.changeRevenueStage.previousStageName` |
| `leadOperation.changeRevenueStage.reason` | `leadOperation.changeRevenueStage.reason` |
| `iif(${leadOperation\.mergeLeads\.sourceIDs} != null && ${leadOperation\.mergeLeads\.sourceIDs} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.mergeLeads\.sourceIDs}, "sourceKey", concat(${leadOperation\.mergeLeads\.sourceIDs},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.mergeLeads.sourceKeys` |
| `leadOperation.mergeLeads.targetUpdated` | `leadOperation.mergeLeads.targetUpdated` |
| `leadOperation.mergeLeads.mergedInCRM` | `leadOperation.mergeLeads.mergedInCRM` |
| `leadOperation.mergeLeads.mergeSource` | `leadOperation.mergeLeads.mergeSource` |
| `iif(${directMarketing\\.emailSent\\.mailingID} != null && ${directMarketing\\.emailSent\\.mailingID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${directMarketing\\.emailSent\\.mailingID}, \"sourceKey\", concat(${directMarketing\\.emailSent\\.mailingID},\"@${MUNCHKIN_ID}.Marketo\")), null)"` | `directMarketing.emailSent.mailingKey` |
| `directMarketing.emailSent.mailingName` | `directMarketing.emailSent.mailingName` |
| `directMarketing.emailSent.testVariantID` | `directMarketing.emailSent.testVariantID` |
| `directMarketing.emailSent.testVariantName` | `directMarketing.emailSent.testVariantName` |
| `directMarketing.emailSent.automationRunID` | `directMarketing.emailSent.automationRunID` |

{style=&quot;table-layout:auto&quot;}

## 项目 {#programs}

| 源数据集 | XDM目标字段 | 注释 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `campaignKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `campaignKey.sourceInstanceID` | 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `id` | `campaignKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignKey.sourceKey` | 主标识。 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `iif(sfdcId != null && sfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", sfdcId, "sourceKey", concat(sfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | 的  `extSourceSystemAudit.externalKey` 是次标识。 的值 `{CRM_ORG_ID}` 和 `{CRM_TYPE}` 将被自动替换。 |
| `name` | `campaignName` |
| `description` | `campaignDescription` |
| `type` | `campaignType` |
| `status` | `campaignStatus` |
| `channel` | `channelName` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `cost` | `actualCost.amount` |
| `iif(parentProgramId != null && parentProgramId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", parentProgramId, "sourceKey", concat(parentProgramId,"@${MUNCHKIN_ID}.Marketo")), null)` | `parentCampaignKey` |
| `integrationPartner` | `integrationPartnerName` |
| `webinarSessionName` | `webinarSessionName` |
| `webinarSessionDescription` | `webinarSessionDescription` |
| `webinarHistorySyncStatus` | `webinarHistorySyncStatus` |
| `webinarHistorySyncDate` | `webinarHistorySyncDate` |
| `startDate` | `campaignStartDate` |
| `endDate` | `campaignEndDate` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## 方案成员资格 {#program-memberships}

| 源数据集 | XDM目标字段 | 注释 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `campaignMemberKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `campaignMemberKey.sourceInstanceID` | 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `id` | `campaignMemberKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignMemberKey.sourceKey` | 主标识。 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `iif(programId != null && programId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", programId, "sourceKey", concat(programId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | 关系 |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | 关系 |
| `iif(acquiredByCampaignID != null && acquiredByCampaignID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", acquiredByCampaignID, "sourceKey", concat(acquiredByCampaignID,"@${MUNCHKIN_ID}.Marketo")), null)` | `acquiredByCampaignKey` |
| `reachedSuccess` | `hasReachedSuccess` |
| `isExhausted` | `isExhausted` |
| `statusName` | `memberStatus` |
| `statusReason` | `memberStatusReason` |
| `membershipDate` | `membershipDate` |
| `nurtureCadence` | `nurtureCadence` |
| `trackName` | `nurtureTrackName` |
| `webinarUrl` | `webinarConfirmationUrl` |
| `registrationCode` | `webinarRegistrationID` |
| `reachedSuccessDate` | `reachedSuccessDate` |
| `iif(sfdc.crmId != null && sfdc.crmId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", sfdc.crmId, "sourceKey", concat(sfdc.crmId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | 的 `extSourceSystemAudit.externalKey` 是次标识。 的值 `{CRM_ORG_ID}` 和 `{CRM_TYPE}` 将被自动替换。 |
| `sfdc.lastStatus` | `lastStatus` |
| `sfdc.hasResponded` | `hasResponded` |
| `sfdc.firstRespondedDate` | `firstRespondedDate` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## 公司 {#companies}

| 源数据集 | XDM目标字段 | 注释 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `concat(id, ".mkto_org")` | `accountKey.sourceID` |
| `concat(id, ".mkto_org@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | 主标识。 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| <ul><li>`iif(mktoCdpExternalId != null && mktoCdpExternalId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", mktoCdpExternalId, "sourceKey", concat(mktoCdpExternalId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(msftCdpExternalId != null && msftCdpExternalId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", msftCdpExternalId, "sourceKey", concat(msftCdpExternalId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `extSourceSystemAudit.externalKey` | 的 `extSourceSystemAudit.externalKey` 是次标识。 的值 `{CRM_ORG_ID}` 和 `{CRM_TYPE}` 将被自动替换。 |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `billingCity` | `accountBillingAddress.city` |
| `billingCountry` | `accountBillingAddress.country` |
| `billingPostalCode` | `accountBillingAddress.postalCode` |
| `billingState` | `accountBillingAddress.state` |
| `billingStreet` | `accountBillingAddress.street1` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `website` | `accountOrganization.website` |
| `mainPhone` | `accountPhone.number` |
| `company` | `accountName` |
| `companyNotes` | `accountDescription` |
| `site` | `accountSite` |
| `iif(mktoCdpParentOrgId != null && mktoCdpParentOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpParentOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpParentOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## 静态列表 {#static-lists}

| 源数据集 | XDM目标字段 | 注释 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `marketingListKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `marketingListKey.sourceInstanceID` | `"${MUNCHKIN_ID}"` 将作为“浏览API”的一部分替换。 |
| `id` | `marketingListKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `marketingListKey.sourceKey` | 主标识。 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `name` | `marketingListName` |
| `description` | `marketingListDescription` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## 静态列表成员关系 {#static-list-memberships}

| 源数据集 | XDM目标字段 | 注释 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `marketingListMemberKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `marketingListMemberKey.sourceInstanceID` | 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `staticListMemberID` | `marketingListMemberKey.sourceID` |
| `concat(staticListMemberID,"@${MUNCHKIN_ID}.Marketo")` | `marketingListMemberKey.sourceKey` | 主标识。 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `iif(staticListID != null && staticListID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", staticListID, "sourceKey", concat(staticListID,"@${MUNCHKIN_ID}.Marketo")), null)` | `marketingListKey` | 关系 |
| `iif(personID != null && personID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", personID, "sourceKey", concat(personID,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | 关系 |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## 指定帐户 {#named-accounts}

>[!IMPORTANT]
>
>只有在Marketo的基于帐户的营销(ABM)功能中，才需要命名帐户数据集。 如果您没有使用ABM，则无需为指定帐户设置映射。

| 源数据集 | XDM目标字段 | 注释 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `concat(id, ".mkto_acct")` | `accountKey.sourceID` |
| `concat(id, ".mkto_acct@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | 主标识。 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `iif(crmGuid != null && crmGuid != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", crmGuid, "sourceKey", concat(crmGuid,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | 的 `extSourceSystemAudit.externalKey` 是次标识。 的值 `{CRM_ORG_ID}` 和 `{CRM_TYPE}` 将被自动替换。 |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `city` | `accountBillingAddress.city` |
| `country` | `accountBillingAddress.country` |
| `state` | `accountBillingAddress.state` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `logoUrl` | `accountOrganization.logoUrl` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `name` | `accountName` |
| `iif(parentAccountId != null && parentAccountId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(parentAccountId, ".mkto_acct"), "sourceKey", concat(parentAccountId, ".mkto_acct@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |
| `sourceType` | `accountSourceType` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## 机会 {#opportunities}

| 源数据集 | XDM目标字段 | 注释 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `opportunityKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `opportunityKey.sourceInstanceID` | 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `id` | `opportunityKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityKey.sourceKey` | 主标识。 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `iif(externalOpportunityId != null && externalOpportunityId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", externalOpportunityId, "sourceKey", concat(externalOpportunityId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey.sourceKey` | 次标识。 的值 `{CRM_ORG_ID}` 和 `{CRM_TYPE}` 将被自动替换。 |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | 关系 |
| `description` | `opportunityDescription` |
| `name` | `opportunityName` |
| `stage` | `opportunityStage` |
| `type` | `opportunityType` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `expectedRevenue` | `expectedRevenue.amount` |
| `amount` | `opportunityAmount.amount` |
| `closeDate` | `expectedCloseDate` |
| `fiscalQuarter` | `fiscalQuarter` |
| `fiscalYear` | `fiscalYear` |
| `forecastCategory` | `forecastCategory` |
| `forecastCategoryName` | `forecastCategoryName` |
| `isClosed` | `isClosed` |
| `isWon` | `isWon` |
| `quantity` | `opportunityQuantity` |
| `probability` | `probabilityPercentage` |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | 此源数据集仅对具有 [!DNL Salesforce] 集成。 |
| `lastActivityDate` | `lastActivityDate` |
| `leadSource` | `leadSource` |
| `nextStep` | `nextStep` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## 机会联系角色 {#opportunity-contact-roles}

| 源数据集 | XDM目标字段 | 注释 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `opportunityPersonKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `opportunityPersonKey.sourceInstanceID` | 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `id` | `opportunityPersonKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityPersonKey.sourceKey` | 主标识。 的值 `"${MUNCHKIN_ID}"` 将作为“浏览API”的一部分替换。 |
| `iif(mktoCdpSfdcId != null && mktoCdpSfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", mktoCdpSfdcId, "sourceKey", concat(mktoCdpSfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | 的 `extSourceSystemAudit.externalKey` 是次标识。 的值 `{CRM_ORG_ID}` 和 `{CRM_TYPE}` 将被自动替换。 |
| `iif(mktoCdpOpptyId != null && mktoCdpOpptyId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", mktoCdpOpptyId, "sourceKey", concat(mktoCdpOpptyId,"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityKey` | 关系 |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | 关系 |
| `role` | `personRole` |
| `isPrimary` | `isPrimary` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## 人员 {#persons}

| 源数据集 | XDM目标字段 | 注释 |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `b2b.personKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `b2b.personKey.sourceInstanceID` | 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `id` | `b2b.personKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `b2b.personKey.sourceKey` | 主标识。 的值 `"${MUNCHKIN_ID}"` 将被自动替换。 |
| `iif(unsubscribed == 'true', 'n', 'y' ))` | `consents.marketing.email.val` | 如果取消订阅，则 `true` (例如，value = `1`)，然后设置 `consents.marketing.email.val` as(`n`)。 如果取消订阅，则 `false` (例如，value = `0`)，然后设置 `consents.marketing.email.val` as `null`. |
| `iif(unsubscribedReason != null && unsubscribedReason != "", substr(unsubscribedReason, 0, 100), null)` | `consents.marketing.email.reason` |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.accountKey` |
| `marketingSuspended` | `b2b.isMarketingSuspended` |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` |
| `leadScore` | `b2b.personScore` |
| `leadSource` | `b2b.personSource` |
| `leadStatus` | `b2b.personStatus` |
| `personType` | `b2b.personType` |
| `leadPartitionId` | `b2b.personGroupID` |
| `mktoCdpIsConverted` | `b2b.isConverted` |
| `mktoCdpConvertedDate` | `b2b.convertedDate` |
| <ul><li>`iif(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null), "sourceKey", concat(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null), "sourceKey", concat(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `extSourceSystemAudit.externalKey` | 的 `extSourceSystemAudit.externalKey` 是次标识。 |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `title` | `extendedWorkDetails.jobTitle` |
| `fax` | `faxPhone.number` |
| `mobilePhone` | `mobilePhone.number` |
| `firstName` | `person.name.firstName` |
| `lastName` | `person.name.lastName` |
| `middleName` | `person.name.middleName` |
| `salutation` | `person.name.courtesyTitle` |
| `dateOfBirth` | `person.birthDate` |
| `city` | `workAddress.city` |
| `country` | `workAddress.country` |
| `postalCode` | `workAddress.postalCode` |
| `state` | `workAddress.state` |
| `address` | `workAddress.street1` |
| `phone` | `workPhone.number` |
| `company` | `b2b.companyName` |
| `website` | `b2b.companyWebsite` |
| `leadScore` | `personComponents.personScore` |
| `leadSource` | `personComponents.personSource` |
| `leadStatus` | `personComponents.personStatus` |
| `personType` | `personComponents.personType` |
| `leadPartitionId` | `personComponents.personGroupID` |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceAccountKey` |
| <ul><li>`iif(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null), "sourceKey", concat(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null), "sourceKey", concat(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `personComponents.sourceExternalKey` |
| `iif(id != null && id != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", id, "sourceKey", concat(id,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourcePersonKey` |
| `email` | `personComponents.workEmail.address` |
| `email` | `workEmail.address` |
| `iif(ecids != null, to_object('ECID',arrays_to_objects('id',explode(ecids))), null)` | `identityMap` | 这是一个计算字段。 |
| `marketoIsDeleted` | `isDeleted` |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", mktoCdpCnvContactPersonId, \"sourceKey\", concat(mktoCdpCnvContactPersonId,\"@${MUNCHKIN_ID}.Marketo\")), null)` | `b2b.convertedContactKey` | 这是一个计算字段。 |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", mktoCdpCnvContactPersonId, \"sourceKey\", concat(mktoCdpCnvContactPersonId,\"@${MUNCHKIN_ID}.Marketo\")), null)` | `personComponents.sourceConvertedContactKey` | 这是一个计算字段。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>的 `to_object('ECID',arrays_to_objects('id',explode(ecids)))` 源字段是一个必须使用 [!UICONTROL 添加计算字段] 选项。 请参阅 [添加计算字段](../../../../data-prep/ui/mapping.md#calculated-fields) 以了解更多信息。

## 后续步骤

通过阅读本文档，您对您的 [!DNL Marketo] 数据集及其对应的XDM字段。 请参阅 [创建 [!DNL Marketo] 源连接](../../../tutorials/ui/create/adobe-applications/marketo.md) 完成 [!DNL Marketo] 数据流。
