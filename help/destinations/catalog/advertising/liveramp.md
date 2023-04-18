---
title: (Alpha) [!DNL LiveRamp SFTP] 連接
description: 了解如何使用LiveRamp連接器將受眾從Adobe Real-time Customer Data Platform上架到LiveRamp Connect。
hidefromtoc: true
hide: true
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: d7625018b7b36d8e9516f7884fc00b726d391103
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 3%

---

# (Alpha) [!DNL LiveRamp - SFTP] 連接 {#liveramp-destination}

使用LiveRamp連線將受眾從Adobe Real-time Customer Data Platform上架至 [!DNL LiveRamp Connect].

>[!IMPORTANT]
>
><p>此目的地連線目前處於Alpha階段，僅適用於有限的客戶選擇。 功能和檔案可能會有所變更。</p>
&gt;<p>此目的地連線的最終版本可能需要客戶移轉。</p>


## 使用案例 {#use-cases}

以協助您更清楚了解應如何及何時使用 [!DNL LiveRamp SFTP] 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

身為行銷人員，我想將受眾從Adobe Experience Platform傳送至將身分識別上線至 [!DNL LiveRamp Connect] 以便鎖定 [!DNL CTV] 平台，使用 [!DNL Ramp ID] 識別碼。

## 先決條件 {#prerequisites}

此 [!DNL LiveRamp - SFTP] 連接導出檔案使用 [LiveRamp的SFTP](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) 儲存。

將資料從Experience Platform傳送至 [!DNL LiveRamp SFTP]，您需要 [!DNL LiveRamp] 憑證。 請聯繫您的 [!DNL LiveRamp] 代表取得您的認證（如果您尚未取得認證）。

## 支援的身分 {#supported-identities}

