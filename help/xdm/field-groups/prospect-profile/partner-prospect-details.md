---
title: 夥伴潛在客戶詳細資訊（範例）欄位群組
description: 瞭解合作夥伴潛在客戶詳細資訊（範例）欄位群組(XDM)結構描述欄位群組。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 9%

---

# [!UICONTROL 合作夥伴潛在客戶詳細資訊（範例）] 欄位群組

[!UICONTROL 合作夥伴潛在客戶詳細資訊（範例）] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 此 [!UICONTROL 合作夥伴潛在客戶詳細資訊（範例）] 提供與潛在客戶設定檔相關的各種細節的範例架構。 此架構可簡化組織和管理各種潛在客戶相關資訊的程式。

此欄位群組可擴充 [個別潛在客戶設定檔類別](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) 在合作夥伴的內容中。

![的圖表 [!UICONTROL 合作夥伴潛在客戶詳細資訊（範例）] 欄位群組。](../../images/field-groups/partner/partner-prospect-details-sample.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | 字串 | 家庭中的年齡範圍。 |
| [!UICONTROL 服飾配件] | `apparelAccessories` | 字串 | 喜好設定或參與服裝/配件。 |
| [!UICONTROL 腳踏車] | `bicycling` | 字串 | 對腳踏車活動的興趣或參與。 |
| [!UICONTROL 有線電視] | `cableTv` | 字串 | 表示與有線電視的互動。 |
| [!UICONTROL 國內法] | `domestics` | 字串 | 國內活動中的偏好設定或參與。 |
| [!UICONTROL 電子產品] | `electronics` | 字串 | 對電子裝置的興趣或參與。 |
| [!UICONTROL 食物與飲料] | `foodAndBeverage` | 字串 | 喜好或參與食品/飲料。 |
| [!UICONTROL 鞋類] | `footwear` | 字串 | 對鞋類的興趣或參與。 |
| [!UICONTROL 健康食品] | `healthFoods` | 字串 | 喜好或參與健康食品。 |
| [!UICONTROL 健行] | `hiking` | 字串 | 對登山活動的興趣或參與。 |
| [!UICONTROL householdId] | `householdId` | 字串 | 適用於家庭的唯一識別碼。 |
| [!UICONTROL individualId] | `individualId` | 字串 | 適用於個人的唯一識別碼。 |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | 字串 | 持卡人的推論。 |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | 字串 | 身為高階持卡人的推論。 |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | 字串 | 相符層級的指標。 |
| [!UICONTROL BuyerRating] | `buyerRating` | 字串 | 和購買行為相關的評等。 |
| [!UICONTROL 捐贈者評等] | `donorRating` | 字串 | 和捐贈者行為相關的評等。 |
| [!UICONTROL 投資評等] | `investmentRating` | 字串 | 與投資行為相關的評等。 |
| [!UICONTROL ResponderRating] | `responderRating` | 字串 | 和回應者行為相關的評等。 |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | 字串 | 花費的速度或速率。 |
| [!UICONTROL 支出量] | `spendingVolume` | 字串 | 支出的金額或數量。 |
| [!UICONTROL recordId] | `recordId` | 字串 | 紀錄的唯一識別碼。 |
| [!UICONTROL residenceId] | `residenceId` | 字串 | 適用於住宅的唯一識別碼。 |
| [!UICONTROL 帆船] | `sailing` | 字串 | 表示對帆船活動的興趣或參與。 |
| [!UICONTROL 季節性假日產品] | `seasonalHolidayProducts` | 字串 | 表示節日產品的偏好設定或參與情形。 |
| [!UICONTROL 滑雪] | `skiing` | 字串 | 表示對滑雪活動的興趣或參與。 |
| [!UICONTROL 網球] | `tennis` | 字串 | 表示對網球活動的興趣或參與。 |
| [!UICONTROL tvShoppers] | `tvShoppers` | 字串 | 表示參與電視購物。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) 位於公用XDM存放庫上。
