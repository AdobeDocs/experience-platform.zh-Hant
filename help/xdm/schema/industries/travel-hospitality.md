---
solution: Experience Platform
title: 旅宿業資料模型ERD
topic-legacy: overview
description: 檢視實體關係圖(ERD)，此圖表說明旅行與旅宿業的標準化資料模型，與Adobe Experience Platform中使用的Experience Data Model(XDM)相容。
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# [!UICONTROL 旅行與住] 宿業資料模型ERD

以下實體關係圖(ERD)代表旅行和旅館業的標準化資料模型。 ERD是刻意以非標準化方式呈現，並考慮資料在Adobe Experience Platform中的儲存方式。

>[!NOTE]
>
>ERD是建議，您應如何為此行業使用案例建立資料模型。 若要在Platform中使用此資料模型，您必須自行建立建議的結構描述及其關係。 如需詳細資訊，請參閱UI中管理[結構](../../ui/resources/schemas.md)和[關係](../../tutorials/relationship-ui.md)的指南。

使用下列圖例來解釋此ERD:

* 中顯示的每個實體都以基礎的[Experience Data Model(XDM)類別](../composition.md#class)為基礎。
* 對於指定實體，在&#x200B;**bold**&#x200B;中標籤的每一行代表欄位組或資料類型，其下提供的相關欄位以未粗體文字列出。
* 指定實體的最重要欄位會以紅色突出顯示。
* 可用於識別個別客戶的所有屬性都會標示為「身分」，其中一個屬性會標示為「主要身分」。
* 實體關係會標示為不相依，因為以Cookie為基礎的事件通常無法判斷進行交易的人員或個人。

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>「體驗事件」實體包含「_ID」欄位，代表XDM ExperienceEvent類別所提供的唯一識別碼(`_id`)屬性。 如需此值預期內容的詳細資訊，請參閱[XDM ExperienceEvent](../../classes/experienceevent.md)上的參考檔案。

## [!UICONTROL 旅行和住] 院使用案例

下表概述了旅行和接待業幾種常見使用案例的建議類別和方案欄位組。

| 使用案例 | 建議的類和欄位組 |
| --- | --- |
| 向即將預訂酒店的市場客人和客人提供交叉銷售的餐飲和其他常駐景點。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[保留詳細資訊](../../field-groups/event/reservation-details.md)</li><li>[住宿預訂](../../field-groups/event/lodging-reservation.md)</li><li>[餐廳預訂](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[個人聯繫人詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯繫人詳細資訊](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 向即將預訂酒店的市場客人和客人提供追加銷售的餐飲和其他常住景點。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[保留詳細資訊](../../field-groups/event/reservation-details.md)</li><li>[餐廳預訂](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[個人聯繫人詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯繫人詳細資訊](../../field-groups/profile/work-contact-details.md)</li><li>[忠誠度詳細資料](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向市場內的客人和即將預訂酒店的客人提供追加銷售的酒店和其他常駐景點。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[保留詳細資訊](../../field-groups/event/reservation-details.md)</li><li>[住宿預訂](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[個人聯繫人詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯繫人詳細資訊](../../field-groups/profile/work-contact-details.md)</li><li>[忠誠度詳細資料](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向即將預訂酒店的市場客人和客人提供追加銷售的航班和其他常住景點。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[保留詳細資訊](../../field-groups/event/reservation-details.md)</li><li>[航班預訂](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[個人聯繫人詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯繫人詳細資訊](../../field-groups/profile/work-contact-details.md)</li><li>[忠誠度詳細資料](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
