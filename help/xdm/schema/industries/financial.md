---
solution: Experience Platform
title: 金融服務業資料模型ERD
description: 檢視實體關係圖(ERD)，該圖描述銀行、金融服務和保險(BFSI)產業的標準化資料模型。 此資料模型與Adobe Experience Platform中使用的Experience Data Model (XDM)相容。
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# [!UICONTROL 金融服務]產業資料模型ERD

下列實體關係圖(ERD)代表銀行、金融服務和保險(BFSI)產業的標準資料模型。 ERD會刻意以非標準化方式呈現，並考量資料在Adobe Experience Platform中的儲存方式。

>[!NOTE]
>
>說明的ERD是您應如何針對此產業使用案例建立資料模型的建議。 若要在Experience Platform中使用此資料模型，您必須自行建構建議的結構描述及其關係。 如需詳細資訊，請參閱在UI中管理[結構描述](../../ui/resources/schemas.md)和[關係](../../tutorials/relationship-ui.md)的指南。

請使用下列圖例來解譯此ERD：

* 中顯示的每個實體都是以基礎的[體驗資料模型(XDM)類別](../composition.md#class)為基礎。
* 在父欄位下縮排的欄位代表屬於父欄位群組的子欄位或子欄位。
* 指定實體最重要的欄位會以紅色反白顯示。
* 所有可用於識別個別客戶的屬性都會標示為「身分」，而其中一項屬性會標示為「主要身分」。
* 實體關係會標示為非相依關係，因為Cookie型事件通常無法判斷執行交易的人員或個人。

![金融產業資料模型的範例ERD](../../images/industries/financial.png)

>[!NOTE]
>
>體驗事件實體包含「_ID」欄位，其代表XDM ExperienceEvent類別所提供的唯一識別碼(`_id`)屬性。 請參閱[XDM ExperienceEvent](../../classes/experienceevent.md)上的參考檔案，以取得這個值預期的詳細資訊。

## [!UICONTROL 金融服務]使用案例

下表概述幾種常見財務使用案例的建議類別和結構描述欄位群組。

| 使用實例 | 建議的類別和欄位群組 |
| --- | --- |
| 透過全通道報告深入分析和自動化歷程，大規模推動偏好區段的個人化，以增加偏好獎勵計畫的註冊。 | <ul><li>**[[!UICONTROL 產品]](../../classes/product.md)**：<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 卡片動作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 報價請求詳細資料]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL 存款詳細資料]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL 餘額轉帳]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**：<ul><li>[[!UICONTROL 人口統計詳細資料]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人連絡人詳細資料]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 熟客方案詳細資料]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 跨線上和離線頻道最佳化跨頻道個人化。 | <ul><li>**[[!UICONTROL 產品]](../../classes/product.md)**：<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**：<ul><li>[[!UICONTROL 人口統計詳細資料]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人連絡人詳細資料]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 熟客方案詳細資料]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 透過使用從跨管道行為分析獲得的見解，識別可能導致新產品選件的產品使用模式，推動新的收入機會。 | <ul><li>**[[!UICONTROL 原則]](../../classes/policy.md)**</li><li>**[[!UICONTROL 產品]](../../classes/product.md)**：<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 卡片動作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 支援網站搜尋]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL 存款詳細資料]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**：<ul><li>[[!UICONTROL 人口統計詳細資料]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人連絡人詳細資料]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 熟客方案詳細資料]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
