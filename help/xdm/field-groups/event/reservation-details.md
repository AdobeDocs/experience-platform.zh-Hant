---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；經驗事件；欄位；模式；模式；模式設計；欄位組；欄位組；保留詳細資訊；
title: 保留詳細資訊方案欄位組
description: 此文檔提供「保留詳細資訊」架構欄位組的概述。
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 4%

---

# [!UICONTROL 保留詳細資訊] 架構欄位組

[!UICONTROL 保留詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用於捕獲有關保留的資訊，包括長度、修改、可退還狀態和房間數。

欄位組提供單個對象類型欄位， `reservations`。 此對象中包含的屬性在下面進行說明。

![保留詳細資訊結構](../../images/field-groups/reservation-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `nonRefundableAmount` | [貨幣](../../data-types/currency.md) | 標籤為不可退還的預留價格金額。 |
| `transaction` | [交易記錄](../../data-types/transaction.md) | 描述保留的幣種交易記錄。 |
| `id` | 字串 | 保留的唯一標識符。 |
| `cancellation` | 整數 | 取消保留後將捕獲此值。 |
| `confirmationNumber` | 字串 | 保留的確認編號或標識符。 |
| `created` | 整數 | 在建立保留時將捕獲此值。 |
| `currencyCode` | 字串 | 用於進行採購的ISO 4217貨幣代碼。 |
| `endDate` | 日期時間 | 保留的結束下拉、返回或簽出日期。 |
| `length` | 整數 | 保留的總天數。 |
| `modification` | 整數 | 在修改保留後將捕獲此值。 |
| `modificationDate` | 日期時間 | 上次修改保留的時間。 |
| `numberOfAdults` | 整數 | 與保留關聯的成人數。 |
| `numberOfChildren` | 整數 | 與保留關聯的子代數。 |
| `purpose` | 字串 | 預訂的目的，通常為商業或個人。 |
| `startDate` | 日期時間 | 保留的開始提貨、出站或簽入日期。 |
| `triptype` | 字串 | 指示預訂是單程旅行、往返旅行還是多城市旅行。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## 特定於行業的保留欄位組

還有幾個其他標準欄位組擴展了 [!UICONTROL 保留詳細資訊] 特定於行業的使用案例的架構。 有關詳細資訊，請參閱以下文檔：

* [[!UICONTROL 餐廳預訂]](./dining-reservation.md)
* [[!UICONTROL 航班預訂]](./flight-reservation.md)
* [[!UICONTROL 住宿預訂]](./lodging-reservation.md)
