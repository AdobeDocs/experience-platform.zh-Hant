---
title: 電子郵件行銷目標
seo-title: 電子郵件行銷目標
description: 電子郵件服務供應商(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件促銷活動。
seo-description: 電子郵件服務供應商(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件促銷活動。
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# 電子郵件行銷目標 {#email-marketing-destinations}

電子郵件服務供應商(ESP)可讓您管理電子郵件行銷活動，例如傳送促銷電子郵件宣傳。 Adobe即時客戶資料平台可讓您將區段啟用至電子郵件行銷目的地，與ESP整合。

若要將區段傳送至行銷活動的電子郵件目的地，Adobe即時CDP必須先連線至目的地。

連線至電子郵件行銷目的地是三步驟。 本頁將進一步說明每個步驟。

在連接目標流中（如下節所述），連接到Amazon S3或SFTP。 即時CDP將您的細分導出為 `.csv` 或文 `.txt` 件，並將其發送到您的首選位置。 從即時CDP中啟用的儲存位置，排程您在電子郵件行銷平台中的資料匯入。 匯入資料的程式會因每個合作夥伴而異。 如需詳細資訊，請參閱個別的目標文章。

## 步驟1 —— 連接目標 {#connect-destination}

1. 在 **[!UICONTROL Connections > Destinations]**&#x200B;中，選擇您要連線的電子郵件行銷目標，然後選擇 **[!UICONTROL Connect destination]**。

   ![連接到目標](/help/rtcdp/destinations/assets/connect-destination.png)

2. 在[連接]嚮導中，選擇 **[!UICONTROL Connection type]** 儲存位置。 您可以在 **Amazon S3**、 **SFTP with Password**、 **SFTP with SSH Key之間進行選擇**。 根據您的連線類型，填入下列資訊，然後選取 **[!UICONTROL Connect]**。

對 **於S3連線**，您必須提供存取金鑰ID和機密存取金鑰。

對於 **具有密碼連接的SFTP** ，必須提供域、埠、用戶名和密碼。

對於 **具有SSH密鑰連接的SFTP** ，必須提供域、埠、用戶名和SSH密鑰。

## 步驟2 —— 選擇在導出的檔案中用作目標屬性的架構欄位 {#destination-attributes}

在此步驟中，您會選取要匯出至電子郵件行銷目的地的欄位。

![目標屬性](/help/rtcdp/destinations/assets/destination-attributes.png)

### 身份 {#identity}

建議您從聯合架構中選擇唯一 [標識符](../../profile/home.md#profile-fragments-and-union-schemas)。 這是您使用者身分識別的欄位。 最常見的欄位是電子郵件地址，但也可以是忠誠度方案ID或電話號碼。 請參見下表，以瞭解統一架構中最常見的唯一標識符及其XDM欄位。

| 唯一識別碼 | 統一模式中的XDM欄位 |
---------|----------
| 電子郵件地址 | `personalEmail.address` |
| 電話 | `mobilePhone.number` |
| 忠誠度方案ID | `Customer-defined XDM field` |

### 其他目標屬性

在「結構」欄位選擇器中，選擇要匯出至電子郵件目的地的其他欄位。 建議的選項包括：

| 架構 | XDM欄位 |
---------|----------
| 「名字」 | `person.name.firstName` |
| 「姓氏」 | `person.name.lastName` |
| 電話 | `mobilePhone.number` |
| 地址城市 | `homeAddress.city` |
| 地址狀態 | `homeAddress.stateProvince` |
| 地址郵遞區號 | `homeAddress.postalCode` |
| 生日 | `person.birthDayAndMonth` |

## 步驟3 —— 將資料從儲存位置匯入目的地

請參閱個別電子郵件行銷目標文章，瞭解如何將資料從儲存位置匯入目標：

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Exovila](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## 啟用區段至電子郵件行銷目標

如需如何啟用區段至電子郵件行銷目的地的指示，請參閱啟 [用資料至目的地](/help/rtcdp/destinations/activate-destinations.md)。