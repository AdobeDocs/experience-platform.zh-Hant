---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；ExperienceEvent；欄位；綱要；綱要設計；欄位群組；欄位群組；預訂；住宿；
title: 住宿預訂結構描述欄位群組
description: 瞭解住宿預訂結構描述欄位群組。
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 5%

---

# [!UICONTROL 住宿預訂] 結構描述欄位群組

[!UICONTROL 住宿預訂] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md) 用於擷取和住宿預訂相關的資訊。

欄位群組是 [!UICONTROL 預訂詳細資料] 欄位群組，並在單一物件型別欄位下包含所有相同的欄位， `reservations`. 除了這些通用欄位外， [!UICONTROL 住宿預訂] 也包含 `lodgingReservations` 陣列。 這個物件陣列可用來說明一或多個保留區，以及住宿所獨有的屬性。

>[!NOTE]
>
>本檔案涵蓋 `lodgingReservations` 陣列。 如需底下其他欄位的詳細資訊， `reservations` 物件，請參閱 [[!UICONTROL 預訂詳細資料] 欄位群組參考](./reservation-details.md).

![住宿預訂結構](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` 是一個物件陣列，代表住宿預訂清單。 例如，如果預訂事件涉及旅行路線上多個不同旅館的預訂，則這些預訂可以列為下的個別物件 `lodgingReservations` 用於單一事件。

下提供的每個物件的結構 `lodgingReservations` 提供如下。

![loggingReservations結構](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 飯店房間的平均每日價格。 |
| `lodgingCheckIn` | 物件 | 說明住宿簽到詳細資訊的物件。 包含下列值：<ul><li>`digitalKey`：（整數）表示訪客在簽入時選取使用數位金鑰的時間。</li><li>`earlyCheckInRequested`：（整數）指出訪客要求比正常簽到時間更早簽到的時數。</li><li>`lateCheckInRequested`：（整數）指出訪客要求晚於正常簽到時間簽到的時數。</li><li>`noRoomCheckIn`：（整數）當來賓完成簽入且當時沒有可用聊天室時，會擷取此值。</li><li>`oneRoomCheckIn`：（整數）當僅有一個房間可供使用時，當來賓完成簽入時擷取此值。</li><li>`roomKeys`：（整數）簽到時提供的標準房鑰匙數量。</li><li>`userSelectedRoom`：（布林值）指出房客是否於簽到時選取房間。</li></ul> |
| `rackrate` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 沒有預先預訂安排的當天預訂成本。 |
| `ID` | 字串 | 預訂編號或識別碼。 |
| `agentID` | 字串 | 和飯店預訂相關聯的代理程式ID。 |
| `basePrice` | 字串 | 新增任何折扣前的基準價格。 |
| `bookingID` | 字串 | 和飯店預訂相關聯的預訂ID。 |
| `cancellation` | 整數 | 此值會在預訂取消時擷取。 |
| `checkInDate` | 日期時間 | 訂房的簽到日期。 |
| `checkOutDate` | 日期時間 | 訂房的結帳日期。 |
| `confirmationNumber` | 字串 | 預訂確認編號或識別碼。 |
| `couponCode` | 字串 | 和飯店預訂相關聯的抵用券代碼。 |
| `created` | 整數 | 此值會在建立預訂時擷取。 |
| `currencyCode` | 字串 | 用於進行購買的ISO 4217貨幣代碼。 |
| `discountPercent` | 雙倍 | 和預訂相關聯的折扣百分比。 |
| `freeCancelation` | 布林值 | 指出會議室是否有免費取消原則。 |
| `guestID` | 字串 | 和飯店預訂相關聯的賓客ID。 |
| `length` | 整數 | 預訂的總天數。 |
| `loyaltyID` | 字串 | 預訂中列出的賓客的熟客方案ID。 |
| `modification` | 整數 | 此值會在預訂修改時擷取。 |
| `modificationDate` | 日期時間 | 上次修改預訂的時間。 |
| `numberOfAdults` | 整數 | 和預訂相關聯的成人數量。 |
| `numberOfChildren` | 整數 | 和預訂相關聯的子項數目。 |
| `numberOfRooms` | 整數 | 和預訂相關聯的房間數。 |
| `propertyID` | 字串 | 預訂的飯店或渡假村的識別碼。 |
| `propertyName` | 字串 | 預訂的飯店或度假村的名稱。 |
| `purpose` | 字串 | 預訂的目的，通常為商業或個人目的。 |
| `ratePlan` | 字串 | 房間售出的費率交易。 |
| `refundable` | 布林值 | 指出房間是否可退款。 |
| `reservationStatus` | 字串 | 預訂的狀態。 |
| `roomAccessibilityType` | 字串 | 房間的無障礙型別，例如行動力、聽力或其他。 |
| `roomCapacity` | 整數 | 飯店房間容納的人數。 |
| `roomType` | 字串 | 預訂的房間型別。 |
| `smoking` | 布林值 | 指示房間是否允許吸菸。 |
| `tripType` | 字串 | 表示此預訂是單程旅行、往返還是多城市旅行。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
