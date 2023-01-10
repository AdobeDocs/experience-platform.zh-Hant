---
solution: Experience Platform
title: 零售業資料模型
description: 檢視與Experience Data Model(XDM)相容、可在Adobe Experience Platform中使用的零售業標準化資料模型。
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 2%

---

# [!UICONTROL 零售] 產業資料模型

以下實體關係圖(ERD)代表零售行業的標準化資料模型。 ERD是刻意以非標準化方式呈現，並考慮資料在Adobe Experience Platform中的儲存方式。

>[!NOTE]
>
>ERD是建議，您應如何為此行業使用案例建立資料模型。 若要在Platform中使用此資料模型，您必須自行建立建議的結構描述及其關係。 請參閱管理指南 [綱要](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) ，以取得詳細資訊。

使用下列圖例來解釋此ERD:

* 中顯示的每個實體均以 [Experience Data Model(XDM)類別](../composition.md#class).
* 對於指定實體，每一行都標有 **粗體** 代表欄位群組或資料類型，其提供的相關欄位以未加粗的文字列於下方。
* 指定實體的最重要欄位會以紅色突出顯示。
* 可用於識別個別客戶的所有屬性都會標示為「身分」，其中一個屬性會標示為「主要身分」。
* 實體關係會標示為不相依，因為以Cookie為基礎的事件通常無法判斷進行交易的人員或個人。

![](../../images/industries/retail.png)

>[!NOTE]
>
>體驗事件實體包含「_ID」欄位，代表唯一識別碼(`_id`)屬性。 請參閱 [XDM ExperienceEvent](../../classes/experienceevent.md) 以取得此值預期值的詳細資訊。

## [!UICONTROL 零售] 使用案例

下表概述了幾種常見零售使用案例的建議類別和架構欄位群組。

| 使用案例 | 建議的類和欄位組 |
| --- | --- |
| 結合線上和離線資料來源，解決跨裝置和線上/離線身分識別問題，提供全方位的跨管道和跨裝置歸因報表。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[商務詳細資訊](../../field-groups/event/commerce-details.md)</li><li>[Web詳細資訊](../../field-groups/event/web-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**:<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 為各個區段提供有針對性的個人化體驗，以增加收入，並協助在全通路協調中增強平台。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[促銷活動行銷詳細資料](../../field-groups/event/campaign-marketing-details.md)</li><li>[管道詳細資料](../../field-groups/event/channel-details.md)</li><li>[商務詳細資訊](../../field-groups/event/commerce-details.md)</li><li>[環境詳細資訊](../../field-groups/event/environment-details.md)</li><li>[Web詳細資訊](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[個人聯繫人詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯繫人詳細資訊](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 分析多點接觸歸因，以提高行銷效率。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[促銷活動行銷詳細資料](../../field-groups/event/campaign-marketing-details.md)</li><li>[管道詳細資料](../../field-groups/event/channel-details.md)</li><li>[商務詳細資訊](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| 改善男性和女性的細分，提高電子郵件的相關性。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[商務詳細資訊](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**:<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 內嵌忠誠度（合作夥伴）資料，以增加網路、電子郵件和數位行銷管道中的相關產品資訊。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Web詳細資訊](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[忠誠度詳細資料](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**:<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 透過自動化和個人化電子郵件重新鎖定購物車放棄者。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[商務詳細資訊](../../field-groups/event/commerce-details.md)</li><li>[Web詳細資訊](../../field-groups/event/web-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**:<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

*\*雖然規劃未來版本的標準產品類別，但目前必須使用自訂類別來建置產品結構。 因此，您必須手動建立架構類別的結構，以及您新增至架構之任何欄位群組的結構。 請參閱 [建立自訂類別](../../ui/resources/classes.md#create) （位於XDM UI指南中）以取得詳細資訊。*
