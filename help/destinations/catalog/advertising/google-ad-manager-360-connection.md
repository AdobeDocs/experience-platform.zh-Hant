---
title: (Beta) [!DNL Google Ad Manager 360] 連接
description: Google廣告管理器360是Google的一個廣告服務平台，它使出版商能夠通過視頻和移動應用管理其網站上廣告的顯示。
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: f163b1e3c60953192b2ddf543eb4f3e8df88799b
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 1%

---

# (Beta) [!DNL Google Ad Manager 360] 連接

## 總覽 {#overview}

的 [!DNL Google Ad Manager 360] 連接啟用批處理上載 [!DNL publisher provided identifiers] (PPID)到 [!DNL Google Ad Manager 360]，通過 [!DNL Google Cloud Storage]。

有關發佈者提供的標識符在Google廣告管理器360中如何工作的詳細資訊，請參閱 [官方Google檔案](https://support.google.com/admanager/answer/2880055?hl=en)。

>[!IMPORTANT]
>
>此目標目前為Beta版，僅對有限數量的客戶可用。 請求訪問 [!DNL Google Ad Manager 360] 連接，請與您的Adobe代表聯繫，並 [!DNL IMS Organization ID]。

的 [!DNL Google Ad Manager 360] 目標導出 [!DNL CSV] 檔案 [!DNL Google Cloud Storage] 桶。 導出後 [!DNL CSV] 檔案必須導入到 [!DNL Google Ad Manager 360] 帳戶。

## 目標說明 {#specifics}

請注意以下特定於 [!DNL Google Ad Manager 360] 目標。

* 在Google平台中以寫程式方式建立激活的受眾，並在CSV檔案中填充。

## 支援的身份 {#supported-identities}

[!DNL This integration] 支援激活下表中描述的身份。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | 選擇此目標標識以將受眾發送到 [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及適用的架構欄位（例如PPID），如在的「選擇配置檔案屬性」螢幕中選擇的 [目標激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style=&quot;table-layout:auto&quot;&quot;

## 先決條件 {#prerequisites}

### 允許清單 {#allow-listing}

>[!NOTE]
>
>在設定第一個允許清單之前，該允許清單是必需的 [!DNL Google Ad Manager] 目標。 請確保以下描述的允許清單過程已由 [!DNL Google] 建立目標之前。

>[!IMPORTANT]
>
>Google簡化了將外部受眾管理平台連接到GoogleAd Manager 360的過程。 您現在可以通過該過程以自助方式連結到Google廣告管理器360。 閱讀 [資料管理平台的細分](https://support.google.com/admanager/answer/3289669?hl=en) 在Google檔案里。 您應將下面列出的ID列在手上。

* **帳戶ID**:Adobe的Google賬戶ID。 帳戶ID:87933855。
* **客戶ID**:Adobe的客戶帳戶ID與Google。 客戶ID:89690775。
* **網路代碼**:這是你的 [!DNL Google Ad Manager] 網路標識符，在 **[!UICONTROL 「管理」>「全局設定」]** 的子菜單。
* **受眾連結ID**:這是與您的 [!DNL Google Ad Manager] 網路 [!DNL Network code]) **[!UICONTROL 「管理」>「全局設定」]** 在Google介面。
* 您的帳戶類型。 由Google或AdX買家提供的DFP。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)。 在目標配置工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

* **[!UICONTROL 訪問密鑰ID]**:61個字元的字母數字字串，用於驗證 [!DNL Google Cloud Storage] 帳戶到平台。
* **[!UICONTROL 秘密訪問密鑰]**:一個40個字元、基64編碼的字串，用於驗證 [!DNL Google Cloud Storage] 帳戶到平台。

有關這些值的詳細資訊，請參見 [Google雲儲存HMAC密鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 的子菜單。 有關如何生成您自己的訪問密鑰ID和密鑰訪問密鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 源概述](/help/sources/connectors/cloud-storage/google-cloud-storage.md)。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:填寫此目標的首選名稱。
* **[!UICONTROL 說明]**:可選。 例如，您可以提及您為此目標使用的市場活動。
* **[!UICONTROL 儲存段名稱]**:輸入 [!DNL Google Cloud Storage] 該目標使用的儲存桶。
* **[!UICONTROL 資料夾路徑]**:輸入將承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 帳戶ID]**:使用 [!DNL Google]。
* **[!UICONTROL 帳戶類型]**:根據您與Google的帳戶選擇選項：
   * 使用 `DFP by Google` 為 [!DNL DoubleClick] 對於發佈者
   * 使用 `AdX buyer` 為 [!DNL Google AdX]

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 有關激活此目標受眾段的說明。

在標識映射步驟中，可以看到以下預填充的映射：

| 預填充映射 | 說明 |
|---------|----------|
| `ECID` -> `ppid` | 這是唯一用戶可編輯的預填充映射。 可以從平台中選擇任何屬性或標識命名空間，並將它們映射到 `ppid`。 |
| `metadata.segment.alias` -> `list_id` | 將Experience Platform段名稱映射到Google平台中的段ID。 |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | 告訴Google平台何時從網段中刪除不合格的用戶。 |

這些映射是 [!DNL Google Ad Manager 360] 由Adobe Experience Platform自動建立 [!DNL Google Ad Manager 360] 連接。

![顯示GoogleAd Manager 360的映射步驟的UI影像。](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## 導出的資料 {#exported-data}

要驗證資料是否已成功導出，請檢查 [!DNL Google Cloud Storage] 儲存段，並確保導出的檔案包含預期的配置檔案總體。
