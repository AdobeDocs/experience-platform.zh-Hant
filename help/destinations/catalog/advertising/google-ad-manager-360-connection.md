---
title: (Beta) [!DNL Google Ad Manager 360] 連接
description: Google廣告管理器360是Google的一個廣告服務平台，它使出版商能夠通過視頻和移動應用管理其網站上廣告的顯示。
source-git-commit: 60ae86ed6e741bd7739086105bfe70952841d454
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 2%

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
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style=&quot;table-layout:auto&quot;&quot;

## 先決條件 {#prerequisites}

### 允許清單 {#allow-listing}

>[!NOTE]
>
>在設定第一個允許清單之前，該允許清單是必需的 [!DNL Google Ad Manager] 目標。 請確保以下描述的允許清單過程已由 [!DNL Google] 建立目標之前。

在建立 [!DNL Google Ad Manager 360] 目標在平台中，您必須聯繫 [!DNL Google] 用於將Adobe置於允許的資料提供程式清單中，以及將帳戶添加到允許清單中。 聯繫人 [!DNL Google] 並提供以下資訊：

* **帳戶ID**:Adobe的Google賬戶ID。 帳戶ID:87933855。
* **客戶ID**:Adobe的客戶帳戶ID與Google。 客戶ID:89690775。
* **網路ID**:這是你的帳戶 [!DNL Google Ad Manager]
* **受眾連結ID**:這是你的帳戶 [!DNL Google Ad Manager]
* 您的帳戶類型。 由Google或AdX買家提供的DFP。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL 名稱]**:填寫此目標的首選名稱。
* **[!UICONTROL 說明]**:可選。 例如，您可以提及您為此目標使用的市場活動。
* **[!UICONTROL 儲存段名稱]**:輸入 [!DNL Google Cloud Storage] 該目標使用的儲存桶。
* **[!UICONTROL 資料夾路徑]**:輸入將承載導出檔案的目標資料夾的路徑。

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
