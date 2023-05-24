---
solution: Experience Platform
title: 金融服務行業資料模型ERD
description: 查看實體關係圖(ERD)，該圖描述銀行、金融服務和保險(BFSI)行業的標準化資料模型。 此資料模型與在Adobe Experience Platform使用的經驗資料模型(XDM)相容。
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 3%

---

# [!UICONTROL 金融服務] 工業資料模型ERD

以下實體關係圖(ERD)代表銀行、金融服務和保險(BFSI)行業的標準化資料模型。 ERD有意以非標準化方式呈現，並考慮資料在Adobe Experience Platform的儲存方式。

>[!NOTE]
>
>如所述，ERD是建議您如何為此行業使用案例建模資料。 要在平台中使用此資料模型，您必須自己構建推薦的架構及其關係。 請參閱管理指南 [模式](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) 的子菜單。

使用以下圖例解釋此ERD:

* 所示各實體均基於 [體驗資料模型(XDM)類](../composition.md#class)。
* 對於給定實體，每行標籤在 **粗** 表示欄位組或資料類型，其提供的相關欄位以未加粗的文本列出。
* 給定實體的最重要欄位以紅色加亮。
* 可用於標識單個客戶的所有屬性都標籤為「identity」，其中一個屬性標籤為「primary identity」。
* 實體關係被標籤為非依賴關係，因為基於cookie的事件通常無法確定執行該事務的人員或個人。

![](../../images/industries/financial.png)

>[!NOTE]
>
>「體驗事件」實體包含「_ID」欄位，該欄位表示唯一標識符(`_id`)由XDM ExperienceEvent類提供的屬性。 請參閱上的參考文檔 [XDM體驗事件](../../classes/experienceevent.md) 的子菜單。

## [!UICONTROL 金融服務] 使用案例

下表概述了幾種常見財務使用情形的推薦類和架構欄位組。

| 使用案例 | 建議的類和欄位組 |
| --- | --- |
| 通過渠道報告洞察和自動化行程，在規模上推動首選段的個性化，以增加對首選獎勵計畫的註冊。 | <ul><li>**[[!UICONTROL 產品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM體驗事件]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 卡操作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 報價請求詳細資訊]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL 存款詳細資訊]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 渠道詳細資訊]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL 餘額轉移]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口結構詳細資訊]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 會員詳細資訊]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 優化跨線上和離線渠道的跨渠道個性化。 | <ul><li>**[[!UICONTROL 產品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM體驗事件]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 渠道詳細資訊]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口結構詳細資訊]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 會員詳細資訊]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 通過利用跨渠道行為分析獲得的洞察力，識別可能導致新產品提供的產品使用模式，來推動新的收入機會。 | <ul><li>**[[!UICONTROL 政策]](../../classes/policy.md)**</li><li>**[[!UICONTROL 產品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM體驗事件]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 卡操作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 支援站點搜索]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL 存款詳細資訊]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 渠道詳細資訊]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口結構詳細資訊]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 會員詳細資訊]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
