---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；訂房；用餐；
title: 用餐預訂方案欄位組
description: 本檔案提供「餐飲預訂」結構欄位群組的概觀。
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 5%

---

# [!UICONTROL 餐廳預訂] 方案欄位組

[!UICONTROL 餐廳預訂] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用來擷取有關餐飲預訂的資訊。

欄位群組是 [!UICONTROL 保留詳細資訊] 欄位組，並在單個對象類型欄位下包含所有相同的欄位， `reservations`. 除了這些通用欄位， [!UICONTROL 餐廳預訂] 也包括 `diningReservations` 陣列。 此物件陣列可用來說明具有餐廳特定屬性的一或多個保留。

>[!NOTE]
>
>本檔案說明 `diningReservations` 陣列。 欲知下方提供的其他欄位 `reservations` 物件，請參閱 [[!UICONTROL 保留詳細資訊] 欄位群組參考](./reservation-details.md).

![餐廳預訂結構](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` 是一系列物件，代表餐飲預訂清單。 例如，如果訂房事件涉及一天中不同時間在多家不同餐廳預訂的情況，則這些預訂可以列為下方的個別對象 `diningReservations` 的URL。

下方提供之每個物件的結構 `diningReservations` 如下所示。

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

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
