---
solution: Experience Platform
title: 金融服務行業資料模型ERD
description: 查看描述銀行、金融服務和保險(BFSI)行業標準化資料模型的實體關係圖(ERD)。 此資料模型與Experience Data Model(XDM)相容，可在Adobe Experience Platform中使用。
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# [!UICONTROL 金融服務] 工業資料模型ERD

以下實體關係圖(ERD)代表銀行、金融服務和保險(BFSI)行業的標準化資料模型。 ERD是刻意以非標準化方式呈現，並考慮資料在Adobe Experience Platform中的儲存方式。

>[!NOTE]
>
>ERD是建議，您應如何為此行業使用案例建立資料模型。 若要在Platform中使用此資料模型，您必須自行建立建議的結構描述及其關係。 請參閱管理指南 [綱要](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) ，以取得詳細資訊。

使用下列圖例來解釋此ERD:

* 中顯示的每個實體均以 [Experience Data Model(XDM)類別](../composition.md#class).
* 對於指定實體，每一行都標有 **粗體** 代表欄位群組或資料類型，其提供的相關欄位以未加粗的文字列於下方。
* 指定實體的最重要欄位會以紅色突出顯示。
* 可用於識別個別客戶的所有屬性都會標示為「身分」，其中一個屬性會標示為「主要身分」。
* 實體關係會標示為不相依，因為以Cookie為基礎的事件通常無法判斷進行交易的人員或個人。

![](../../images/industries/financial.png)

>[!NOTE]
>
>體驗事件實體包含「_ID」欄位，代表唯一識別碼(`_id`)屬性。 請參閱 [XDM ExperienceEvent](../../classes/experienceevent.md) 以取得此值預期值的詳細資訊。

## [!UICONTROL 金融服務] 使用案例

下表概述了幾個常見財務使用案例的建議類和架構欄位組。

| 使用案例 | 建議的類和欄位組 |
| --- | --- |
| 透過全通路報告深入分析和自動化歷程，大規模推動偏好區段的個人化，以增加註冊至偏好獎勵計畫的次數。 | <ul><li>**[[!UICONTROL 產品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 卡片動作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 報價請求詳細資訊]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL 存款詳細資訊]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL 餘額轉移]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口統計詳細資料]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠誠度詳細資料]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 線上上和離線頻道上最佳化跨頻道個人化。 | <ul><li>**[[!UICONTROL 產品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口統計詳細資料]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠誠度詳細資料]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 利用從跨管道行為分析中獲得的洞察力，識別可能導致新產品優惠的產品使用模式，借此創造新的收入機會。 | <ul><li>**[[!UICONTROL 政策]](../../classes/policy.md)**</li><li>**[[!UICONTROL 產品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 卡片動作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 支援網站搜尋]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL 存款詳細資訊]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口統計詳細資料]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠誠度詳細資料]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
