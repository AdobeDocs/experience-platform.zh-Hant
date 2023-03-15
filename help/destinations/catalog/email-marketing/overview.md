---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地
title: 電子郵件行銷目的地概觀
type: Tutorial
description: 電子郵件服務提供者(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件行銷活動。
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: ccbc633bfce8f4f66577b50064c28cfc26cb6dca
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 4%

---

# 電子郵件行銷目的地概觀 {#email-marketing-destinations}

## 總覽 {#overview}

電子郵件服務提供者(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件行銷活動。 Adobe Experience Platform可讓您啟用區段至電子郵件行銷目的地，與ESP整合。

Platform會將您的區段匯出為 `.csv` 檔案，並將其傳送至您偏好的位置。 從中啟用的儲存位置，排程電子郵件行銷平台中的資料匯入 [!DNL Platform]. 匯入資料的程式因各合作夥伴而異。 如需詳細資訊，請參閱個別目的地文章。

## 支援的電子郵件行銷目的地 {#supported-destinations}

Adobe Experience Platform支援下列電子郵件行銷目的地：

* [Adobe Campaign](adobe-campaign.md)
* [Oracle雄辯](oracle-eloqua.md)
* [OracleResponsys](oracle-responsys.md)
* [SalesforceMarketing Cloud](salesforce-marketing-cloud.md)
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

### 其他目標屬性

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

## 將資料從儲存位置匯入目的地 {#import-data-into-destination}

請參閱個別電子郵件行銷目的地文章，了解如何將資料從您的儲存位置匯入目的地：

* [Adobe Campaign](adobe-campaign.md)
* [Oracle雄辯](oracle-eloqua.md)
* [OracleResponsys](oracle-responsys.md)
* [SalesforceMarketing Cloud](salesforce-marketing-cloud.md)

## 啟用區段至電子郵件行銷目的地 {#activate}

如需如何啟用區段至電子郵件行銷目的地的指示，請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md).

## 其他資源

* [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)
* [使用流量服務API建立電子郵件行銷目的地和啟用資料](../../api/connect-activate-batch-destinations.md)
