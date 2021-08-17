---
keywords: 電子郵件；電子郵件；電子郵件目的地；oracle雄辯；oracle
title: OracleEloqua連線
description: OracleEloqua是Oracle提供的軟體即服務(SaaS)平台，用於實現行銷自動化，旨在幫助B2B行銷人員和組織管理行銷活動和銷售機會的產生。
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# [!DNL Oracle Eloqua] 連接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 是軟體即服務(SaaS)平台，提供行銷自動化功能， [!DNL Oracle] 旨在協助B2B行銷人員和組織管理行銷活動和銷售機會開發。

若要將區段資料傳送至[!DNL Oracle Eloqua]，您必須先[連接Adobe Experience Platform中的目標](#connect-destination)，然後[設定從儲存位置匯入](#import-data-into-eloqua)的資料。[!DNL Oracle Eloqua]

## 匯出類型 {#export-type}

**以設定檔為基礎**  — 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，從對象啟用工作流程的「選取屬性」畫面 [中選取](../../ui/activate-batch-profile-destinations.md#select-attributes)。

## IP位址允許清單 {#allow-list}

使用SFTP儲存設定電子郵件行銷目的地時，Adobe建議您將特定IP範圍新增至允許清單。

如果您需要將AdobeIP新增至允許清單，請參閱雲端儲存目的地的[IP位址允許清單](../cloud-storage/ip-address-allow-list.md)。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

此目的地支援以下連接類型：

* **[!UICONTROL 含密碼的SFTP]**
* **[!UICONTROL 具有SSH金鑰的SFTP]**

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* 對於&#x200B;**[!UICONTROL 使用密碼]**&#x200B;連接的SFTP，必須提供：
   * [!UICONTROL 網域]
   * [!UICONTROL 埠]
   * [!UICONTROL 使用者名稱]
   * [!UICONTROL 密碼]
* 對於&#x200B;**[!UICONTROL 具有SSH金鑰的SFTP]**&#x200B;連線，您必須提供：
   * [!UICONTROL 網域]
   * [!UICONTROL 埠]
   * [!UICONTROL 使用者名稱]
   * [!UICONTROL SSH金鑰]

* 或者，您可以附加RSA格式的公鑰，以在&#x200B;**[!UICONTROL Key]**&#x200B;部分下嚮導出的檔案中添加PGP/GPG加密。 您的公開金鑰必須寫入為[!DNL Base64]編碼字串。
* **[!UICONTROL 名稱]**:為目的地選擇相關名稱。
* **[!UICONTROL 說明]**:輸入目的地的說明。
* **[!UICONTROL 資料夾路徑]**:在您的儲存位置中提供路徑，讓Platform將匯出資料存放為CSV或以Tab分隔的檔案。
* **[!UICONTROL 檔案格式]**: **** CSV或 **TAB_DELIMITED**。選擇要導出到儲存位置的檔案格式。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## 啟用此目的地的區段 {#activate}

請參閱[將受眾資料啟用至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) ，以取得關於將受眾區段啟用至此目的地的指示。

### 目標屬性 {#destination-attributes}

啟用此目的地的區段時，Adobe建議您從[聯合架構](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 選取唯一識別碼，以及您要匯出至目的地的任何其他XDM欄位。 如需詳細資訊，請參閱[啟用對象至電子郵件行銷目的地時的最佳實務](overview.md#best-practices)。

## 匯出的資料 {#exported-data}

對於[!DNL Oracle Eloqua]目的地，Platform會在您提供的儲存位置中建立以Tab分隔的`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟動教學課程中的[verify segment activation](../../ui/activate-batch-profile-destinations.md#verify) 。

## 將資料導入[!DNL Oracle Eloqua] {#import-data-into-eloqua}

將[!DNL Platform]連接到[!DNL SFTP]儲存後，必須將資料從儲存位置導入[!DNL Oracle Eloqua]。 要了解如何完成此操作，請參閱[!DNL Oracle Eloqua Help Center]中的[導入聯繫人或帳戶](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm)。
