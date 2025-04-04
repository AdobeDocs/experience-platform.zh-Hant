---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地；oracle responsys目的地
title: Oracle回應系統連線
description: Responsys是Oracle所提供用於跨頻道行銷活動的企業電子郵件行銷工具，可將電子郵件、行動裝置、顯示和社交的互動個人化。
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 3%

---

# [!DNL Oracle Responsys]個連線

## 概觀 {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/)是[!DNL Oracle]提供的跨頻道行銷活動的企業電子郵件行銷工具，可個人化電子郵件、行動裝置、顯示和社交的互動。

若要將對象資料傳送至[!DNL Oracle Responsys]，您必須先[連線至Adobe Experience Platform中的目的地](#connect-destination)，然後[設定從儲存位置匯入](#import-data-into-responsys)到[!DNL Oracle Responsys]的資料。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## IP位址允許清單 {#allow-list}

使用SFTP儲存設定電子郵件行銷目的地時，Adobe建議您將特定IP範圍新增至允許清單。

如果您需要將Adobe IP新增至允許清單，請參閱SFTP目的地的[IP位址允許清單](../cloud-storage/ip-address-allow-list.md)。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

此目的地支援下列連線型別：

* **[!UICONTROL 使用密碼的SFTP]**
* 使用SSH金鑰的&#x200B;**[!UICONTROL SFTP]**

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* 對於使用密碼&#x200B;]**連線的**[!UICONTROL  SFTP，您必須提供：
   * [!UICONTROL 網域]
   * [!UICONTROL 連線埠]
   * [!UICONTROL 使用者名稱]
   * [!UICONTROL 密碼]
* 針對使用SSH金鑰&#x200B;]**連線的**[!UICONTROL  SFTP，您必須提供：
   * [!UICONTROL 網域]
   * [!UICONTROL 連線埠]
   * [!UICONTROL 使用者名稱]
   * [!UICONTROL SSH金鑰]
* 您可以選擇附加RSA格式的公開金鑰，將PGP/GPG的加密新增至&#x200B;**[!UICONTROL 金鑰]**&#x200B;區段下的匯出檔案。 您的公開金鑰必須寫入為[!DNL Base64]編碼字串。
* **[!UICONTROL 名稱]**：為您的目的地挑選相關名稱。
* **[!UICONTROL 描述]**：輸入目的地的描述。
* **[!UICONTROL 資料夾路徑]**：提供Experience Platform會將匯出資料儲存為CSV檔案的儲存位置路徑。
* **[!UICONTROL 檔案格式]**：選取&#x200B;**CSV**，將CSV檔案匯出至您的儲存位置。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

請參閱[啟用對象資料至批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md)，以取得啟用對象至此目的地的指示。

### 目的地屬性 {#destination-attributes}

啟用此目的地的對象時，Adobe建議您從[聯合結構描述](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 選取唯一識別碼以及您要匯出至目的地的任何其他XDM欄位。 如需詳細資訊，請參閱[啟用電子郵件行銷目的地的對象時的最佳實務](overview.md#best-practices)。

## 匯出的資料 {#exported-data}

針對[!DNL Oracle Responsys]目的地，Experience Platform會在您提供的儲存位置中建立`.csv`檔案。 如需檔案的詳細資訊，請參閱對象啟用教學課程中的[驗證對象啟用](../../ui/activate-batch-profile-destinations.md#verify)。

## 設定將資料匯入[!DNL Oracle Responsys] {#import-data-into-responsys}

將[!DNL Experience Platform]連線到您的[!DNL SFTP]儲存體後，您必須設定從儲存位置匯入到[!DNL Oracle Responsys]的資料匯入。 若要瞭解如何完成此作業，請參閱[!DNL Oracle Responsys Help Center]中的[匯入連絡人或帳戶](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm)。
