---
title: 設定檔合作夥伴擴充（範例）欄位群組
description: 瞭解設定檔合作夥伴擴充（範例）結構描述欄位群組。
exl-id: 02f7c358-3cf9-45cb-a5c5-e2cb1f140d93
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 14%

---

# [!UICONTROL 設定檔合作夥伴擴充（範例）]結構描述欄位群組

[!UICONTROL 設定檔夥伴擴充（範例）]是[[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md)的標準結構描述欄位群組。 使用此欄位群組可為客戶設定檔提供與合作夥伴驅動之擴充功能相關的其他資料。

![ [!UICONTROL 設定檔夥伴擴充（範例）]欄位群組的圖表。](../../images/field-groups/profile-partner-enrichment-sample.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | 字串 | 家庭中的年齡範圍。 |
| [!UICONTROL 服飾] | `apparelAccessories` | 字串 | 服飾與配件資料。 |
| [!UICONTROL 腳踏車] | `bicycling` | 字串 | 與腳踏車相關的資訊。 |
| [!UICONTROL 有線電視] | `cableTv` | 字串 | 有線電視的相關資訊。 |
| [!UICONTROL 國內法] | `domestics` | 字串 | 國內相關資料。 |
| [!UICONTROL 電子產品] | `electronics` | 字串 | 電子相關資訊。 |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | 字串 | 食物和飲料資料。 |
| [!UICONTROL 鞋類] | `footwear` | 字串 | 與鞋類相關的資訊。 |
| [!UICONTROL 健康食品] | `healthFoods` | 字串 | 健康食品資料。 |
| [!UICONTROL 健行] | `hiking` | 字串 | 健行相關資訊。 |
| [!UICONTROL householdId] | `householdId` | 字串 | 家庭的唯一ID。 |
| [!UICONTROL individualId] | `individualId` | 字串 | 個人的唯一ID。 |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | 字串 | 推斷的持卡人資訊。 |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder` | 字串 | 推斷的進階持卡人詳細資訊。 |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | 字串 | 符合層級旗標資料。 |
| [!UICONTROL 買家評等] | `buyerRating` | 字串 | 採購員評等資訊。 |
| [!UICONTROL 捐贈者評等] | `donorRating` | 字串 | 捐贈者評等詳細資料。 |
| [!UICONTROL 投資評等] | `investmentRating` | 字串 | 投資評等資料。 |
| [!UICONTROL ResponderRating] | `responderRating` | 字串 | 回應者評等資訊。 |
| [!UICONTROL 花費速度] | `spendingVelocity` | 字串 | 花費速度詳細資料。 |
| [!UICONTROL SpendingVolume] | `spendingVolume` | 字串 | 花費數量資訊。 |
| [!UICONTROL recordId] | `recordId` | 字串 | 唯一記錄識別碼。 |
| [!UICONTROL 居住識別碼] | `residenceId` | 字串 | 居住地的唯一ID。 |
| [!UICONTROL 航行] | `sailing` | 字串 | 航行相關資料。 |
| [!UICONTROL 季節性假期產品] | `seasonalHolidayProducts` | 字串 | 季節性假日產品資訊。 |
| [!UICONTROL 滑雪] | `skiing` | 字串 | 滑雪相關資料。 |
| [!UICONTROL 網球] | `tennis` | 字串 | 網球相關資訊。 |
| [!UICONTROL tvShoppers] | `tvShoppers` | 字串 | 電視購物者資訊。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫上的[完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json)。
