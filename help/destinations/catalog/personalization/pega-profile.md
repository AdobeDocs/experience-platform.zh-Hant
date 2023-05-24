---
title: Pega輪廓連接器
description: 使用Adobe Experience PlatformAmazonS3的Pega配置檔案連接器將完整或增量配置檔案資料導出到AmazonS3雲儲存。 在Pega客戶決策中心中，可以在客戶配置檔案設計器中安排資料作業，以定期從AmazonS3儲存中導入配置檔案資料。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# Pega輪廓連接器

## 總覽 {#overview}

使用 [!DNL Pega Profile Connector] 在Adobe Experience Platform建立與 [!DNL Amazon Web Services] (AWS)S3儲存，定期將配置檔案資料從Adobe Experience Platform導出到CSV檔案，並將其導出到您自己的S3儲存桶中。 在 [!DNL Pega Customer Decision Hub]，您可以安排資料作業從S3儲存導入此配置檔案資料以更新 [!DNL Pega Customer Decision Hub] 檔案。

此連接器有助於設定配置檔案資料的初始導出，還有助於定期將新配置檔案同步到 [!DNL Pega Customer Decision Hub]。  在客戶決策中心擁有最新資料，為下一最佳行動決策提供了更好、更新的客戶群視圖。

>[!IMPORTANT]
>
>此文檔頁面由Pegasystems建立。 如有任何查詢或更新請求，請直接與Pega聯繫 [這裡](mailto:support@pega.com)。

## 使用案例

幫助您更好地瞭解您應如何以及何時使用 [!DNL Pega Profile Connector] 目的地，以下是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 用例1

營銷商希望最初設定 [!DNL Pega Customer Decision Hub] 從Adobe Experience Platform裝載的資料。 這是初始滿載，然後是按計畫的增量載荷。

### 用例2

營銷商希望從Adobe Experience Platform獲得最新的個人資料資料 [!DNL Pega Customer Decision Hub] 這可以不斷增強Pega對客戶簡介的洞察力。

## 先決條件 {#prerequisites}

在使用此目標將資料導出到Adobe Experience Platform並將配置檔案導入到 [!DNL Pega Customer Decision Hub]，確保完成以下先決條件：

* 配置 [!DNL Amazon S3] 儲存段和用於導出和導入資料檔案的資料夾路徑。
* 配置 [!DNL Amazon S3] 訪問密鑰和 [!DNL Amazon S3] 密鑰：在 [!DNL Amazon S3]，生成 `access key - secret access key` 對以授予您的平台訪問權 [!DNL Amazon S3] 帳戶。
* 要成功將資料連接和導出到 [!DNL Amazon S3] 建立Identity and Access Management(IAM)用戶 [!DNL Platform] 在 [!DNL Amazon S3] 分配權限，如 `s3:DeleteObject`。 `s3:GetBucketLocation`。 `s3:GetObject`。 `s3:ListBucket`。 `s3:PutObject`。 `s3:ListMultipartUploadParts`
* 確保 [!DNL Pega Customer Decision Hub] 實例已升級到8.8版或更高版本。

## 支援的身份 {#supported-identities}

[!DNL Pega Customer Decision Hub] 支援激活下表中所述的自定義用戶ID。 有關詳細資訊，請參閱 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 |
|---|---|
| *客戶ID* | 唯一標識中配置檔案的通用用戶標識符 [!DNL Pega Customer Decision Hub] 和Adobe Experience Platform |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在目標配置工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

* **[!DNL Amazon S3]訪問密鑰** 和 **[!DNL Amazon S3]密鑰**:在 [!DNL Amazon S3]，生成 `access key - secret access key` 兩對給Adobe Experience Platform訪問 [!DNL Amazon S3] 帳戶。 在 [Amazon Web Services文檔](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

### 填寫目標詳細資訊 {#destination-details}

在建立與 [!DNL Amazon S3]，提供目標的以下資訊：

![UI螢幕的影像顯示Pega配置檔案連接器目標詳細資訊的已完成欄位](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

要配置目標的詳細資訊，請填寫必填欄位並選擇 **[!UICONTROL 下一個]**。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:輸入一個名稱，以幫助您標識此目標。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 儲存段名稱]**:輸入 [!DNL Amazon S3] 該目標使用的儲存桶。
* **[!UICONTROL 資料夾路徑]**:輸入將承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 壓縮類型]**:選擇壓縮類型為GZIP或NONE。

>[!TIP]
>
>在連接目標工作流中，您可以在每個導出的段檔案的AmazonS3儲存中建立一個自定義資料夾。 閱讀 [使用宏在儲存位置中建立資料夾](/help/destinations/catalog/cloud-storage/overview.md#use-macros) 的雙曲餘切值。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 有關激活此目標受眾段的說明。

### 映射屬性和標識 {#map}

在 **[!UICONTROL 映射]** 步驟，您可以選擇要為配置檔案導出的屬性和標識欄位。 也可以選擇將導出檔案中的標題更改為任何您希望的友好名稱。 有關詳細資訊，請查看 [映射步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在激活批處理目標UI教程中。

## 驗證資料導出 {#exported-data}

對於 [!DNL Pega Profile Connector] 目的地， [!DNL Platform] 建立 `.csv` 檔案位於您提供的AmazonS3儲存位置。 有關檔案的詳細資訊，請參見 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 在段激活教程中。

從S3成功導入配置檔案資料會在 [!DNL Pega Customer] 配置檔案資料儲存。 導入的客戶配置檔案資料可在 [!DNL Pega Customer Profile Designer] ，如下圖所示。
![UI螢幕的影像，您可以在客戶配置檔案設計器中驗證Adobe配置檔案資料](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

在 [!DNL Pega Customer Decision Hub]，資料管理員可以配置資料作業 [!DNL Customer Profile Designer] 定期從S3導入配置檔案資料，如下圖所示。 查看 [額外資源](#additional-resources) 有關如何配置資料作業以從導入配置檔案資料的詳細資訊 [!DNL Amazon S3]。
![UI螢幕的影像，用於配置客戶配置檔案設計器中的資料作業](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## 其他資源 {#additional-resources}

請參閱 [導入資料作業](https://academy.pega.com/topic/import-data-jobs/v1) 在 [!DNL Pega Customer Decision Hub]。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。
