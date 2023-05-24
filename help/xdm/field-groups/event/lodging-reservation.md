---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；經驗事件；欄位；模式；模式；模式設計；欄位組；欄位組；保留；住宿；
title: 寄宿預留方案欄位組
description: 此文檔提供「住宿預留方案」欄位組的概述。
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 5%

---

# [!UICONTROL 住宿預訂] 架構欄位組

[!UICONTROL 住宿預訂] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用於捕獲有關住宿預訂的資訊。

欄位組是 [!UICONTROL 保留詳細資訊] 欄位組，並包含單個對象類型欄位下的所有相同欄位， `reservations`。 除了這些泛型欄位， [!UICONTROL 住宿預訂] 還包括 `lodgingReservations` 陣列。 此對象陣列用於描述具有唯一於lodging的屬性的一個或多個保留。

>[!NOTE]
>
>本文檔介紹 `lodgingReservations` 陣列。 有關在 `reservations` 對象，請參閱 [[!UICONTROL 保留詳細資訊] 欄位組引用](./reservation-details.md)。

![住宿預訂結構](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` 是表示lodging保留清單的對象陣列。 例如，如果預訂事件涉及沿行程路線在多個不同酒店的預訂，則這些預訂可以作為單獨的對象列在 `lodgingReservations` 一次性。

下面提供的每個對象的結構 `lodgingReservations` 清單。

![lodgingReservations結構](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 酒店房間的日均價格。 |
| `lodgingCheckIn` | 物件 | 描述住宿簽入詳細資訊的對象。 包括以下值：<ul><li>`digitalKey`:（整數）指示來賓在簽入時選擇使用數字密鑰的時間。</li><li>`earlyCheckInRequested`:（整數）指示來賓請求在正常簽入小時之前簽入的時間。</li><li>`lateCheckInRequested`:（整數）指示來賓請求在正常簽入小時後簽入的時間。</li><li>`noRoomCheckIn`:（整數）當來賓完成簽入時，當時沒有可用的工作室時，將捕獲此值。</li><li>`oneRoomCheckIn`:（整數）當來賓完成簽入時，此時只有一個可用房間時，將捕獲此值。</li><li>`roomKeys`:（整數）簽入時提供的標準房間密鑰數。</li><li>`userSelectedRoom`:（布爾值）指示來賓是否在簽入時選擇了其房間。</li></ul> |
| `rackrate` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 當天預訂的費用，無需事先預訂。 |
| `ID` | 字串 | 保留編號或標識符。 |
| `agentID` | 字串 | 與酒店預訂關聯的座席ID。 |
| `basePrice` | 字串 | 添加任何折扣前的基價。 |
| `bookingID` | 字串 | 與酒店預訂關聯的預訂ID。 |
| `cancellation` | 整數 | 取消保留後將捕獲此值。 |
| `checkInDate` | 日期時間 | 房間預訂的登記日期。 |
| `checkOutDate` | 日期時間 | 房間預訂的退房日期。 |
| `confirmationNumber` | 字串 | 保留確認編號或標識符。 |
| `couponCode` | 字串 | 與酒店預訂相關聯的優惠券代碼。 |
| `created` | 整數 | 在建立保留時捕獲此值。 |
| `currencyCode` | 字串 | 用於進行採購的ISO 4217貨幣代碼。 |
| `discountPercent` | 雙倍 | 與預訂關聯的折扣百分比。 |
| `freeCancelation` | 布林值 | 指示檔案室是否具有免費取消策略。 |
| `guestID` | 字串 | 與酒店預訂關聯的來賓ID。 |
| `length` | 整數 | 保留的總天數。 |
| `loyaltyID` | 字串 | 保留中列出的來賓的會員計畫ID。 |
| `modification` | 整數 | 在修改保留後將捕獲此值。 |
| `modificationDate` | 日期時間 | 上次修改保留的時間。 |
| `numberOfAdults` | 整數 | 與保留關聯的成人數。 |
| `numberOfChildren` | 整數 | 與保留關聯的子代數。 |
| `numberOfRooms` | 整數 | 與保留關聯的檔案室數。 |
| `propertyID` | 字串 | 預訂的酒店或度假村的標識符。 |
| `propertyName` | 字串 | 預訂的酒店或度假村的名稱。 |
| `purpose` | 字串 | 預訂的目的，通常為商業或個人。 |
| `ratePlan` | 字串 | 房間的售價協定。 |
| `refundable` | 布林值 | 指示檔案室是否可退還。 |
| `reservationStatus` | 字串 | 保留的狀態。 |
| `roomAccessibilityType` | 字串 | 房間的輔助功能類型，如移動、聽力或其他。 |
| `roomCapacity` | 整數 | 酒店房間的人數。 |
| `roomType` | 字串 | 正在保留的房間類型。 |
| `smoking` | 布林值 | 指示房間是否允許吸煙。 |
| `tripType` | 字串 | 指示預訂是單程旅行、往返旅行還是多城市旅行。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
