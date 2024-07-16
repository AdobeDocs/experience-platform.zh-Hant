---
title: 夥伴潛在客戶詳細資訊（範例）欄位群組
description: 瞭解合作夥伴潛在客戶詳細資訊（範例）欄位群組(XDM)結構描述欄位群組。
exl-id: 2de1eb7a-2e44-4417-9bdd-7a8a4b2d3a7f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 11%

---

# [!UICONTROL 夥伴潛在客戶詳細資料（範例）]欄位群組

[!UICONTROL 夥伴潛在客戶詳細資料（範例）]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組。 [!UICONTROL 夥伴潛在客戶詳細資訊（範例）]提供了與潛在客戶設定檔相關的各種詳細資訊的範例架構。 此架構可簡化組織和管理各種潛在客戶相關資訊的程式。

此欄位群組會在合作夥伴的內容中延伸[個別潛在客戶設定檔類別](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html)。

![ [!UICONTROL 夥伴潛在客戶詳細資料（範例）]欄位群組的圖表。](../../images/field-groups/partner/partner-prospect-details-sample.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | 字串 | 家庭中的年齡範圍。 |
| [!UICONTROL 服飾] | `apparelAccessories` | 字串 | 喜好設定或參與服裝/配件。 |
| [!UICONTROL 腳踏車] | `bicycling` | 字串 | 對腳踏車活動的興趣或參與。 |
| [!UICONTROL 有線電視] | `cableTv` | 字串 | 表示與有線電視的互動。 |
| [!UICONTROL 國內法] | `domestics` | 字串 | 國內活動中的偏好設定或參與。 |
| [!UICONTROL 電子產品] | `electronics` | 字串 | 對電子裝置的興趣或參與。 |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | 字串 | 喜好或參與食品/飲料。 |
| [!UICONTROL 鞋類] | `footwear` | 字串 | 對鞋類的興趣或參與。 |
| [!UICONTROL 健康食品] | `healthFoods` | 字串 | 喜好或參與健康食品。 |
| [!UICONTROL 健行] | `hiking` | 字串 | 對登山活動的興趣或參與。 |
| [!UICONTROL householdId] | `householdId` | 字串 | 適用於家庭的唯一識別碼。 |
| [!UICONTROL individualId] | `individualId` | 字串 | 適用於個人的唯一識別碼。 |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | 字串 | 持卡人的推論。 |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | 字串 | 身為高階持卡人的推論。 |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | 字串 | 相符層級的指標。 |
| [!UICONTROL 買家評等] | `buyerRating` | 字串 | 和購買行為相關的評等。 |
| [!UICONTROL 捐贈者評等] | `donorRating` | 字串 | 和捐贈者行為相關的評等。 |
| [!UICONTROL 投資評等] | `investmentRating` | 字串 | 與投資行為相關的評等。 |
| [!UICONTROL ResponderRating] | `responderRating` | 字串 | 和回應者行為相關的評等。 |
| [!UICONTROL 花費速度] | `spendingVelocity` | 字串 | 花費的速度或速率。 |
| [!UICONTROL SpendingVolume] | `spendingVolume` | 字串 | 支出的金額或數量。 |
| [!UICONTROL recordId] | `recordId` | 字串 | 紀錄的唯一識別碼。 |
| [!UICONTROL 居住識別碼] | `residenceId` | 字串 | 適用於住宅的唯一識別碼。 |
| [!UICONTROL 航行] | `sailing` | 字串 | 表示對帆船活動的興趣或參與。 |
| [!UICONTROL 季節性假期產品] | `seasonalHolidayProducts` | 字串 | 表示節日產品的偏好設定或參與情形。 |
| [!UICONTROL 滑雪] | `skiing` | 字串 | 表示對滑雪活動的興趣或參與。 |
| [!UICONTROL 網球] | `tennis` | 字串 | 表示對網球活動的興趣或參與。 |
| [!UICONTROL tvShoppers] | `tvShoppers` | 字串 | 表示參與電視購物。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫上的[完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json)。
