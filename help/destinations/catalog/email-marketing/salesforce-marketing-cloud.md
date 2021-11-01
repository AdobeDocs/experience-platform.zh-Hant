---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地；salesforce;salesforce目的地
title: SalesforceMarketing Cloud連接
seo-description: Salesforce Marketing Cloud is a digital marketing suite formerly known as ExactTarget that allows you to build and customize journeys for visitors and customers to personalize their experience.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: b0d6e02c67f2a62971332acb224c7422ea467e6c
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud] 連接

## 總覽 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是數位行銷套裝，先前稱為ExactTarget，可讓您建置和自訂歷程，供訪客和客戶個人化其體驗。

若要傳送區段資料至 [!DNL Salesforce Marketing Cloud]您必須先 [連接目標](#connect-destination) 在平台中，然後 [設定資料匯入](#import-data-into-salesforce) 從儲存位置 [!DNL Salesforce Marketing Cloud].

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

針對 [!DNL Salesforce Marketing Cloud] 目的地，平台會建立 `.csv` 檔案。 如需檔案的詳細資訊，請參閱 [驗證區段啟用](../../ui/activate-batch-profile-destinations.md#verify) 在區段啟用教學課程中。

## 設定資料匯入至 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

連接後 [!DNL Platform] 至 [!DNL SFTP] 儲存，您必須將資料從儲存位置匯入至 [!DNL Salesforce Marketing Cloud]. 若要了解如何完成此操作，請參閱 [從檔案將訂閱者匯入Marketing Cloud](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) 在 [!DNL Salesforce Help Center].
