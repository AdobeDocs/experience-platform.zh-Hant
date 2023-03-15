---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地；adobe campaign；行銷活動
title: Adobe Campaign連線
description: Adobe Campaign是一套解決方案，可協助您個人化所有線上和離線管道，並傳送行銷活動。
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# Adobe Campaign連線

## 總覽 {#overview}

Adobe Campaign是一套解決方案，可協助您個人化所有線上和離線管道，並傳送行銷活動。 請參閱 [開始使用Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 以取得更多資訊。

若要傳送區段資料至Adobe Campaign，您必須先 [連接目標](#connect-destination) 在Adobe Experience Platform [設定資料匯入](#import-data-into-campaign) 從儲存位置移入Adobe Campaign。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取設定檔屬性」畫面中所選 [目的地啟動工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以3、6、8、12或24小時為增量將檔案匯出至下游平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP位址允許清單 {#allow-list}

使用SFTP儲存設定電子郵件行銷目的地時，Adobe建議您將特定IP範圍新增至允許清單。

請參閱 [雲端儲存目的地的IP位址允許清單](../cloud-storage/ip-address-allow-list.md) 如果您需要將AdobeIP新增至允許清單。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或連絡您的產品管理員以取得所需的權限

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

Adobe Campaign支援下列連線類型：

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL 含密碼的SFTP]**
* **[!UICONTROL 具有SSH金鑰的SFTP]**
* **[!UICONTROL Azure Blob]**

將資料傳送至Adobe Campaign的偏好方法為 [!DNL Amazon S3] 或 [!DNL Azure Blob].

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* 針對 **[!UICONTROL Amazon S3]** 連線，您必須提供 [!UICONTROL 訪問密鑰ID] 和 [!UICONTROL 秘密訪問密鑰].
* 針對 **[!UICONTROL 含密碼的SFTP]** 連接，您必須提供 [!UICONTROL 網域], [!UICONTROL 埠], [!UICONTROL 使用者名稱]，和 [!UICONTROL 密碼].
* 針對 **[!UICONTROL 具有SSH金鑰的SFTP]** 連接，您必須提供 [!UICONTROL 網域], [!UICONTROL 埠], [!UICONTROL 使用者名稱]，和 [!UICONTROL SSH金鑰].
* 針對 **[!UICONTROL Azure Blob]** 連接，必須提供連接字串。
* 或者，您可以附加RSA格式的公開金鑰，將加密功能與PGP/GPG一起新增至 **[!UICONTROL 金鑰]** 區段。 您的公開金鑰必須寫入 [!DNL Base64] 編碼字串。
* **[!UICONTROL 名稱]**:為目的地選擇相關名稱。
* **[!UICONTROL 說明]**:輸入目的地的說明。
* **[!UICONTROL 貯體名稱]**: *S3連線*. 輸入S3儲存貯體的位置 [!DNL Platform] 會將您的匯出資料儲存為CSV檔案。
* **[!UICONTROL 資料夾路徑]**:在儲存位置提供路徑，其中 [!DNL Platform] 會將您的匯出資料儲存為CSV檔案。
* **[!UICONTROL 容器]**: *對於Blob連接*. 包含資料夾路徑的Blob的容器。
* **[!UICONTROL 檔案格式]**:選擇 **CSV** 將CSV檔案匯出至儲存位置。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。


請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 目標屬性 {#destination-attributes}

啟用此目的地的區段時，Adobe建議您從 [聯合方案](../../../profile/home.md#profile-fragments-and-union-schemas). 選取唯一識別碼，以及您要匯出至目的地的任何其他XDM欄位。 如需詳細資訊，請參閱 [啟用受眾以傳送電子郵件給行銷目的地的最佳實務](overview.md#best-practices).

## 匯出的資料 {#exported-data}

針對 [!DNL Adobe Campaign] 目的地， [!DNL Platform] 會建立 `.csv` 檔案。 如需檔案的詳細資訊，請參閱 [驗證區段啟用](../../ui/activate-batch-profile-destinations.md#verify) 在區段啟用教學課程中。

## 設定資料匯入至Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 請記住 [!DNL SFTP] 執行此整合時，會根據您的Adobe Campaign合約，限制儲存空間、資料庫儲存空間和作用中設定檔限制。
>* 您需要在Adobe Campaign中，使用 [!DNL Campaign] 工作流程。 請參閱 [設定循環匯入](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) 在Adobe Campaign Classic檔案和 [關於資料管理活動](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) 在Adobe Campaign Standard檔案中。
>* 將資料傳送至Adobe Campaign的偏好方法為 [!DNL Amazon S3] 或 [!DNL Azure Blob].


連接後 [!DNL Platform] 至 [!DNL Amazon S3] 或 [!DNL Azure Blob] 儲存，您必須將資料從儲存位置匯入至Adobe Campaign。 若要了解如何完成此操作，請參閱下列Adobe Campaign檔案頁面：
* [開始匯入和匯出資料](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=zh-Hant) 和 [資料載入（檔案）](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) 在Adobe Campaign Classic檔案中。
* [開始使用程式和資料管理](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) 和 [載入檔案](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) 在Adobe Campaign Standard檔案中。
