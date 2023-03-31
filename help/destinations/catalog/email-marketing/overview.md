---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地
title: 電子郵件行銷目的地概觀
type: Tutorial
description: 電子郵件服務提供者(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件行銷活動。 了解哪些ESP是受支援的Experience Platform目的地。
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d6ea94b275ab0ed7c0638200188fe7ada7bacf5c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 4%

---

# 電子郵件行銷目的地概觀 {#email-marketing-destinations}

## 總覽 {#overview}

電子郵件服務提供者(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件行銷活動。 Adobe Experience Platform可讓您啟用區段至電子郵件行銷目的地，與ESP整合。

## 支援的電子郵件行銷目的地 {#supported-destinations}

Adobe Experience Platform支援下列電子郵件行銷目的地：

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [(API)OracleEloqua](oracle-eloqua-api.md)
* [(API)SalesforceMarketing Cloud](salesforce-marketing-cloud-exact-target.md)
* [（檔案）OracleEloqua](oracle-eloqua.md)
* [（檔案）SalesforceMarketing Cloud](salesforce-marketing-cloud.md)
* [OracleResponsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## 連線至新的電子郵件行銷目的地 {#connect-destination}

若要傳送區段至您促銷活動的電子郵件行銷目的地，Platform必須先連線至目的地。 請參閱 [目的地建立教學課程](../../ui/connect-destination.md) 以了解設定新目的地的詳細資訊。

## 將受眾啟用至電子郵件行銷目的地的最佳實務 {#best-practices}

### 身份選擇 {#identity}

Adobe建議您從 [聯合方案](../../../profile/home.md#profile-fragments-and-union-schemas). 這是您的使用者身分識別所擷取的欄位。 最常見的欄位是電子郵件地址，但也可以是忠誠計畫ID或電話號碼。 如需架構中最常見的唯一識別碼及其XDM欄位，請參閱下表。

| 唯一識別碼 | 統一架構中的XDM欄位 |
|----------------- | ---------------------------|
| Email Address | `personalEmail.address` |
| 電話 | `mobilePhone.number` |
| 忠誠計畫ID | `Customer-defined XDM field` |

{style="table-layout:auto"}

### 其他目標屬性 {#other-destination-attributes}

在「結構」欄位選取器中，選擇要匯出至電子郵件目的地的其他欄位。 建議的選項有：

| 方案 | XDM欄位 |
|------ | ---------|
| 「名字」 | `person.name.firstName` |
| 「姓氏」 | `person.name.lastName` |
| 電話 | `mobilePhone.number` |
| 地址城市 | `homeAddress.city` |
| 地址狀態 | `homeAddress.stateProvince` |
| 地址郵遞區號 | `homeAddress.postalCode` |
| 生日 | `person.birthDayAndMonth` |
| 區段成員資格 | `segmentMembership.status` |

{style="table-layout:auto"}

## 啟用區段至電子郵件行銷目的地 {#activate}

目錄中的某些電子郵件行銷目的地會透過與目的地的API整合，以串流方式匯出設定檔。

其他目標會將檔案匯出至雲端儲存空間位置。 匯出完成後，您需要將資料從雲端儲存空間匯入電子郵件行銷目的地。

請遵循 [支援電子郵件行銷目的地](#supported-destinations) 區段，了解如何為每個電子郵件行銷目的地啟用區段。

## 其他資源 {#additional-resources}

* [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)
* [使用流量服務API建立電子郵件行銷目的地和啟用資料](../../api/connect-activate-batch-destinations.md)
