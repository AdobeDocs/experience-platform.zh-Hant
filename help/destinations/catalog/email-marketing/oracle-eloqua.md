---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目標；oracle雄辯；oracle
title: （檔案）OracleEloqua連接
description: OracleEloqua是Oracle提供的一個軟體即服務(SaaS)平台，用於實現營銷自動化，旨在幫助B2B營銷人員和組織管理營銷活動和銷售線索的生成。
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: e986fd9479ca2258fc9aab752e2d0376c608554b
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 1%

---

# [!DNL (Files) Oracle Eloqua] 連接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 是一個軟體即服務(SaaS)平台，用於由 [!DNL Oracle] 旨在幫助B2B營銷人員和組織管理營銷活動和銷售線索生成。

將段資料發送到 [!DNL Oracle Eloqua]，必須先 [連接目標](#connect-destination) 在Adobe Experience Platform，然後 [設定資料導入](#import-data-into-eloqua) 從儲存位置 [!DNL Oracle Eloqua]。

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

此目標支援以下連接類型：

* **[!UICONTROL 帶密碼的SFTP]**
* **[!UICONTROL 帶SSH密鑰的SFTP]**

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* 對於 **[!UICONTROL 帶密碼的SFTP]** 連接，必須提供：
   * [!UICONTROL 網域]
   * [!UICONTROL 連接埠]
   * [!UICONTROL 用戶名]
   * [!UICONTROL 密碼]
* 對於 **[!UICONTROL 帶SSH密鑰的SFTP]** 連接，必須提供：
   * [!UICONTROL 網域]
   * [!UICONTROL 連接埠]
   * [!UICONTROL 用戶名]
   * [!UICONTROL SSH密鑰]

* 或者，您可以將RSA格式的公鑰附加到導出的檔案下，將PGP/GPG加密 **[!UICONTROL 鍵]** 的子菜單。 您的公鑰必須寫為 [!DNL Base64] 編碼字串。
* **[!UICONTROL 名稱]**:為目標選擇相關名稱。
* **[!UICONTROL 說明]**:輸入目標的說明。
* **[!UICONTROL 資料夾路徑]**:在儲存位置中提供平台將導出資料儲存為CSV檔案的路徑。
* **[!UICONTROL 檔案格式]**:選擇 **CSV** 將CSV檔案導出到儲存位置。

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

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

對於 [!DNL Oracle Eloqua] 目標，平台建立 `.csv` 檔案。 有關檔案的詳細資訊，請參見 [驗證段激活](../../ui/activate-batch-profile-destinations.md#verify) 在段激活教程中。

## 設定資料導入到 [!DNL Oracle Eloqua] {#import-data-into-eloqua}

連接後 [!DNL Platform] 到 [!DNL SFTP] 儲存，必須將資料導入從儲存位置設定為 [!DNL Oracle Eloqua]。 要瞭解如何完成此操作，請參閱 [導入聯繫人或帳戶](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) 的 [!DNL Oracle Eloqua Help Center]。
