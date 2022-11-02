---
title: （測試版）Google雲端儲存連線
description: 了解如何連線至Google雲端儲存空間及啟用區段或匯出資料集。
source-git-commit: 97a39e12d916e4fbd048c0fb9ddfa9bdfa10d438
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---

# （測試版） [!DNL Google Cloud Storage] 連接

>[!IMPORTANT]
>
>此目的地目前為測試版，僅適用於有限數量的客戶。 若要要求存取 [!DNL Google Cloud Storage] 連線，請連絡您的Adobe代表，並提供 [!DNL Organization ID].

## 總覽 {#overview}

建立即時出站連線至 [!DNL Google Cloud Storage] 定期將資料檔案從Adobe Experience Platform匯出至您自己的貯體。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要依「 」的「選取設定檔屬性」畫面中的選取，匯出區段的所有成員，以及適用的結構欄位 [目的地啟動工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以3、6、8、12或24小時為增量將檔案匯出至下游平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 連接您的 [!DNL Google Cloud Storage] 帳戶 {#prerequisites}

將Platform連線至 [!DNL Google Cloud Storage]，您必須先啟用 [!DNL Google Cloud Storage] 帳戶。 要訪問互操作性設定，請開啟 [!DNL Google Cloud Platform] 選取 **[!UICONTROL 設定]** 從 **[!UICONTROL 雲端儲存空間]** 選項。

![Google雲端平台控制面板，並反白顯示雲端儲存空間和設定。](/help/sources/images/tutorials/create/google-cloud-storage/nav.png)

此 **[!UICONTROL 設定]** 頁。 從這裡，您可以看到 [!DNL Google] 專案ID和您 [!DNL Google Cloud Storage] 帳戶。 要訪問互操作性設定，請選擇 **[!UICONTROL 互操作性]** 從頂端標題。

![Google Cloud Platform控制面板中強調顯示的「互操作性」標籤。](/help/sources/images/tutorials/create/google-cloud-storage/project-access.png)

此 **[!UICONTROL 互操作性]** 頁面包含與服務帳戶相關聯的驗證、存取金鑰和預設專案的相關資訊。 要為服務帳戶生成新的訪問密鑰ID和秘密訪問密鑰，請選擇 **[!UICONTROL 建立服務帳戶的金鑰]**.

![為Google雲端平台控制面板中醒目顯示的服務帳戶控制項建立金鑰。](/help/sources/images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新產生的存取金鑰ID和秘密存取金鑰來連接您的 [!DNL Google Cloud Storage] 帳戶至Platform。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](/help/destinations/ui/connect-destination.md). 在目標設定工作流程中，填寫下列兩節中列出的欄位。

### 驗證到目標 {#authenticate}

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

* **[!UICONTROL 訪問密鑰ID]**:61個字元的英數字串，用於驗證您的 [!DNL Google Cloud Storage] 帳戶至Platform。 如需如何取得此值的詳細資訊，請閱讀 [必要條件](#prerequisites) 一節。
* **[!UICONTROL 秘密訪問密鑰]**:用於驗證您的 [!DNL Google Cloud Storage] 帳戶至Platform。 如需如何取得此值的詳細資訊，請閱讀 [必要條件](#prerequisites) 一節。
* **[!UICONTROL 加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入 [!DNL Base64-encoded] 字串。 在以下說明檔案連結中檢視格式正確且以base64編碼的鍵的範例。 中間部縮短為簡潔。

   ![此影像顯示UI中格式正確且以base64加密的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

如需這些值的詳細資訊，請參閱 [Google雲端儲存HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有關如何生成您自己的訪問密鑰ID和秘密訪問密鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 來源概觀](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:選填。 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 貯體名稱]**:輸入 [!DNL Google Cloud Storage] 此目的地所使用的貯體。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 排程

在 **[!UICONTROL 排程]** 步驟，您可以 [設定匯出排程](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 為 [!DNL Google Cloud Storage] 目的地，您也 [配置導出檔案的名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 對應屬性和身分 {#map}

在 **[!UICONTROL 對應]** 步驟中，您可以選取要針對設定檔匯出的屬性和身分欄位。 您也可以選取將匯出檔案中的標題變更為任何您想要的好記名稱。 如需詳細資訊，請檢視 [對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 在「啟動批次目的地UI」教學課程中。

## （測試版）匯出資料集 {#export-datasets}

此目的地支援資料集匯出。 如需設定資料集匯出的完整資訊，請閱讀 [匯出資料集教學課程](/help/destinations/ui/export-datasets.md).

## 驗證是否成功匯出資料 {#exported-data}

若要確認資料是否已成功匯出，請檢查 [!DNL Google Cloud Storage] 儲存貯體，並確認匯出的檔案包含預期的設定檔母體。
