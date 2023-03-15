---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構；結構設計；欄位群組；欄位群組；保留；保留詳細資訊；
title: 保留詳細資訊結構欄位組
description: 本文檔概述了「保留詳細資訊」架構欄位組。
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 4%

---

# [!UICONTROL 保留詳細資訊] 方案欄位組

[!UICONTROL 保留詳細資訊] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用來擷取保留的相關資訊，包括長度、修改、可退還狀態和房間數。

欄位組提供單個對象類型欄位， `reservations`. 此物件中包含的屬性說明如下。

![保留詳細資訊結構](../../images/field-groups/reservation-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `nonRefundableAmount` | [貨幣](../../data-types/currency.md) | 標示為不可退還的保留價格金額。 |
| `transaction` | [交易](../../data-types/transaction.md) | 描述保留的幣種交易記錄。 |
| `id` | 字串 | 保留的唯一標識符。 |
| `cancellation` | 整數 | 取消保留時，會擷取此值。 |
| `confirmationNumber` | 字串 | 預訂的確認號或標識符。 |
| `created` | 整數 | 建立保留時，會擷取此值。 |
| `currencyCode` | 字串 | 用於購買的ISO 4217貨幣代碼。 |
| `endDate` | DateTime | 訂房的結束下拉、回訪或結帳日期。 |
| `length` | 整數 | 保留的總天數。 |
| `modification` | 整數 | 修改保留時，會擷取此值。 |
| `modificationDate` | DateTime | 上次修改保留的時間。 |
| `numberOfAdults` | 整數 | 與保留相關聯的成人人數。 |
| `numberOfChildren` | 整數 | 與保留相關聯的子項數。 |
| `purpose` | 字串 | 保留的目的，通常為商業或個人。 |
| `startDate` | DateTime | 預訂的開始接收、出站或簽入日期。 |
| `triptype` | 字串 | 指出預訂是單程旅行、往返旅行還是多城旅行。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## 特定於行業的保留欄位組

有數個其他標準欄位群組會擴充 [!UICONTROL 保留詳細資訊] 特定產業使用案例的結構描述。 如需詳細資訊，請參閱下列檔案：

* [[!UICONTROL 餐廳預訂]](./dining-reservation.md)
* [[!UICONTROL 航班預訂]](./flight-reservation.md)
* [[!UICONTROL 住宿預訂]](./lodging-reservation.md)
