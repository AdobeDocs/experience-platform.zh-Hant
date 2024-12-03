---
solution: Experience Platform
title: 旅遊業及旅館業資料模型ERD
description: 檢視實體關係圖(ERD)，其說明適用於旅遊業及旅館業的標準化資料模型，且與Experience Data Model (XDM)相容，以便用於Adobe Experience Platform。
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 23bf89977b13a1f51e1ea7a0bb0561522a09745d
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# [!UICONTROL 旅遊及旅館業]產業資料模型ERD

下列實體關係圖(ERD)代表旅遊業及旅館業的標準化資料模型。 ERD會刻意以非標準化方式呈現，並考量資料在Adobe Experience Platform中的儲存方式。

>[!NOTE]
>
>說明的ERD是您應如何針對此產業使用案例建立資料模型的建議。 若要在Platform中使用此資料模型，您必須自行建構建議的結構描述及其關係。 如需詳細資訊，請參閱在UI中管理[結構描述](../../ui/resources/schemas.md)和[關係](../../tutorials/relationship-ui.md)的指南。

請使用下列圖例來解譯此ERD：

* 中顯示的每個實體都是以基礎的[體驗資料模型(XDM)類別](../composition.md#class)為基礎。
* 在父欄位下縮排的欄位代表屬於父欄位群組的子欄位或子欄位。
* 指定實體最重要的欄位會以紅色反白顯示。
* 所有可用於識別個別客戶的屬性都會標示為「身分」，而其中一項屬性會標示為「主要身分」。
* 實體關係會標示為非相依關係，因為Cookie型事件通常無法判斷執行交易的人員或個人。

![旅遊旅館業資料模型的範例ERD](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>體驗事件實體包含「_ID」欄位，其代表XDM ExperienceEvent類別所提供的唯一識別碼(`_id`)屬性。 請參閱[XDM ExperienceEvent](../../classes/experienceevent.md)上的參考檔案，以取得這個值預期的詳細資訊。

## [!UICONTROL 旅遊及旅館業]個使用案例

下表概述旅遊業及旅館業數個常見使用案例的建議類別和結構描述欄位群組。

| 使用實例 | 建議的類別和欄位群組 |
| --- | --- |
| 向即將預訂飯店的市內賓客和賓客交叉銷售餐飲和其他住家景點。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[預訂詳細資料](../../field-groups/event/reservation-details.md)</li><li>[住宿預訂](../../field-groups/event/lodging-reservation.md)</li><li>[餐飲預訂](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[個人連絡人詳細資料](../../field-groups/profile/personal-contact-details.md)</li><li>[工作連絡人詳細資料](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 追加銷售餐飲和其他住家景點，提供給即將預訂旅館的市內賓客和賓客。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[預訂詳細資料](../../field-groups/event/reservation-details.md)</li><li>[餐飲預訂](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[個人連絡人詳細資料](../../field-groups/profile/personal-contact-details.md)</li><li>[工作連絡人詳細資料](../../field-groups/profile/work-contact-details.md)</li><li>[熟客方案詳細資料](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 將飯店和其他住家景點追加銷售給市場內的賓客和即將預訂飯店的賓客。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[預訂詳細資料](../../field-groups/event/reservation-details.md)</li><li>[住宿預訂](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[個人連絡人詳細資料](../../field-groups/profile/personal-contact-details.md)</li><li>[工作連絡人詳細資料](../../field-groups/profile/work-contact-details.md)</li><li>[熟客方案詳細資料](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 將航班和其他住家景點追加銷售給市場內的賓客和即將預訂旅館的賓客。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[預訂詳細資料](../../field-groups/event/reservation-details.md)</li><li>[航班預訂](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[人口統計詳細資料](../../field-groups/profile/demographic-details.md)</li><li>[個人連絡人詳細資料](../../field-groups/profile/personal-contact-details.md)</li><li>[工作連絡人詳細資料](../../field-groups/profile/work-contact-details.md)</li><li>[熟客方案詳細資料](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
