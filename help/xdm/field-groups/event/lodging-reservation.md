---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；訂房；住宿；
title: 住宿預訂結構欄位組
description: 本檔案提供「住宿預訂」結構欄位組的概述。
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 4%

---


# [!UICONTROL 住宿預] 留方案欄位組

[!UICONTROL 住宿] 預訂是類別的標準結構欄位 [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 群組，用於擷取與住宿預訂相關的資訊。

欄位組是[!UICONTROL 保留詳細資訊]欄位組的擴展，在單個對象類型欄位`reservations`下包含所有相同的欄位。 除了這些通用欄位外，[!UICONTROL Lodging Reservation]還包含`lodgingReservations`陣列。 此對象陣列用於描述一個或多個保留，這些保留具有與倒置特有的屬性。

>[!NOTE]
>
>本文檔涵蓋`lodgingReservations`陣列的詳細資訊。 有關`reservations`對象下提供的其他欄位的資訊，請參閱[[!UICONTROL 保留詳細資訊]欄位組引用](./reservation-details.md)。

![住宿預訂結構](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` 是一個物件陣列，代表lodging保留清單。例如，如果預訂事件涉及沿行程路線在多個不同酒店的預訂，則這些預訂可以作為單個事件的`lodgingReservations`下的單個對象列出。

`lodgingReservations`下提供的每個對象的結構如下。

![lodgingReservations結構](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 酒店房間的平均日價。 |
| `lodgingCheckIn` | 物件 | 描述住宿簽入詳細資訊的對象。 包含下列值：<ul><li>`digitalKey`:（整數）指示來賓何時在簽入時選擇使用數字密鑰。</li><li>`earlyCheckInRequested`:（整數）指示來賓在正常簽入小時之前要求籤入的時間。</li><li>`lateCheckInRequested`:（整數）指示來賓何時要求在正常簽入時間之後簽入。</li><li>`noRoomCheckIn`:（整數）當來賓在當時沒有可用房間時完成簽入時，將捕獲此值。</li><li>`oneRoomCheckIn`:（整數）當來賓在當時只有一個可用房間時完成簽入時，將捕獲此值。</li><li>`roomKeys`:（整數）在簽入時提供的標準房間密鑰數。</li><li>`userSelectedRoom`:（布林值）指示來賓是否在簽入時選擇了其房間。</li></ul> |
| `rackrate` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 當天訂房的費用，無需事先預訂。 |
| `ID` | 字串 | 保留編號或標識符。 |
| `agentID` | 字串 | 與酒店預訂相關聯的代理ID。 |
| `basePrice` | 字串 | 加入任何折扣前的基本價格。 |
| `bookingID` | 字串 | 與酒店預訂相關聯的預訂ID。 |
| `cancellation` | 整數 | 取消保留時，會擷取此值。 |
| `checkInDate` | DateTime | 房間預訂的登記日期。 |
| `checkOutDate` | DateTime | 房間預訂的結帳日期。 |
| `confirmationNumber` | 字串 | 預訂確認號或標識符。 |
| `couponCode` | 字串 | 與酒店預訂相關聯的抵用券代碼。 |
| `created` | 整數 | 建立保留時，會擷取此值。 |
| `currencyCode` | 字串 | 用於購買的ISO 4217貨幣代碼。 |
| `discountPercent` | 雙倍 | 與預訂相關的折扣百分比。 |
| `freeCancelation` | 布林值 | 指示檔案室是否具有免費取消策略。 |
| `guestID` | 字串 | 與酒店預訂相關聯的訪客ID。 |
| `length` | 整數 | 保留的總天數。 |
| `loyaltyID` | 字串 | 訂房中所列訪客的忠誠計畫ID。 |
| `modification` | 整數 | 修改保留時，會擷取此值。 |
| `modificationDate` | DateTime | 上次修改保留的時間。 |
| `numberOfAdults` | 整數 | 與保留相關聯的成人人數。 |
| `numberOfChildren` | 整數 | 與保留相關聯的子項數。 |
| `numberOfRooms` | 整數 | 與預訂相關聯的房間數。 |
| `propertyID` | 字串 | 預訂的酒店或度假村的標識符。 |
| `propertyName` | 字串 | 預訂的酒店或度假村的名稱。 |
| `purpose` | 字串 | 保留的目的，通常為商業或個人。 |
| `ratePlan` | 字串 | 房間的賣價。 |
| `refundable` | 布林值 | 指出該房間是否可退還。 |
| `reservationStatus` | 字串 | 保留的狀態。 |
| `roomAccessibilityType` | 字串 | 房間的無障礙類型，如移動性、聽覺等。 |
| `roomCapacity` | 整數 | 酒店房間的住客人數。 |
| `roomType` | 字串 | 預訂的房間類型。 |
| `smoking` | 布林值 | 指示房間是否允許吸煙。 |
| `tripType` | 字串 | 指出預訂是單程旅行、往返旅行還是多城旅行。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
