---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；經驗事件；欄位；模式；模式；模式設計；欄位組；欄位組；保留；飛行；
title: 航班預訂架構欄位組
description: 此文檔提供「航班預訂方案」欄位組的概述。
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 4%

---

# [!UICONTROL 航班預訂] 架構欄位組

[!UICONTROL 航班預訂] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用於捕獲有關航班預訂的資訊。

欄位組是 [!UICONTROL 保留詳細資訊] 欄位組，並包含單個對象類型欄位下的所有相同欄位， `reservations`。 除了這些泛型欄位， [!UICONTROL 航班預訂] 還包括 `flightReservations` 陣列。 該對象陣列用於描述具有航空旅行所特有的屬性的一個或多個預訂。

>[!NOTE]
>
>本文檔介紹 `flightReservations` 陣列。 有關在 `reservations` 對象，請參閱 [[!UICONTROL 保留詳細資訊] 欄位組引用](./reservation-details.md)。

![航班預訂結構](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` 是表示飛行預訂清單的對象陣列。 例如，如果預訂事件涉及對一次旅行中多個連接航班的預訂，則這些預訂可以列為以下各個對象 `flightReservations` 一次性。

下面提供的每個對象的結構 `flightReservations` 清單。

![flightReservations結構](../../images/field-groups/flight-reservation/flightReservations.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `flightCheckIn` | 物件 | 捕獲有關航班登機的詳細資訊。 該對象包括以下屬性：<ul><li>`arrivalAirportCode`:（字串）抵達城市的機場代碼。</li><li>`boardingGroup`:（字串）航空公司特定的登機指令。</li><li>`checkInMethod`:（字串）該方法使用簽入，如計數器、線上、自助服務。</li><li>`checkedBags`:（整數）為航班檢查的包數。</li><li>`checkedPassengers`:（整數）如果同一預訂號碼存在多個乘客，則登記為航班的乘客數。</li><li>`confirmationNumber`:（字串）保留確認號或標識符。</li><li>`departureAirportCode`:（字串）離港市機場代碼。</li><li>`flightNumber`:（字串）正在保留的航班號。</li></ul> |
| `flightStatusSearch` | 物件 | 捕獲搜索航班狀態時返回的詳細資訊。 該對象包括以下屬性：<ul><li>`arrivalAirportCode`:（字串）抵達城市的機場代碼。</li><li>`boardingGroup`:（字串）航空公司特定的登機指令。</li><li>`departureAirportCode`:（字串）離港市機場代碼。</li><li>`departureDate`:（日期時間）正在保留的航班起飛日期。</li><li>`flightNumber`:（字串）正在保留的航班號。</li><li>`searchCount`:（整數）搜索保留航班狀態的次數。</li></ul> |
| `agentID` | 字串 | 負責預訂預訂的代理或預訂者（如果適用）。 |
| `aircraftID` | 字串 | 飛機的標識符。 |
| `aircraftType` | 字串 | 飛機的類型。 |
| `arrivalAirportCode` | 字串 | 抵達城市的機場代碼。 |
| `arrivalDate` | 日期時間 | 預定航班的到達日期。 |
| `cancellation` | 整數 | 取消保留後將捕獲此值。 |
| `confirmationNumber` | 字串 | 保留確認編號或標識符。 |
| `created` | 字串 | 在建立保留時捕獲此值。 |
| `currencyCode` | 字串 | 用於進行採購的ISO 4217貨幣代碼。 |
| `departureAirportCode` | 字串 | 出發城的機場代碼。 |
| `departureDate` | 日期時間 | 預定航班的起飛日期。 |
| `fareClass` | 字串 | 正在預訂的航班的票價等級。 |
| `flightNumber` | 字串 | 正在預訂的航班號。 |
| `length` | 整數 | 保留的總天數。 |
| `loyaltyID` | 字串 | 保留中列出的乘客的忠誠或獎勵計畫ID。 |
| `modification` | 整數 | 在修改保留後將捕獲此值。 |
| `modificationDate` | 日期時間 | 上次修改保留的時間。 |
| `numberOfAdults` | 整數 | 與保留關聯的成人數。 |
| `numberOfChildren` | 整數 | 與保留關聯的子代數。 |
| `passengerID` | 字串 | 與預訂關聯的乘客資訊。 |
| `purpose` | 字串 | 預訂的目的，通常為商業或個人。 |
| `salesChannel` | 字串 | 預訂的銷售渠道。 |
| `securityScreening` | 字串 | 對乘客進行安全檢查的類型。 |
| `status` | 字串 | 航班預訂的狀態。 |
| `ticketNumber` | 字串 | 保留編號或標識符。 |
| `tripType` | 字串 | 指示預訂是單程旅行、往返旅行還是多城市旅行。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
