---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目標
title: 電子郵件營銷目標概述
type: Tutorial
description: 電子郵件服務提供商(ESP)允許您管理電子郵件營銷活動，例如發送促銷電子郵件活動。
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 9d2e98c834eddcacf67de7caafef4717e38d80f8
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 4%

---

# 電子郵件營銷目標概述 {#email-marketing-destinations}

## 總覽 {#overview}

電子郵件服務提供商(ESP)使您能夠管理電子郵件營銷活動，如發送促銷電子郵件活動。 Adobe Experience Platform通過允許您將市場細分激活到電子郵件營銷目標與ESP整合。

平台將段導出為 `.csv` 檔案，並將其傳送到首選位置。 計畫從啟用的儲存位置在您的電子郵件營銷平台中導入資料 [!DNL Platform]。 導入資料的過程因每個合作夥伴而異。 有關詳細資訊，請閱讀各個目標項目。

## 支援的電子郵件營銷目標 {#supported-destinations}

Adobe Experience Platform支援以下電子郵件營銷目標：

* [Adobe Campaign](adobe-campaign.md)
* [Oracle雄辯](oracle-eloqua.md)
* [Oracle響應系統](oracle-responsys.md)
* [SalesforceMarketing Cloud](salesforce-marketing-cloud.md)

## 連接到新的電子郵件營銷目標 {#connect-destination}

要將市場活動的市場推廣目標發送到電子郵件，平台必須首先連接到目標。 查看 [目標建立教程](../../ui/connect-destination.md) 的子菜單。

## 將受眾激活到電子郵件營銷目標時的最佳做法 {#best-practices}

### 身份選擇 {#identity}

Adobe建議您從 [聯合架構](../../../profile/home.md#profile-fragments-and-union-schemas)。 這是用戶標識被鎖定的欄位。 最常見的是，此欄位是電子郵件地址，但它也可以是會員計畫ID或電話號碼。 有關架構中最常見的唯一標識符及其XDM欄位，請參閱下表。

| 唯一標識符 | 統一架構中的XDM欄位 |
|----------------- | ---------------------------|
| Email Address | `personalEmail.address` |
| 電話 | `mobilePhone.number` |
| 會員計畫ID | `Customer-defined XDM field` |

### 其他目標屬性

在「架構」欄位選擇器中，選擇要導出到電子郵件目標的其他欄位。 建議的選項包括：

| 方案 | XDM欄位 |
|------ | ---------|
| 「名字」 | `person.name.firstName` |
| 「姓氏」 | `person.name.lastName` |
| 電話 | `mobilePhone.number` |
| 地址城市 | `homeAddress.city` |
| 地址狀態 | `homeAddress.stateProvince` |
| 地址郵遞區號 | `homeAddress.postalCode` |
| 生日 | `person.birthDayAndMonth` |
| 段成員資格 | `segmentMembership.status` |

## 將資料從儲存位置導入目標 {#import-data-into-destination}

閱讀單個電子郵件營銷目標文章，瞭解如何將資料從儲存位置導入目標：

* [Adobe Campaign](adobe-campaign.md)
* [Oracle雄辯](oracle-eloqua.md)
* [Oracle響應系統](oracle-responsys.md)
* [SalesforceMarketing Cloud](salesforce-marketing-cloud.md)

## 激活段以通過電子郵件將營銷目標 {#activate}

有關如何激活市場細分以通過電子郵件發送營銷目標的說明，請參閱 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md)。

## 其他資源

* [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md)
* [使用流服務API建立電子郵件營銷目標並激活資料](../../api/connect-activate-batch-destinations.md)
