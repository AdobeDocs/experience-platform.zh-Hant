---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；訂房；投放；
title: 飛行預定架構欄位組
description: 本文檔提供「飛行預定」架構欄位組的概述。
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 4%

---


# [!UICONTROL 飛行] 預留方案欄位組

[!UICONTROL 飛行] 預訂是類別的標準架構欄位 [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 群組，用於擷取有關飛行預訂的資訊。

欄位組是[!UICONTROL 保留詳細資訊]欄位組的擴展，在單個對象類型欄位`reservations`下包含所有相同的欄位。 除了這些通用欄位外，[!UICONTROL 飛行預留]還包括`flightReservations`陣列。 該對象陣列用於描述具有航空旅行特有的屬性的一個或多個保留。

>[!NOTE]
>
>本文檔涵蓋`flightReservations`陣列的詳細資訊。 有關`reservations`對象下提供的其他欄位的資訊，請參閱[[!UICONTROL 保留詳細資訊]欄位組引用](./reservation-details.md)。

![飛行預訂結構](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` 是表示飛行保留清單的對象陣列。如果預訂事件涉及對一次行程中的多個連接航班的預訂，例如，對於單個事件，這些預訂可以列為`flightReservations`下的單個對象。

`flightReservations`下提供的每個對象的結構如下。

![flightReservations結構](../../images/field-groups/flight-reservation/flightReservations.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `flightCheckIn` | 物件 | 捕獲有關飛行登錄的詳細資訊。 物件包含下列屬性：<ul><li>`arrivalAirportCode`:（字串）到達城市的機場代碼。</li><li>`boardingGroup`:（字串）航空公司特有的登機順序指標。</li><li>`checkInMethod`:（字串）簽入的方法，例如計數器、線上、資訊站或自助服務。</li><li>`checkedBags`:（整數）為飛行檢查的袋數。</li><li>`checkedPassengers`:（整數）登記為航班的乘客人數，如果同一預訂號有多名乘客。</li><li>`confirmationNumber`:（字串）訂房確認號碼或識別碼。</li><li>`departureAirportCode`:（字串）出發城市的機場代碼。</li><li>`flightNumber`:（字串）要保留的航班號。</li></ul> |
| `flightStatusSearch` | 物件 | 捕獲搜索航班狀態時返回的詳細資訊。 物件包含下列屬性：<ul><li>`arrivalAirportCode`:（字串）到達城市的機場代碼。</li><li>`boardingGroup`:（字串）航空公司特有的登機順序指標。</li><li>`departureAirportCode`:（字串）出發城市的機場代碼。</li><li>`departureDate`:(DateTime)要保留的航班出發日期。</li><li>`flightNumber`:（字串）要保留的航班號。</li><li>`searchCount`:（整數）搜索預留飛行狀態的次數。</li></ul> |
| `agentID` | 字串 | 負責預訂預訂的代理或預訂者（如果適用）。 |
| `aircraftID` | 字串 | 飛機的標識符。 |
| `aircraftType` | 字串 | 飛機的類型。 |
| `arrivalAirportCode` | 字串 | 到達城市的機場代碼。 |
| `arrivalDate` | DateTime | 預定的航班到達日期。 |
| `cancellation` | 整數 | 取消保留時，會擷取此值。 |
| `confirmationNumber` | 字串 | 預訂確認號或標識符。 |
| `created` | 字串 | 建立保留時，會擷取此值。 |
| `currencyCode` | 字串 | 用於購買的ISO 4217貨幣代碼。 |
| `departureAirportCode` | 字串 | 出發城的機場代碼。 |
| `departureDate` | DateTime | 預定航班的出發日期。 |
| `fareClass` | 字串 | 預訂的航班票價。 |
| `flightNumber` | 字串 | 要保留的航班號。 |
| `length` | 整數 | 保留的總天數。 |
| `loyaltyID` | 字串 | 訂房中所列乘客的忠誠度或獎勵方案ID。 |
| `modification` | 整數 | 修改保留時，會擷取此值。 |
| `modificationDate` | DateTime | 上次修改保留的時間。 |
| `numberOfAdults` | 整數 | 與保留相關聯的成人人數。 |
| `numberOfChildren` | 整數 | 與保留相關聯的子項數。 |
| `passengerID` | 字串 | 與預訂相關聯的乘客資訊。 |
| `purpose` | 字串 | 保留的目的，通常為商業或個人。 |
| `salesChannel` | 字串 | 預訂所在的銷售管道。 |
| `securityScreening` | 字串 | 對乘客進行安全檢查的類型。 |
| `status` | 字串 | 航班預訂的狀態。 |
| `ticketNumber` | 字串 | 保留編號或標識符。 |
| `tripType` | 字串 | 指出預訂是單程旅行、往返旅行還是多城旅行。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
