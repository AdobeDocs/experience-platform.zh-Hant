---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；經驗事件；欄位；模式；模式；模式設計；欄位組；欄位組；保留；用餐；
title: 用餐預訂方案欄位組
description: 此文檔提供「餐飲預訂」架構欄位組的概述。
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 5%

---

# [!UICONTROL 餐廳預訂] 架構欄位組

[!UICONTROL 餐廳預訂] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用於捕獲有關餐飲預訂的資訊。

欄位組是 [!UICONTROL 保留詳細資訊] 欄位組，並包含單個對象類型欄位下的所有相同欄位， `reservations`。 除了這些泛型欄位， [!UICONTROL 餐廳預訂] 還包括 `diningReservations` 陣列。 此對象陣列用於使用特定於餐廳的屬性描述一個或多個保留。

>[!NOTE]
>
>本文檔介紹 `diningReservations` 陣列。 有關在 `reservations` 對象，請參閱 [[!UICONTROL 保留詳細資訊] 欄位組引用](./reservation-details.md)。

![用餐預訂結構](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` 是一組表示餐位預訂清單的對象。 例如，如果預訂事件涉及在一天的不同時間在多個不同餐館預訂，則這些預訂可以列為在 `diningReservations` 一次性。

下面提供的每個對象的結構 `diningReservations` 清單。

![用餐預訂結構](../../images/field-groups/dining-reservation/diningReservations.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `ID` | 字串 | 保留編號或標識符。 |
| `cancellation` | 整數 | 取消保留後將捕獲此值。 |
| `confirmationNumber` | 字串 | 保留確認編號或標識符。 |
| `created` | 整數 | 在建立保留時捕獲此值。 |
| `cuisine` | 整數 | 餐廳菜類。 |
| `currencyCode` | 字串 | 用於進行採購的ISO 4217貨幣代碼。 |
| `deliveryPartners` | 字串 | 餐廳提供送貨合作夥伴。 |
| `diningOptions` | 字串 | 餐廳提供送餐和餐飲服務。 |
| `groupReservation` | 布林值 | 指示是否正在為組進行保留。 |
| `length` | 整數 | 保留的總天數。 |
| `loyaltyID` | 字串 | 保留中列出的來賓的會員計畫ID。 |
| `modification` | 整數 | 在修改保留後將捕獲此值。 |
| `modificationDate` | 日期時間 | 上次修改保留的時間。 |
| `numberOfAdults` | 整數 | 與保留關聯的成人數。 |
| `numberOfChildren` | 整數 | 與保留關聯的子代數。 |
| `numberOfRooms` | 整數 | 與保留關聯的檔案室數。 |
| `partySize` | 整數 | 用餐宴會的人數。 |
| `priceCategory` | 字串 | 所做保留的價格類別。 |
| `purpose` | 字串 | 預訂的目的，通常為商業或個人。 |
| `reservationTime` | 日期時間 | 預訂餐位的時間。 |
| `restaurantID` | 字串 | 餐廳或用餐地點的標識符。 |
| `reservationStatus` | 字串 | 保留的狀態。 |
| `specialOccasion` | 布林值 | 指示是否為特殊場合進行保留。 |
| `status` | 整數 | 餐飲預訂的狀態。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
