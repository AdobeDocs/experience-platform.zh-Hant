---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；ExperienceEvent；欄位；綱要；綱要設計；欄位群組；欄位群組；預訂；就餐；
title: 餐飲預訂結構描述欄位群組
description: 瞭解餐飲預訂結構欄位群組。
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 13%

---

# [!UICONTROL 餐飲預訂]結構描述欄位群組

[!UICONTROL 餐飲預訂]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組，用於擷取餐飲預訂的相關資訊。

欄位群組是[!UICONTROL 保留詳細資料]欄位群組的延伸，且包含單一物件型別欄位`reservations`下的所有相同欄位。 除了這些一般欄位之外，[!UICONTROL 餐飲預訂]也包含`diningReservations`陣列。 這個物件陣列是用來說明一或多個保留區與餐廳特定屬性。

>[!NOTE]
>
>本檔案涵蓋`diningReservations`陣列的詳細資料。 如需`reservations`物件下提供之其他欄位的資訊，請參閱[[!UICONTROL 保留區詳細資料]欄位群組參考](./reservation-details.md)。

![餐飲預訂結構](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations`是代表餐飲預訂清單的物件陣列。 例如，如果預訂事件在一天中的不同時間涉及多個不同餐廳的預訂，則這些預訂可以列為單一事件`diningReservations`下的個別物件。

`diningReservations`下提供的每個物件結構如下。

![diningReservations結構](../../images/field-groups/dining-reservation/diningReservations.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `ID` | 字串 | 預訂編號或識別碼。 |
| `cancellation` | 整數 | 此值會在預訂取消時擷取。 |
| `confirmationNumber` | 字串 | 預訂確認編號或識別碼。 |
| `created` | 整數 | 此值會在建立預訂時擷取。 |
| `cuisine` | 整數 | 餐廳的菜餚型別。 |
| `currencyCode` | 字串 | 用於進行購買的ISO 4217貨幣代碼。 |
| `deliveryPartners` | 字串 | 餐廳可提供宅配合作夥伴。 |
| `diningOptions` | 字串 | 餐廳可提供的宅配和餐飲選項。 |
| `groupReservation` | 布林值 | 指出是否為群組進行預訂。 |
| `length` | 整數 | 預訂的總天數。 |
| `loyaltyID` | 字串 | 預訂中列出的賓客的熟客方案ID。 |
| `modification` | 整數 | 此值會在預訂修改時擷取。 |
| `modificationDate` | 日期時間 | 上次修改預訂的時間。 |
| `numberOfAdults` | 整數 | 和預訂相關聯的成人數量。 |
| `numberOfChildren` | 整數 | 和預訂相關聯的子項數目。 |
| `numberOfRooms` | 整數 | 和預訂相關聯的房間數。 |
| `partySize` | 整數 | 宴會中的人數。 |
| `priceCategory` | 字串 | 正在進行之預訂的價格類別。 |
| `purpose` | 字串 | 預訂的目的，通常為商業或個人目的。 |
| `reservationTime` | 日期時間 | 餐廳訂位時間。 |
| `restaurantID` | 字串 | 餐廳或就餐位置的識別碼。 |
| `reservationStatus` | 字串 | 預訂的狀態。 |
| `specialOccasion` | 布林值 | 表示此預訂是否為特別場合所做。 |
| `status` | 整數 | 餐飲預訂的狀態。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
