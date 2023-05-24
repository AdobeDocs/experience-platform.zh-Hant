---
title: (Beta)Google雲儲存連接
description: 瞭解如何連接到Google雲儲存並激活資料段或導出資料集。
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: a07557ec398631ece0c8af6ec7b32e0e8593e24b
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 0%

---

# (Beta) [!DNL Google Cloud Storage] 連接

>[!IMPORTANT]
>
>此目標目前為Beta版，僅對有限數量的客戶可用。 請求訪問 [!DNL Google Cloud Storage] 連接，請與您的Adobe代表聯繫，並 [!DNL Organization ID]。

## 總覽 {#overview}

建立即時出站連接到 [!DNL Google Cloud Storage] 定期將資料檔案從Adobe Experience Platform導出到您自己的儲存桶中。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及適用的架構欄位，如在的「選擇配置檔案屬性」螢幕中選擇的 [目標激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連接您的 [!DNL Google Cloud Storage] 帳戶 {#prerequisites}

將平台連接到 [!DNL Google Cloud Storage]，您必須首先啟用互操作性 [!DNL Google Cloud Storage] 帳戶。 要訪問互操作性設定，請開啟 [!DNL Google Cloud Platform] 選擇 **[!UICONTROL 設定]** 從 **[!UICONTROL 雲儲存]** 的子菜單。

![Google雲平台儀表板，其中突出顯示了雲儲存和設定。](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

的 **[!UICONTROL 設定]** 的子菜單。 從這裡，您可以看到 [!DNL Google] 項目ID和有關您的 [!DNL Google Cloud Storage] 帳戶。 要訪問互操作性設定，請選擇 **[!UICONTROL 互操作性]** 的下界。

![Google雲平台儀表板中突出顯示的互操作性頁籤。](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

的 **[!UICONTROL 互操作性]** 頁面包含有關驗證、訪問密鑰和與服務帳戶關聯的預設項目的資訊。 要為服務帳戶生成新的訪問密鑰ID和密鑰訪問密鑰，請選擇 **[!UICONTROL 為服務帳戶建立密鑰]**。

![為Google雲平台儀表板中突出顯示的服務帳戶控制項建立密鑰。](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新生成的訪問密鑰ID和密鑰訪問密鑰來連接 [!DNL Google Cloud Storage] 帳戶到平台。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](/help/destinations/ui/connect-destination.md)。 在目標配置工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

* **[!UICONTROL 訪問密鑰ID]**:61個字元的字母數字字串，用於驗證 [!DNL Google Cloud Storage] 帳戶到平台。 有關如何獲取此值的資訊，請閱讀 [先決條件](#prerequisites) 的上界。
* **[!UICONTROL 秘密訪問密鑰]**:一個40個字元的base64編碼字串，用於驗證 [!DNL Google Cloud Storage] 帳戶到平台。 有關如何獲取此值的資訊，請閱讀 [先決條件](#prerequisites) 的上界。
* **[!UICONTROL 加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 查看下圖中格式正確的加密密鑰示例。

   ![顯示UI中格式正確的PGP鍵示例的影像](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

有關這些值的詳細資訊，請閱讀 [Google雲儲存HMAC密鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 的子菜單。 有關如何生成您自己的訪問密鑰ID和密鑰訪問密鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 源概述](/help/sources/connectors/cloud-storage/google-cloud-storage.md)。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:填寫此目標的首選名稱。
* **[!UICONTROL 說明]**:可選。 例如，您可以提及您為此目標使用的市場活動。
* **[!UICONTROL 儲存段名稱]**:輸入 [!DNL Google Cloud Storage] 該目標使用的儲存桶。
* **[!UICONTROL 資料夾路徑]**:輸入將承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 檔案類型]**:選擇導出檔案應使用的格式Experience Platform。 選擇 [!UICONTROL CSV] 選項 [配置檔案格式選項](../../ui/batch-destinations-file-formatting-options.md)。
* **[!UICONTROL 壓縮格式]**:選擇Experience Platform應用於導出檔案的壓縮類型。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 有關激活此目標受眾段的說明。

### 計畫

在 **[!UICONTROL 計畫]** 步驟 [設定導出計畫](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 為 [!DNL Google Cloud Storage] 目標，您也 [配置導出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。

### 映射屬性和標識 {#map}

在 **[!UICONTROL 映射]** 步驟，您可以選擇要為配置檔案導出的屬性和標識欄位。 也可以選擇將導出檔案中的標題更改為任何您希望的友好名稱。 有關詳細資訊，請查看 [映射步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在激活批處理目標UI教程中。

## (Beta)導出資料集 {#export-datasets}

此目標支援資料集導出。 有關如何設定資料集導出的完整資訊，請閱讀 [導出資料集教程](/help/destinations/ui/export-datasets.md)。

## 驗證成功的資料導出 {#exported-data}

要驗證資料是否已成功導出，請檢查 [!DNL Google Cloud Storage] 儲存段，並確保導出的檔案包含預期的配置檔案總體。
