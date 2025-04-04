---
solution: Experience Platform
title: 零售業資料模型
description: 檢視適用於零售業的標準化資料模型，此模型與Experience Data Model (XDM)相容，可在Adobe Experience Platform中使用。
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# [!UICONTROL 零售業]產業資料模型

下列實體關係圖(ERD)代表零售業的標準化資料模型。 ERD會刻意以非標準化方式呈現，並考量資料在Adobe Experience Platform中的儲存方式。

>[!NOTE]
>
>說明的ERD是您應如何針對此產業使用案例建立資料模型的建議。 若要在Experience Platform中使用此資料模型，您必須自行建構建議的結構描述及其關係。 如需詳細資訊，請參閱在UI中管理[結構描述](../../ui/resources/schemas.md)和[關係](../../tutorials/relationship-ui.md)的指南。

請使用下列圖例來解譯此ERD：

* 中顯示的每個實體都是以基礎的[體驗資料模型(XDM)類別](../composition.md#class)為基礎。
* 在父欄位下縮排的欄位代表屬於父欄位群組的子欄位或子欄位。
* 指定實體最重要的欄位會以紅色反白顯示。
* 所有可用於識別個別客戶的屬性都會標示為「身分」，而其中一項屬性會標示為「主要身分」。
* 實體關係會標示為非相依關係，因為Cookie型事件通常無法判斷執行交易的人員或個人。

![零售業資料模型的範例ERD](../../images/industries/retail.png)

>[!NOTE]
>
>體驗事件實體包含「_ID」欄位，其代表XDM ExperienceEvent類別所提供的唯一識別碼(`_id`)屬性。 請參閱[XDM ExperienceEvent](../../classes/experienceevent.md)上的參考檔案，以取得這個值預期的詳細資訊。

## [!UICONTROL 零售]使用案例

下表概述幾種常見零售使用案例的建議類別和結構描述欄位群組。

| 使用實例 | 建議的類別和欄位群組 |
| --- | --- |
| 結合線上和離線資料來源，並解析跨裝置和線上/離線身分，以提供整體的跨頻道和跨裝置歸因報表。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[Commerce詳細資料](../../field-groups/event/commerce-details.md)</li><li>[網頁詳細資料](../../field-groups/event/web-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**：<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 為各種區段提供鎖定目標的個人化體驗，以提升收入，並幫助增強全通路協調的平台。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[行銷活動行銷詳細資料](../../field-groups/event/campaign-marketing-details.md)</li><li>[管道詳細資料](../../field-groups/event/channel-details.md)</li><li>[Commerce詳細資料](../../field-groups/event/commerce-details.md)</li><li>[環境詳細資料](../../field-groups/event/environment-details.md)</li><li>[網頁詳細資料](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[個人連絡人詳細資料](../../field-groups/profile/personal-contact-details.md)</li><li>[工作連絡人詳細資料](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 分析多點接觸歸因，以提升行銷效率。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[行銷活動行銷詳細資料](../../field-groups/event/campaign-marketing-details.md)</li><li>[管道詳細資料](../../field-groups/event/channel-details.md)</li><li>[Commerce詳細資料](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| 透過改善男性和女性的區隔來改善電子郵件關聯性。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[Commerce詳細資料](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**：<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 擷取忠誠度（合作夥伴）資料，以提升網路、電子郵件和數位行銷管道的相關產品資訊。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[網頁詳細資料](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[熟客方案詳細資料](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**：<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 透過自動和個人化的電子郵件重新鎖定購物車放棄者。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[Commerce詳細資料](../../field-groups/event/commerce-details.md)</li><li>[網頁詳細資料](../../field-groups/event/web-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**：<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
