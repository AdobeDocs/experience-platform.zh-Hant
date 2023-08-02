---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地；salesforce；salesforce目的地
title: SalesforceMarketing Cloud連線
description: SalesforceMarketing Cloud是數位行銷套件，先前稱為ExactTarget，可讓您為訪客和客戶建置和自訂歷程，以個人化其體驗。
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 2%

---

# [!DNL (Files) Salesforce Marketing Cloud] 連線

## 概觀 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 是數位行銷套件，先前稱為ExactTarget，可讓您為訪客和客戶建置和自訂歷程，以個人化其體驗。

若要傳送受眾資料至 [!DNL Salesforce Marketing Cloud]，您必須先 [連線到目的地](#connect-destination) 在Platform中，然後 [設定資料匯入](#import-data-into-salesforce) 從您的儲存位置移至 [!DNL Salesforce Marketing Cloud].

## 支援的對象 {#supported-audiences}

本節說明您可以匯出至此目的地的所有對象。

此目的地支援啟用透過Experience Platform產生的所有對象 [分段服務](../../../segmentation/home.md).

*此外*，此目的地也支援下表所述的對象啟用。

| 對象型別 | 說明 |
---------|----------|
| 自訂上傳 | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如 [目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP位址允許清單 {#allow-list}

使用SFTP儲存設定電子郵件行銷目的地時，Adobe建議您將特定IP範圍新增至允許清單。

請參閱 [SFTP目的地的IP位址允許清單](../cloud-storage/ip-address-allow-list.md) 如果您需要將AdobeIP新增至允許清單。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

此目的地支援下列連線型別：

* **[!UICONTROL 使用密碼的SFTP]**
* **[!UICONTROL 使用SSH金鑰的SFTP]**

### 連線引數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* 的 **[!UICONTROL 使用密碼的SFTP]** 連線，您必須提供：
   * **[!UICONTROL 網域]**：SFTP帳戶的IP位址或網域名稱；
   * **[!UICONTROL 連線埠]**：您的SFTP儲存位置使用的連線埠；
   * **[!UICONTROL 使用者名稱]**：登入您的SFTP儲存位置的使用者名稱；
   * **[!UICONTROL 密碼]**：登入SFTP儲存位置的密碼。
* 的 **[!UICONTROL 使用SSH金鑰的SFTP]** 連線，您必須提供：
   * **[!UICONTROL 網域]**：SFTP帳戶的IP位址或網域名稱；
   * **[!UICONTROL 連線埠]**：您的SFTP儲存位置使用的連線埠；
   * **[!UICONTROL 使用者名稱]**：登入您的SFTP儲存位置的使用者名稱；
   * **[!UICONTROL ssh金鑰]**：用來登入SFTP儲存位置的私人SSH金鑰。 私密 金鑰的格式必須為 Base64 編碼的字串，並且不得受密碼保護。

* 或者，您可以附加RSA格式的公開金鑰，將PGP/GPG的加密新增至匯出的檔案，位於 **[!UICONTROL 索引鍵]** 區段。 您的公開金鑰必須寫成 [!DNL Base64] 編碼字串。
* **[!UICONTROL 名稱]**：為您的目的地選擇相關名稱。
* **[!UICONTROL 說明]**：輸入目的地的說明。
* **[!UICONTROL 資料夾路徑]**：在您的儲存位置中提供路徑，Platform會將您的匯出資料儲存為CSV檔案。
* **[!UICONTROL 檔案格式]**：選取 **CSV** 以將CSV檔案匯出至您的儲存位置。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地對象的指示。

### 目的地屬性 {#destination-attributes}

將受眾啟用至此目的地時，Adobe建議您從 [聯合結構描述](../../../profile/home.md#profile-fragments-and-union-schemas). 選取唯一識別碼以及您要匯出至目的地的任何其他XDM欄位。 如需詳細資訊，請參閱 [將對象啟用至電子郵件行銷目的地的最佳實務](overview.md#best-practices).

## 匯出的資料 {#exported-data}

的 [!DNL Salesforce Marketing Cloud] 目的地，平台會建立 `.csv` 檔案中所指定的儲存位置。 如需檔案的詳細資訊，請參閱 [驗證對象啟用](../../ui/activate-batch-profile-destinations.md#verify) （在audience activation教學課程中）。

## 設定將資料匯入 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

連線之後 [!DNL Platform] 至您的 [!DNL SFTP] 儲存，您必須設定從儲存位置匯入到中的資料 [!DNL Salesforce Marketing Cloud]. 若要瞭解如何完成此作業，請參閱 [將訂閱者從檔案匯入Marketing Cloud](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) 在 [!DNL Salesforce Help Center].