LiveRamp SFTP支援身分識別的啟用，例如以PII為基礎的識別碼、已知識別碼和自訂ID，如 [LiveRamp檔案](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

在 [對應步驟](#map) 在啟動工作流程中，您必須將目標對應定義為自訂屬性。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，其中包含 [!DNL LiveRamp SFTP] 目的地。 |
| 匯出頻率 | **[!UICONTROL 每日批]** | 隨著設定檔會根據區段評估在Experience Platform中更新，設定檔（身分）會每天更新一次，順流至目的地平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

### 驗證到目標 {#authenticate}

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

**使用密碼進行SFTP驗證** {#sftp-password}

![螢幕擷圖範例，說明如何使用密碼使用SFTP驗證至目的地](../../assets/catalog/advertising/liveramp/liveramp-sftp-password.png)

* **[!UICONTROL 使用者名稱]**:您的 [!DNL LiveRamp SFTP] 儲存位置。
* **[!UICONTROL 密碼]**:您 [!DNL LiveRamp SFTP] 儲存位置。
* **[!UICONTROL PGP/GPG加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 在下圖中查看格式正確的加密密鑰示例。 如果您提供加密金鑰，您還必須提供 **[!UICONTROL 加密子密鑰ID]** 在 [目的地詳細資訊](#destination-details) 區段。

   ![顯示UI中格式正確之PGP金鑰的範例影像](../../assets/catalog/advertising/liveramp/pgp-key.png)

**SSH金鑰驗證的SFTP** {#sftp-ssh}

![螢幕擷圖範例，說明如何使用SSH金鑰驗證目的地](../../assets/catalog/advertising/liveramp/liveramp-sftp-ssh.png)

* **[!UICONTROL 使用者名稱]**:您的 [!DNL LiveRamp SFTP] 儲存位置。
* **[!UICONTROL SSH金鑰]**:私人 [!DNL SSH] 用來登入的金鑰 [!DNL LiveRamp SFTP] 儲存位置。 私密金鑰的格式必須為 [!DNL Base64] — 編碼字串且不得受密碼保護。

   * 連接 [!DNL SSH] 鍵 [!DNL LiveRamp SFTP] 伺服器，您必須透過 [!DNL LiveRamp]的技術支援門戶，並提供您的公開密鑰。 如需詳細資訊，請參閱 [LiveRamp檔案](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL PGP/GPG加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 如果您提供加密金鑰，您還必須提供 **[!UICONTROL 加密子密鑰ID]** 在 [目的地詳細資訊](#destination-details) 區段。 在下圖中查看格式正確的加密密鑰示例。

   ![顯示UI中格式正確之PGP金鑰的範例影像](../../assets/catalog/advertising/liveramp/pgp-key.png)

### 填寫目的地詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="加密子機碼 ID"
>abstract="用於加密的子機碼 ID，是根據 LiveRamp 公開加密金鑰。如果您在驗證步驟中提供了加密金鑰，則需要此欄位。"
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="了解如何取得子機碼 ID"

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

![Platform UI螢幕擷取畫面，顯示如何填入目的地的詳細資訊](../../assets/catalog/advertising/liveramp/liveramp-connection-details.png)

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 資料夾路徑]**:路徑 [!DNL LiveRamp] `uploads` 用於承載導出檔案的子資料夾。 此 `uploads` 前置詞會自動新增至資料夾路徑。
   * 例如，如果您要將檔案匯出至 `uploads/my_export_folder`，請輸入 `my_export_folder` 在 **[!UICONTROL 資料夾路徑]** 欄位。
* **[!UICONTROL 壓縮格式]**:選擇Experience Platform應用於導出檔案的壓縮類型。 可用選項包括 **[!UICONTROL GZIP]** 或 **[!UICONTROL 無]**.
* **[!UICONTROL 加密子密鑰ID]**:用於加密的子密鑰，根據 [!DNL LiveRamp] 公用加密密鑰。 若您在 [驗證](#authenticate) 步驟。 請參閱 [!DNL LiveRamp] [加密檔案](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) 了解如何取得子索引鍵ID。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟用受眾資料以批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 排程 {#scheduling}

在 [!UICONTROL 排程] 步驟中，使用下列顯示的設定，為每個區段建立匯出排程。

>[!IMPORTANT]
>
>所有啟動至此目的地的區段都必須以完全相同的排程進行設定，如下所示。

* **[!UICONTROL 檔案導出選項]**: [!UICONTROL 導出完整檔案]. [增量檔案導出](../../ui/activate-batch-profile-destinations.md#export-incremental-files) 目前不支援 [!DNL LiveRamp] 目的地。
* **[!UICONTROL 頻率]**: [!UICONTROL 每日]
* 將匯出時間設為 **[!UICONTROL 區段評估後]**. 排程區段匯出和 [隨需檔案匯出](../../ui/export-file-now.md) 目前不支援 [!DNL LiveRamp] 目的地。
* **[!UICONTROL 日期]**:選擇所需的導出開始和結束時間。

![Platform UI螢幕擷取畫面，顯示區段排程步驟。](../../assets/catalog/advertising/liveramp/liveramp-segment-scheduling.png)

導出的檔案名當前不可由用戶配置。 所有匯出至 [!DNL LiveRamp SFTP] 目的地會根據下列範本自動命名：

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Platform UI螢幕擷圖，顯示匯出的檔案名稱範本。](../../assets/catalog/advertising/liveramp/liveramp-file-name.png)

例如，組織的匯出檔案名稱為 [!DNL Luma] 可能看起來類似於以下：

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### 對應屬性和身分 {#map}

在 **[!UICONTROL 對應]** 步驟中，您可以選取要針對設定檔匯出的屬性和身分。

>[!IMPORTANT]
>
>此目的地支援每個啟用流程激活一個源身份命名空間。 如果您需要匯出多個身分識別命名空間，例如 `Email` 和 `Phone`，您必須 [建立個別的啟動流程](../../ui/activate-batch-profile-destinations.md) 每個身分。

在 **[!UICONTROL 對應]** 步驟， **[!UICONTROL 目標欄位]** 「對應」會定義匯出之CSV檔案中欄標題的名稱。 您可以為匯出的檔案提供自訂名稱，將CSV欄標題變更為任何您想要的好記名稱 **[!UICONTROL 目標欄位]**.

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**. 畫面上會顯示新的對應列。

   ![Experience PlatformUI畫面，顯示「對應」畫面。](../../assets/catalog/advertising/liveramp/liveramp-add-new-mapping.png)

2. 在 **[!UICONTROL 選擇源欄位]** 窗口，選擇 **[!UICONTROL 選擇屬性]** 類別，並選取您要對應的XDM屬性，或選擇 **[!UICONTROL 選取身分命名空間]** 類別，並選取要對應至目的地的身分。

   ![Experience PlatformUI畫面，顯示來源對應畫面。](../../assets/catalog/advertising/liveramp/liveramp-source-mapping.png)

3. 在 **[!UICONTROL 選擇目標欄位]** 窗口，輸入要將選定源欄位映射到的屬性名。 此處定義的屬性名稱會以欄標題的形式反映在匯出的CSV檔案中。

   ![Experience PlatformUI畫面，顯示「目標對應」畫面。](../../assets/catalog/advertising/liveramp/liveramp-target-mapping.png)

   您也可以直接在 **[!UICONTROL 目標欄位]**.

   ![Experience PlatformUI畫面，顯示「目標對應」畫面。](../../assets/catalog/advertising/liveramp/liveramp-target-field.png)

新增所有所需對應後，請選取 **[!UICONTROL 下一個]** 並完成啟動工作流程。

## 匯出的資料/驗證資料匯出 {#exported-data}

您的資料會匯出至 [!DNL LiveRamp SFTP] 儲存位置（以CSV檔案形式）。

將檔案匯出至 [!DNL LiveRamp SFTP] 目的地，Platform會為每個目標產生一個CSV檔案 [合併策略ID](../../../profile/merge-policies/overview.md).

例如，讓我們考量下列區段：

* 段A（合併策略1）
* 段B（合併策略2）
* 段C（合併策略1）
* 段D（合併策略1）

Platform會將兩個CSV檔案匯出至 [!DNL LiveRamp SFTP]:

* 一個包含區段A、C和D的CSV檔案；
* 一個包含區段B的CSV檔案。

匯出的CSV檔案包含的設定檔具有選取的屬性和對應的區段狀態，位於個別的欄上，且屬性名稱和區段ID為欄標題。

匯出檔案中包含的設定檔可以符合下列其中一個區段資格狀態：

* `Active`:設定檔目前符合區段的資格。
* `Expired`:設定檔不再符合區段資格，但過去已符合資格。
* `""`（空字串）:設定檔從未符合區段的資格。


例如，匯出的CSV檔案，其中包含 `email` 屬性和3個區段可能如下所示：

```csv
email,aa2e3d98-974b-4f8b-9507-59f65b6442df,45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

因為Platform會為每個 [合併策略ID](../../../profile/merge-policies/overview.md)，它還會為每個合併策略ID生成一個單獨的資料流運行。

這表示 **[!UICONTROL 已激活身份]** 和 **[!UICONTROL 收到的設定檔]** 量度 [資料流運行](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 會針對使用相同合併原則的每一組區段匯總頁面，而非針對每個區段顯示。

由於為使用相同合併策略的一組段生成了資料流運行，因此在 [監視儀表板](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Experience PlatformUI畫面會顯示已啟用的身分量度。](../../assets/catalog/advertising/liveramp/liveramp-metrics.png)

## 將匯出的資料上傳至LiveRamp {#upload-to-liveramp}

將資料成功匯出至 [!DNL LiveRamp - SFTP] 儲存，您必須將資料上傳至 [!DNL LiveRamp] 平台。

如需如何從 [!DNL LiveRamp - SFTP] 儲存到 [!DNL LiveRamp] 對象，請參閱下列檔案： [上傳第一個檔案至對象時的考量事項](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

如需如何設定LiveRamp SFTP儲存的詳細資訊，請參閱 [官方檔案](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
