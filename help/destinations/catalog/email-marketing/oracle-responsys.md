---
keywords: 電子郵件；電子郵件；電子郵件目的地；oracleresponsys目的地
title: OracleResponsys連線
description: Responsys是企業電子郵件行銷工具，適用於Oracle提供的跨管道行銷活動，可個人化電子郵件、行動裝置、顯示器和社交的互動。
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: b0d6e02c67f2a62971332acb224c7422ea467e6c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# [!DNL Oracle Responsys] 連接

## 總覽 {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/) 是企業電子郵件行銷工具，適用於 [!DNL Oracle] 個人化電子郵件、行動裝置、顯示器和社交的互動。

若要傳送區段資料至 [!DNL Oracle Responsys]您必須先 [連接到目標](#connect-destination) 在Adobe Experience Platform [設定資料匯入](#import-data-into-responsys) 從儲存位置 [!DNL Oracle Responsys].

## 匯出類型 {#export-type}

**設定檔**  — 您要匯出區段的所有成員，以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取屬性」畫面中所選 [對象啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes).

## IP位址允許清單 {#allow-list}

使用SFTP儲存設定電子郵件行銷目的地時，Adobe建議您將特定IP範圍新增至允許清單。

請參閱 [雲端儲存目的地的IP位址允許清單](../cloud-storage/ip-address-allow-list.md) 如果您需要將AdobeIP新增至允許清單。

## 連接到目標 {#connect}

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

此目的地支援以下連接類型：

* **[!UICONTROL 含密碼的SFTP]**
* **[!UICONTROL 具有SSH金鑰的SFTP]**

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* 針對 **[!UICONTROL 含密碼的SFTP]** 連線，您必須提供：
   * [!UICONTROL 網域]
   * [!UICONTROL 埠]
   * [!UICONTROL 使用者名稱]
   * [!UICONTROL 密碼]
* 針對 **[!UICONTROL 具有SSH金鑰的SFTP]** 連線，您必須提供：
   * [!UICONTROL 網域]
   * [!UICONTROL 埠]
   * [!UICONTROL 使用者名稱]
   * [!UICONTROL SSH金鑰]
* 或者，您可以附加RSA格式的公開金鑰，將加密功能與PGP/GPG一起新增至 **[!UICONTROL 金鑰]** 區段。 您的公開金鑰必須寫入 [!DNL Base64] 編碼字串。
* **[!UICONTROL 名稱]**:為目的地選擇相關名稱。
* **[!UICONTROL 說明]**:輸入目的地的說明。
* **[!UICONTROL 資料夾路徑]**:在您的儲存位置中提供路徑，讓Platform將匯出資料存放為CSV檔案。
* **[!UICONTROL 檔案格式]**:選擇 **CSV** 將CSV檔案匯出至儲存位置。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## 啟用此目的地的區段 {#activate}

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 目標屬性 {#destination-attributes}

啟用此目的地的區段時，Adobe建議您從 [聯合方案](../../../profile/home.md#profile-fragments-and-union-schemas). 選取唯一識別碼，以及您要匯出至目的地的任何其他XDM欄位。 如需詳細資訊，請參閱 [啟用受眾以傳送電子郵件給行銷目的地的最佳實務](overview.md#best-practices).

## 匯出的資料 {#exported-data}

針對 [!DNL Oracle Responsys] 目的地，平台會建立 `.csv` 檔案。 如需檔案的詳細資訊，請參閱 [驗證區段啟用](../../ui/activate-batch-profile-destinations.md#verify) 在區段啟用教學課程中。

## 設定資料匯入至 [!DNL Oracle Responsys] {#import-data-into-responsys}

連接後 [!DNL Platform] 至 [!DNL SFTP] 儲存，您必須將資料從儲存位置匯入至 [!DNL Oracle Responsys]. 若要了解如何完成此操作，請參閱 [導入聯繫人或帳戶](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) 在 [!DNL Oracle Responsys Help Center].
