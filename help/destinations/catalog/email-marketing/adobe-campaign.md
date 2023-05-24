---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目標；adobe促銷活動；市場活動
title: Adobe Campaign
description: Adobe Campaign是一組解決方案，可幫助您個性化並提供所有線上和離線渠道的促銷活動。
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# Adobe Campaign

## 總覽 {#overview}

Adobe Campaign是一組解決方案，可幫助您個性化並提供所有線上和離線渠道的促銷活動。 請參閱 [開始使用Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 的子菜單。

要將段資料發送到Adobe Campaign，必須首先 [連接目標](#connect-destination) 在Adobe Experience Platform，然後 [設定資料導入](#import-data-into-campaign) 從你的倉庫到Adobe Campaign。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## IP地址允許清單 {#allow-list}

當使用SFTP儲存設定電子郵件營銷目標時，Adobe建議將某些IP範圍添加到允許清單中。

請參閱 [雲儲存目標的IP地址允許清單](../cloud-storage/ip-address-allow-list.md) 如果需要將AdobeIP添加到允許清單。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

Adobe Campaign支援以下連接類型：

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL 帶密碼的SFTP]**
* **[!UICONTROL 帶SSH密鑰的SFTP]**
* **[!UICONTROL Azure Blob]**

向Adobe Campaign發送資料的首選方法是 [!DNL Amazon S3] 或 [!DNL Azure Blob]。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* 對於 **[!UICONTROL AmazonS3]** 連接，必須提供 [!UICONTROL 訪問密鑰ID] 和 [!UICONTROL 密鑰訪問密鑰]。
* 對於 **[!UICONTROL 帶密碼的SFTP]** 連接，必須提供 [!UICONTROL 域]。 [!UICONTROL 埠]。 [!UICONTROL 用戶名], [!UICONTROL 密碼]。
* 對於 **[!UICONTROL 帶SSH密鑰的SFTP]** 連接，必須提供 [!UICONTROL 域]。 [!UICONTROL 埠]。 [!UICONTROL 用戶名], [!UICONTROL SSH密鑰]。
* 對於 **[!UICONTROL Azure Blob]** 連接，必須提供連接字串。
* 或者，您可以將RSA格式的公鑰附加到導出的檔案下，將PGP/GPG加密 **[!UICONTROL 鍵]** 的子菜單。 您的公鑰必須寫為 [!DNL Base64] 編碼字串。
* **[!UICONTROL 名稱]**:為目標選擇相關名稱。
* **[!UICONTROL 說明]**:輸入目標的說明。
* **[!UICONTROL 儲存段名稱]**: *對於S3連接*。 輸入S3時段的位置 [!DNL Platform] 將導出資料儲存為CSV檔案。
* **[!UICONTROL 資料夾路徑]**:提供儲存位置中的路徑 [!DNL Platform] 將導出資料儲存為CSV檔案。
* **[!UICONTROL 容器]**: *對於Blob連接*。 包含資料夾路徑的Blob的容器在中。
* **[!UICONTROL 檔案格式]**:選擇 **CSV** 將CSV檔案導出到儲存位置。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。


請參閱 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 有關激活此目標受眾段的說明。

### 目標屬性 {#destination-attributes}

激活此目標的段時，Adobe建議您從 [聯合架構](../../../profile/home.md#profile-fragments-and-union-schemas)。 選擇要導出到目標的唯一標識符和任何其他XDM欄位。 有關詳細資訊，請參閱 [激活受眾電子郵件營銷目標時的最佳做法](overview.md#best-practices)。

## 導出的資料 {#exported-data}

對於 [!DNL Adobe Campaign] 目的地， [!DNL Platform] 建立 `.csv` 檔案。 有關檔案的詳細資訊，請參見 [驗證段激活](../../ui/activate-batch-profile-destinations.md#verify) 在段激活教程中。

## 設定資料導入到Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 記住 [!DNL SFTP] 執行此整合時，根據您的Adobe Campaign合同，儲存限制、資料庫儲存限制和活動配置檔案限制。
>* 您需要使用 [!DNL Campaign] 工作流。 請參閱 [設定定期導入](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) 在Adobe Campaign Classic文檔和 [關於資料管理活動](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) 在Adobe Campaign Standard檔案中。
>* 向Adobe Campaign發送資料的首選方法是 [!DNL Amazon S3] 或 [!DNL Azure Blob]。


連接後 [!DNL Platform] 到 [!DNL Amazon S3] 或 [!DNL Azure Blob] 儲存，必須將資料從儲存位置導入到Adobe Campaign。 要瞭解如何完成此操作，請參閱以下Adobe Campaign文檔頁面：
* [開始資料導入和導出](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=zh-Hant) 和 [資料載入（檔案）](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) 在Adobe Campaign Classic檔案里。
* [開始處理流程和資料管理](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) 和 [載入檔案](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) 在Adobe Campaign Standard檔案里。
