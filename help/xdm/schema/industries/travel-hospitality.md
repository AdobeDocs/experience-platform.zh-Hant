---
solution: Experience Platform
title: 旅遊和酒店業資料模型ERD
description: 查看實體關係圖(ERD)，該圖描述了與在Adobe Experience Platform使用的經驗資料模型(XDM)相容的旅行和酒店業的標準化資料模型。
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 3%

---

# [!UICONTROL 旅行和招待] 工業資料模型ERD

以下實體關係圖(ERD)代表旅行和接待業的標準化資料模型。 ERD有意以非標準化方式呈現，並考慮資料在Adobe Experience Platform的儲存方式。

>[!NOTE]
>
>如所述，ERD是建議您如何為此行業使用案例建模資料。 要在平台中使用此資料模型，您必須自己構建推薦的架構及其關係。 請參閱管理指南 [模式](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) 的子菜單。

使用以下圖例解釋此ERD:

* 所示各實體均基於 [體驗資料模型(XDM)類](../composition.md#class)。
* 對於給定實體，每行標籤在 **粗** 表示欄位組或資料類型，其提供的相關欄位以未加粗的文本列出。
* 給定實體的最重要欄位以紅色加亮。
* 可用於標識單個客戶的所有屬性都標籤為「identity」，其中一個屬性標籤為「primary identity」。
* 實體關係被標籤為非依賴關係，因為基於cookie的事件通常無法確定執行該事務的人員或個人。

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>「體驗事件」實體包含「_ID」欄位，該欄位表示唯一標識符(`_id`)由XDM ExperienceEvent類提供的屬性。 請參閱上的參考文檔 [XDM體驗事件](../../classes/experienceevent.md) 的子菜單。

## [!UICONTROL 旅行和招待] 使用案例

下表概述了旅行和接待業幾種常見使用案例的推薦類和模式欄位組。

| 使用案例 | 建議的類和欄位組 |
| --- | --- |
| 向市場內的客人和即將預訂酒店的客人交叉銷售餐飲和其他常駐景點。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[保留詳細資訊](../../field-groups/event/reservation-details.md)</li><li>[住宿預訂](../../field-groups/event/lodging-reservation.md)</li><li>[餐廳預訂](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM 個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口結構詳細資訊](../../field-groups/profile/demographic-details.md)</li><li>[個人聯繫人詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯繫人詳細資訊](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 向市場內的客人和即將預訂酒店的客人追加銷售餐飲和其他常駐景點。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[保留詳細資訊](../../field-groups/event/reservation-details.md)</li><li>[餐廳預訂](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM 個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口結構詳細資訊](../../field-groups/profile/demographic-details.md)</li><li>[個人聯繫人詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯繫人詳細資訊](../../field-groups/profile/work-contact-details.md)</li><li>[會員詳細資訊](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向市場內的客人和即將預訂酒店的客人追加銷售酒店和其他常駐景點。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[保留詳細資訊](../../field-groups/event/reservation-details.md)</li><li>[住宿預訂](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM 個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口結構詳細資訊](../../field-groups/profile/demographic-details.md)</li><li>[個人聯繫人詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯繫人詳細資訊](../../field-groups/profile/work-contact-details.md)</li><li>[會員詳細資訊](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向市場內的客人和即將預訂酒店的客人追加銷售航班和其他常駐景點。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[保留詳細資訊](../../field-groups/event/reservation-details.md)</li><li>[航班預訂](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM 個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口結構詳細資訊](../../field-groups/profile/demographic-details.md)</li><li>[個人聯繫人詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯繫人詳細資訊](../../field-groups/profile/work-contact-details.md)</li><li>[會員詳細資訊](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
