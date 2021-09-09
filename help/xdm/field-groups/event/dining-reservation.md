---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；訂房；用餐；
title: 用餐預訂方案欄位組
description: 本檔案提供「餐飲預訂」結構欄位群組的概觀。
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---


# [!UICONTROL Dining ] Reservationschema欄位組

[!UICONTROL Dining Reservation] 是類別的標準結構欄位群組， [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 用於擷取與用餐預訂相關的資訊。

欄位組是[!UICONTROL 保留詳細資訊]欄位組的擴展，在單個對象類型欄位`reservations`下包含所有相同的欄位。 除了這些通用欄位外，[!UICONTROL Dining Reservation]還包括`diningReservations`陣列。 此物件陣列可用來說明具有餐廳特定屬性的一或多個保留。

>[!NOTE]
>
>本文檔涵蓋`diningReservations`陣列的詳細資訊。 有關`reservations`對象下提供的其他欄位的資訊，請參閱[[!UICONTROL 保留詳細資訊]欄位組引用](./reservation-details.md)。

![餐廳預訂結構](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` 是一系列物件，代表餐飲預訂清單。例如，如果預訂事件涉及在一天中不同時間在多個不同餐廳預訂的情況，則這些預訂可以作為單個事件的`diningReservations`下的單個對象列出。

`diningReservations`下提供的每個對象的結構如下。

![diningReservations結構](../../images/field-groups/dining-reservation/diningReservations.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `ID` | 字串 | 保留編號或標識符。 |
| `cancellation` | 整數 | 取消保留時，會擷取此值。 |
| `confirmationNumber` | 字串 | 預訂確認號或標識符。 |
| `created` | 整數 | 建立保留時，會擷取此值。 |
| `cuisine` | 整數 | 餐廳的菜。 |
| `currencyCode` | 字串 | 用於購買的ISO 4217貨幣代碼。 |
| `deliveryPartners` | 字串 | 餐廳提供送貨合作夥伴。 |
| `diningOptions` | 字串 | 餐廳提供送貨和餐飲服務。 |
| `groupReservation` | 布林值 | 指示是否正在對組進行保留。 |
| `length` | 整數 | 保留的總天數。 |
| `loyaltyID` | 字串 | 訂房中所列訪客的忠誠計畫ID。 |
| `modification` | 整數 | 修改保留時，會擷取此值。 |
| `modificationDate` | DateTime | 上次修改保留的時間。 |
| `numberOfAdults` | 整數 | 與保留相關聯的成人人數。 |
| `numberOfChildren` | 整數 | 與保留相關聯的子項數。 |
| `numberOfRooms` | 整數 | 與預訂相關聯的房間數。 |
| `partySize` | 整數 | 在餐會上的人數。 |
| `priceCategory` | 字串 | 正在進行的保留的價格類別。 |
| `purpose` | 字串 | 保留的目的，通常為商業或個人。 |
| `reservationTime` | DateTime | 預訂餐飲預訂的時間。 |
| `restaurantID` | 字串 | 餐廳或用餐地點的標識符。 |
| `reservationStatus` | 字串 | 保留的狀態。 |
| `specialOccasion` | 布林值 | 指出是否正在為特殊場合提出保留。 |
| `status` | 整數 | 餐飲預訂的狀態。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
