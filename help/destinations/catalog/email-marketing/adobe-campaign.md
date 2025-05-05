---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地；adobe campaign；行銷活動
title: Adobe Campaign連線
description: Adobe Campaign 這一組解決方案可協助您針對所有線上和離線管道來實現個人化並提供行銷活動。
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 4%

---

# Adobe Campaign連線

## 概觀 {#overview}

Adobe Campaign這一組解決方案可協助您針對所有線上和離線管道來實現個人化並提供行銷活動。 如需詳細資訊，請參閱[開始使用Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=zh-Hant)。

若要將對象資料傳送至Adobe Campaign，您必須先在Adobe Experience Platform中[連線目的地](#connect-destination)，然後[設定從儲存位置匯入](#import-data-into-campaign)至Adobe Campaign的資料。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
| ---------|----------|----------|
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
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

Adobe Campaign支援下列連線型別：

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL 使用密碼的SFTP]**
* 使用SSH金鑰的&#x200B;**[!UICONTROL SFTP]**
* **[!UICONTROL Azure Blob]**

將資料傳送至Adobe Campaign的偏好方法是透過[!DNL Amazon S3]或[!DNL Azure Blob]。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* 針對&#x200B;**[!UICONTROL Amazon S3]**&#x200B;連線，您必須提供您的[!UICONTROL 存取金鑰識別碼]和[!UICONTROL 秘密存取金鑰]。
* 針對使用密碼&#x200B;**連線的** SFTP，您必須提供[!UICONTROL 網域]、[!UICONTROL 連線埠]、[!UICONTROL 使用者名稱]以及[!UICONTROL 密碼]。
* 針對具有SSH金鑰&#x200B;**連線的** SFTP，您必須提供[!UICONTROL 網域]、[!UICONTROL 連線埠]、[!UICONTROL 使用者名稱]和[!UICONTROL SSH金鑰]。
* 對於&#x200B;**[!UICONTROL Azure Blob]**&#x200B;連線，您必須提供連線字串。
* 您可以選擇附加RSA格式的公開金鑰，將PGP/GPG的加密新增至&#x200B;**[!UICONTROL 金鑰]**&#x200B;區段下的匯出檔案。 您的公開金鑰必須寫入為[!DNL Base64]編碼字串。
* **[!UICONTROL 名稱]**：為您的目的地挑選相關名稱。
* **[!UICONTROL 描述]**：輸入目的地的描述。
* **[!UICONTROL Bucket名稱]**： S3連線&#x200B;*的*。 輸入S3儲存貯體的位置，[!DNL Experience Platform]會將您的匯出資料儲存為CSV檔案。
* **[!UICONTROL 資料夾路徑]**：提供儲存位置的路徑，[!DNL Experience Platform]會將您的匯出資料儲存為CSV檔案。
* **[!UICONTROL 容器]**： Blob連線&#x200B;*的*。 包含資料夾路徑所在Blob的容器。
* **[!UICONTROL 檔案格式]**：選取&#x200B;**CSV**，將CSV檔案匯出至您的儲存位置。

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

針對[!DNL Adobe Campaign]目的地，[!DNL Experience Platform]會在您提供的儲存位置中建立`.csv`檔案。 如需檔案的詳細資訊，請參閱對象啟用教學課程中的[驗證對象啟用](../../ui/activate-batch-profile-destinations.md#verify)區段。

## 設定資料匯入Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 在執行此整合時，請記住Adobe Campaign合約中的[!DNL SFTP]儲存空間限制、資料庫儲存空間限制和作用中設定檔限制。
>* 您需要使用[!DNL Campaign]工作流程在Adobe Campaign中排程、匯入及對應匯出的區段。 請參閱Adobe Campaign Classic檔案中的[設定循環匯入](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html?lang=zh-Hant)以及Adobe Campaign Standard檔案中的[關於資料管理活動](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html?lang=zh-Hant)。
>* 將資料傳送至Adobe Campaign的偏好方法是透過[!DNL Amazon S3]或[!DNL Azure Blob]。

將[!DNL Experience Platform]連線至您的[!DNL Amazon S3]或[!DNL Azure Blob]儲存體後，您必須設定從儲存位置匯入Adobe Campaign的資料。 若要瞭解如何完成此作業，請參閱下列Adobe Campaign檔案頁面：
* [開始在Adobe Campaign Classic檔案中匯入和匯出資料](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=zh-Hant)以及[資料載入（檔案）](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html?lang=zh-Hant)。
* [開始使用流程和資料管理](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html?lang=zh-Hant)和[在Adobe Campaign Standard檔案中載入檔案](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html?lang=zh-Hant)。
