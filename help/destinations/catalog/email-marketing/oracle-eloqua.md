---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地；oracleEloqua；oracle
title: （檔案） Eloqua連線Oracle
description: oracle Eloqua是Oracle提供的行銷自動化軟體即服務(SaaS)平台，旨在協助B2B行銷人員和組織管理行銷活動與銷售機會開發。
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 8e37ff057ec0fb750bc7b4b6f566f732d9fe5d68
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 3%

---

# [!DNL (Files) Oracle Eloqua] 連線

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 是一個軟體即服務(SaaS)平台，用於行銷自動化，由 [!DNL Oracle] 旨在協助B2B行銷人員和組織管理行銷活動和銷售機會開發。

若要傳送受眾資料至 [!DNL Oracle Eloqua]，您必須先 [連線到目的地](#connect-destination) 在Adobe Experience Platform中，然後 [設定資料匯入](#import-data-into-eloqua) 從您的儲存位置移至 [!DNL Oracle Eloqua].

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

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

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

此目的地支援下列連線型別：

* **[!UICONTROL 使用密碼的SFTP]**
* **[!UICONTROL 使用SSH金鑰的SFTP]**

### 連線參數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* 的 **[!UICONTROL 使用密碼的SFTP]** 連線，您必須提供：
   * [!UICONTROL 網域]
   * [!UICONTROL 連接埠]
   * [!UICONTROL 使用者名稱]
   * [!UICONTROL 密碼]
* 的 **[!UICONTROL 使用SSH金鑰的SFTP]** 連線，您必須提供：
   * [!UICONTROL 網域]
   * [!UICONTROL 連接埠]
   * [!UICONTROL 使用者名稱]
   * [!UICONTROL ssh金鑰]

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

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

另請參閱 [啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用此目的地對象的指示。

### 目的地屬性 {#destination-attributes}

將受眾啟用至此目的地時，Adobe建議您從 [聯合結構描述](../../../profile/home.md#profile-fragments-and-union-schemas). 選取唯一識別碼以及您要匯出至目的地的任何其他XDM欄位。 如需詳細資訊，請參閱 [將對象啟用至電子郵件行銷目的地的最佳實務](overview.md#best-practices).

## 匯出的資料 {#exported-data}

的 [!DNL Oracle Eloqua] 目的地，平台會建立 `.csv` 檔案中所指定的儲存位置。 如需檔案的詳細資訊，請參閱 [驗證對象啟用](../../ui/activate-batch-profile-destinations.md#verify) （在audience activation教學課程中）。

## 設定將資料匯入 [!DNL Oracle Eloqua] {#import-data-into-eloqua}

連線之後 [!DNL Platform] 至您的 [!DNL SFTP] 儲存，您必須設定從儲存位置匯入到中的資料 [!DNL Oracle Eloqua]. 若要瞭解如何完成此作業，請參閱 [匯入連絡人或帳戶](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) 在 [!DNL Oracle Eloqua Help Center].
