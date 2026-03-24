---
title: Talon.One Source概觀
description: 瞭解Adobe Experience Platform上的Talon.One來源
badge: Beta
exl-id: 92ed180a-6175-45e2-a831-0f40fd8606b0
source-git-commit: 3d0c216a9f8eb46a25221660253a80ce8e7a7eb0
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 2%

---

# [!DNL Talon.One]

>[!AVAILABILITY]
>
>[!DNL Talon.One]來源為測試版。 閱讀來源概觀中的[條款與條件](../../home.md#terms-and-conditions)，以取得有關使用測試版標籤之來源的詳細資訊。

透過[!DNL Talon.One]，您可以輕鬆建立、管理及最佳化針對客戶量身打造的個人化行銷活動。 使用這個強大的平台來執行折扣、分發優惠券、啟動轉介計畫、設定忠誠度計畫以及提供遊戲化的獎勵，所有這些都透過一個可擴充的系統來協助您吸引和獎勵您的對象。

您可以使用Adobe Experience Platform來源目錄中的[!DNL Talon.One]來源，從您的[!DNL Talon.One]帳戶中擷取批次和串流熟客資料。

* [Talon.One串流事件](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One Batch Source Connector](../../tutorials/ui/create/loyalty/talon-one-batch.md)

>[!TIP]
>
>忠誠度資料是指您一般使用者的忠誠度計畫資訊，例如忠誠度點數、花費的忠誠度點數、目前層級、授予的優惠券、轉介和成就。

## 先決條件 {#prerequisites}

提供下列認證的值，以驗證及連線[!DNL Talon.One Batch Source Connector]。

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| 網域 | 與您的[!DNL Talon.One]應用程式環境關聯的唯一URL。 輸入網域時，請確定不含通訊協定或路徑。 | `acmetalonone.us-east4` |
| [!DNL Talon.One]管理API金鑰 | 管理API金鑰是用來驗證及授權存取[!DNL Talon.One]的管理API的認證。 這會處理下列作業： <ul><li>正在匯入優惠券</li><li>擷取行銷活動資料</li><li>管理應用程式和端點</li></ul> | `ManagementKey-v1 {YOUR_MANAGEMENT_KEY}` |

## 對應 {#mapping}

若要協助您根據每個特效物件的唯一`effectType`值對應該物件，您可以使用資料準備`array_to_map`函式。 這可讓您輕鬆地將無序效果陣列轉換為符合您需求的機碼值組。 如需指引，請參閱下列範例。

您也可以使用Adobe提供的標準化忠誠度欄位群組，以一致的方式模擬您的忠誠度計畫概念。

>[!BEGINTABS]

>[!TAB 熟客方案詳細資料]

這是XDM個人設定檔的標準XDM欄位群組，用於擷取個人記錄屬性（而非事件資料）來說明個人的熟客會籍狀態。 在您的設定檔結構描述中使用此欄位群組來擷取：

* **誰**&#x200B;成員在方案中(`loyaltyID`， `program`， `status`， `tier`)
* 他們的&#x200B;**目前與期限餘額** （`points`、`lifetimePoints`、`expiredPoints`等）
* 金鑰&#x200B;**會籍日期** (`joinDate`， `upgradeDate`， `tierExpiryDate`)

>[!TAB 熟客活動詳細資料]

「熟客活動詳細資料」欄位群組的設計目的，是擷取事件層級的熟客活動，例如在特定交易中掙得或兌換的點數。 此欄位群組包含`xdm:points`、`xdm:pointsRedeemed`、`xdm:pointsAsOfDate`和`xdm:program`等欄位。 在您的「體驗事件」結構描述中，使用此事件層級欄位群組來擷取：

* **每個事件的移動**&#x200B;點（已取得、已兌換、已到期）
* 由忠誠度優惠券或轉介所帶來的&#x200B;**折扣**
* **方案ID**&#x200B;和交易ID，以便與忠誠度提供者進行調解。

>[!ENDTABS]

| 來源 | 目標 |
| ---- | --- |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsGained[0].promotionId` |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsGained[0].value` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsRedemption[0].promotionId` |
| `array_to_map(data.effects, "effectType").acceptCoupon.campaignId` | `_{TENANT_ID}.loyalty.couponRedemption[0].campaignId` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsRedemption[0].value` |
| `array_to_map(data.effects, "effectType").acceptCoupon.props.value` | `_{TENANT_ID}.loyalty.couponRedemption[0].id` |
| `array_to_map(data.effects, "effectType").setDiscount.campaignId` | `_{TENANT_ID}.loyalty.discounts[0].promotionId` |
| `array_to_map(data.effects, "effectType").setDiscount.props.value` | `_{TENANT_ID}.loyalty.discounts[0].value` |
| `data.created` | `timestamp` |
| `data.attributes.params.profileId` | `personID` |
| `data.attributes.integrationId` | `_id` |
| `data.attributes.params.cartItems[*].name` | `productListItems[*].name` |
| `data.attributes.params.cartItems[*].category` | `productListItems[*].productCategories[0].categoryID` |
| `data.attributes.params.cartItems[*].sku` | `productListItems[*].SKU` |

{style="table-layout:auto"}

## 後續步驟

請閱讀下列檔案，瞭解如何將[!DNL Talon.One]帳戶連結至Experience Platform，並擷取批次和串流忠誠度資料。

* [Talon.One串流事件](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One Batch Source Connector](../../tutorials/ui/create/loyalty/talon-one-batch.md)
