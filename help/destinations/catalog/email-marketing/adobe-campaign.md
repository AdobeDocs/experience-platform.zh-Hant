---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地；adobe campaign；行銷活動
title: Adobe Campaign連線
description: Adobe Campaign是一套解決方案，可協助您個人化所有線上和離線管道，並傳送行銷活動。
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 1%

---

# Adobe Campaign連線

## 概覽 {#overview}

Adobe Campaign是一套解決方案，可協助您個人化所有線上和離線管道，並傳送行銷活動。 如需詳細資訊，請參閱[開始使用Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 。

若要將區段資料傳送至Adobe Campaign，您必須先[連接Adobe Experience Platform中的目的地](#connect-destination)，然後[設定從儲存位置匯入](#import-data-into-campaign)的資料。

## 匯出類型 {#export-type}

**以設定檔為基礎**  — 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，如目的地啟用工作 **[!UICONTROL 流程]** 的「選取歸 [因」步驟中所選](../../ui/activate-destinations.md#select-attributes)。

## IP位址允許清單 {#allow-list}

使用SFTP儲存設定電子郵件行銷目的地時，Adobe建議您將特定IP範圍新增至允許清單。

如果您需要將AdobeIP新增至允許清單，請參閱雲端儲存目的地的[IP位址允許清單](../cloud-storage/ip-address-allow-list.md)。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

Adobe Campaign支援下列連線類型：

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL 含密碼的SFTP]**
* **[!UICONTROL 具有SSH金鑰的SFTP]**
* **[!UICONTROL Azure Blob]**

傳送資料至Adobe Campaign的慣用方法是透過[!DNL Amazon S3]或[!DNL Azure Blob]。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* 對於&#x200B;**[!UICONTROL Amazon S3]**&#x200B;連接，必須提供[!UICONTROL 訪問密鑰ID]和[!UICONTROL 秘密訪問密鑰]。
* 對於&#x200B;**[!UICONTROL 具有密碼]**&#x200B;連接的SFTP，必須提供[!UICONTROL 域]、[!UICONTROL 埠]、[!UICONTROL 用戶名]和[!UICONTROL 密碼]。
* 對於&#x200B;**[!UICONTROL 具有SSH密鑰]**&#x200B;的SFTP，必須提供[!UICONTROL 域]、[!UICONTROL 埠]、[!UICONTROL 用戶名]和[!UICONTROL SSH密鑰]。
* 對於&#x200B;**[!UICONTROL Azure Blob]**&#x200B;連接，必須提供連接字串。
* 或者，您可以附加RSA格式的公鑰，以在&#x200B;**[!UICONTROL Key]**&#x200B;部分下嚮導出的檔案中添加PGP/GPG加密。 您的公開金鑰必須寫入為[!DNL Base64]編碼字串。
* **[!UICONTROL 名稱]**:為目的地選擇相關名稱。
* **[!UICONTROL 說明]**:輸入目的地的說明。
* **[!UICONTROL 貯體名稱]**: *用於S3連線*。輸入S3儲存貯體的位置，其中[!DNL Platform]會將匯出資料存入為CSV或以Tab分隔的檔案。
* **[!UICONTROL 資料夾路徑]**:在您的儲存位置中提供路徑， [!DNL Platform] 將匯出資料儲存為CSV或以Tab分隔的檔案。
* **[!UICONTROL 容器]**: *用於Blob連線*。包含資料夾路徑的Blob的容器。
* **[!UICONTROL 檔案格式]**: **** CSV或 **TAB_DELIMITED**。選擇要導出到儲存位置的檔案格式。

## 啟用此目的地的區段 {#activate}

請參閱[將設定檔和區段啟用至目的地](../../ui/activate-destinations.md) ，以取得將對象區段啟用至目的地的指示。

## 目標屬性 {#destination-attributes}

當[啟用區段](../../ui/activate-destinations.md)至此目的地時，Adobe建議您從[聯合架構](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 選取唯一識別碼，以及您要匯出至目的地的任何其他XDM欄位。 有關詳細資訊，請參閱[選擇要在導出的檔案](./overview.md#destination-attributes)中用作目標屬性的架構欄位。

## 匯出的資料 {#exported-data}

對於[!DNL Adobe Campaign]目標， [!DNL Platform]會在您提供的儲存位置中建立以Tab分隔的`.csv`檔案。 如需檔案的詳細資訊，請參閱區段啟用教學課程中的[電子郵件行銷目的地和雲端儲存目的地](../../ui/activate-destinations.md#esp-and-cloud-storage)。

## 設定資料匯入至Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 執行此整合時，請記住[!DNL SFTP]儲存限制、資料庫儲存限制和作用中設定檔限制，如您的Adobe Campaign合約所述。
>* 您需要使用[!DNL Campaign]工作流程，在Adobe Campaign中排程、匯入和對應已匯出的區段。 請參閱Adobe Campaign Classic檔案中的[設定循環匯入](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html)和Adobe Campaign Standard檔案中的[關於資料管理活動](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html)。
>* 傳送資料至Adobe Campaign的慣用方法是透過[!DNL Amazon S3]或[!DNL Azure Blob]。


將[!DNL Platform]連接到[!DNL Amazon S3]或[!DNL Azure Blob]儲存後，必須將資料從儲存位置導入Adobe Campaign。 若要了解如何完成此操作，請參閱下列Adobe Campaign檔案頁面：
* [開始使用Adobe Campaign Classic檔案](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=zh-Hant) 中 [的資料匯入和匯出（檔案）](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) 。
* [開始使用Adobe Campaign Standard檔案中](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) 的程 [式](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) 與資料管理及載入檔案。
