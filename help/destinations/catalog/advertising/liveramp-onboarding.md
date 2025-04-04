---
title: LiveRamp — 入門連線
description: 瞭解如何使用LiveRamp聯結器將對象從Adobe Real-Time Customer Data Platform上線到LiveRamp Connect。
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1948'
ht-degree: 3%

---

# [!DNL LiveRamp - Onboarding]個連線 {#liveramp-onboarding}

使用[!DNL LiveRamp - Onboarding]連線將對象從Adobe Real-Time Customer Data Platform上線到[!DNL LiveRamp Connect]。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL LiveRamp - Onboarding]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

身為行銷人員，我想要將對象從Adobe Experience Platform傳送至內建身分識別至[!DNL LiveRamp Connect]，以便我可以使用[!DNL Ramp ID]識別碼在行動、開啟Web、社交和[!DNL CTV]平台上鎖定使用者。

## 先決條件 {#prerequisites}

[!DNL LiveRamp - Onboarding]連線使用[LiveRamp的SFTP](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html)儲存空間匯出檔案。

在您可以從Experience Platform傳送資料給[!DNL LiveRamp - Onboarding]之前，您需要您的[!DNL LiveRamp]認證。 如果您尚未取得認證，請洽詢您的[!DNL LiveRamp]代表以取得認證。

## 支援的身分 {#supported-identities}

[!DNL LiveRamp - Onboarding]支援啟用PII型識別碼、已知識別碼和自訂ID等識別碼，如官方[LiveRamp檔案](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers)所述。

在啟動工作流程的[對應步驟](#map)中，您必須將目標對應定義為自訂屬性。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出具有[!DNL LiveRamp - Onboarding]目的地中所使用識別碼（名稱、電話號碼或其他）的對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 每日批次]** | 由於設定檔會根據對象評估在Experience Platform中更新，因此設定檔（身分）會每天更新一次，從下游傳送到目的地平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

**使用密碼的SFTP驗證** {#sftp-password}

![範例熒幕擷圖顯示如何使用包含密碼的SFTP驗證目的地](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-password.png)

* **[!UICONTROL 連線埠]**：您的[!DNL LiveRamp - Onboarding]儲存位置所使用的連線埠。  使用與您地理位置對應的連線埠，如下所述：
   * **[!UICONTROL NA]**：使用連線埠`22`
   * **[!UICONTROL AU]**：使用連線埠`2222`
* **[!UICONTROL 使用者名稱]**： [!DNL LiveRamp - Onboarding]儲存位置的使用者名稱。
* **[!UICONTROL 密碼]**： [!DNL LiveRamp - Onboarding]儲存位置的密碼。
* **[!UICONTROL PGP/GPG加密金鑰]**：您可以選擇附加RSA格式的公開金鑰，將加密新增至匯出的檔案。 在下圖中檢視格式正確的加密金鑰範例。
  ![影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL 子金鑰識別碼]**：如果您提供加密金鑰，您也必須提供加密&#x200B;**[!UICONTROL 子金鑰識別碼]**。 請參閱[!DNL LiveRamp] [加密檔案](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key)以瞭解如何取得子金鑰ID。

**使用SSH金鑰驗證的SFTP** {#sftp-ssh}

![顯示如何使用SSH金鑰驗證目的地的熒幕擷取畫面範例](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-ssh.png)

* **[!UICONTROL 連線埠]**：您的[!DNL LiveRamp - Onboarding]儲存位置所使用的連線埠。  使用與您地理位置對應的連線埠，如下所述：
   * **[!UICONTROL EU]**：使用連線埠`4222`
* **[!UICONTROL 使用者名稱]**： [!DNL LiveRamp - Onboarding]儲存位置的使用者名稱。
* **[!UICONTROL SSH金鑰]**：用來登入[!DNL LiveRamp - Onboarding]儲存位置的私人[!DNL SSH]金鑰。 私密金鑰必須格式化為[!DNL Base64]編碼的字串，且不得受密碼保護。

   * 若要將您的[!DNL SSH]金鑰連線至[!DNL LiveRamp - Onboarding]伺服器，您必須透過[!DNL LiveRamp]的技術支援入口網站提交票證，並提供您的公開金鑰。 請參閱[LiveRamp檔案](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client)中的詳細資訊。

* **[!UICONTROL PGP/GPG加密金鑰]**：您可以選擇附加RSA格式的公開金鑰，將加密新增至匯出的檔案。 在下圖中檢視格式正確的加密金鑰範例。
  ![影像顯示UI中格式正確的PGP金鑰範例](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL 子金鑰識別碼]**：如果您提供加密金鑰，您也必須提供加密&#x200B;**[!UICONTROL 子金鑰識別碼]**。 請參閱[!DNL LiveRamp] [加密檔案](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key)以瞭解如何取得子金鑰ID。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="加密子機碼 ID"
>abstract="用於加密的子機碼 ID，是根據 LiveRamp 公開加密金鑰。如果您在驗證步驟中提供了加密金鑰，則需要此欄位。"
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="了解如何取得子機碼 ID"

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![Experience Platform UI熒幕擷圖顯示如何填寫您目的地的詳細資料](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-destination-details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 地區]**：您LiveRamp SFTP儲存體執行個體的地理區域。
* **[!UICONTROL 資料夾路徑]**： [!DNL LiveRamp] `uploads`子資料夾的路徑，此子資料夾將裝載匯出的檔案。 `uploads`首碼會自動新增至資料夾路徑。 [!DNL LiveRamp]建議從Adobe Real-Time CDP建立傳遞的專用子資料夾，以將檔案與其他任何現有的摘要分開，並確保所有自動化運作順暢無礙。
   * 例如，如果您要將檔案匯出至`uploads/my_export_folder`，請在&#x200B;**[!UICONTROL 資料夾路徑]**&#x200B;欄位中輸入`my_export_folder`。
* **[!UICONTROL 壓縮格式]**：選取Experience Platform應該用於匯出檔案的壓縮型別。 可用的選項為&#x200B;**[!UICONTROL GZIP]**&#x200B;或&#x200B;**[!UICONTROL 無]**。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

讀取[啟用批次設定檔匯出目的地的對象資料](/help/destinations/ui/activate-batch-profile-destinations.md)，以取得啟用此目的地對象的指示。

### 正在安排 {#scheduling}

在[!UICONTROL 排程]步驟中，為每個對象建立一個匯出排程，其設定如下所示。

* **[!UICONTROL 檔案匯出選項]**： [!UICONTROL 匯出完整檔案]。 [目前不支援[!DNL LiveRamp]目的地的增量檔案匯出](../../ui/activate-batch-profile-destinations.md#export-incremental-files)。
* **[!UICONTROL 頻率]**： [!UICONTROL 每日]
* **[!UICONTROL 日期]**：視需要選取匯出開始和結束時間。

![Experience Platform UI熒幕擷圖顯示對象排程步驟。](../../assets/catalog/advertising/liveramp-onboarding/liveramp_scheduling_screenshot.png)

匯出的檔案名稱目前無法由使用者設定。 所有匯出至[!DNL LiveRamp - Onboarding]目的地的檔案都會根據下列範本自動命名：

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Experience Platform UI熒幕擷圖顯示匯出的檔案名稱範本。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-file-name.png)

例如，名為[!DNL Luma]之組織的匯出檔案名稱可能如下所示：

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### 對應屬性和身分 {#map}

在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，您可以選取要為設定檔匯出的屬性和身分。

>[!IMPORTANT]
>
>此目的地支援為每個啟用流程啟用一個來源身分名稱空間。 如果您需要匯出多個身分識別名稱空間（例如`Email`和`Phone`），您必須[為每個身分識別建立個別的啟用流程](../../ui/activate-batch-profile-destinations.md)。

在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，**[!UICONTROL 目標欄位]**&#x200B;對應會定義匯出CSV檔案中欄標題的名稱。 您可以為&#x200B;**[!UICONTROL 目標欄位]**&#x200B;提供自訂名稱，將匯出檔案中的CSV欄位標題變更為您想要的任何好記名稱。

>[!IMPORTANT]
>
>若在初始檔案傳遞至[!DNL LiveRamp]後對目標欄位所做的任何變更，請通知您的[!DNL LiveRamp]帳戶團隊或[將票證提交至LiveRamp支援](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#creating-a-support-case)，以確保變更反映在自動化程式中。

1. 在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，選取&#x200B;**[!UICONTROL 新增對應]**。 您會在畫面上看到新的對應列。

   ![Experience Platform UI熒幕顯示對應熒幕。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-add-new-mapping.png)

2. 在&#x200B;**[!UICONTROL 選取來源欄位]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL 選取屬性]**&#x200B;類別並選取您要對應的XDM屬性，或選擇&#x200B;**[!UICONTROL 選取身分名稱空間]**&#x200B;類別並選取要對應到目的地的身分。

   ![Experience Platform UI熒幕顯示來源對應熒幕。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-source-mapping.png)

3. 在&#x200B;**[!UICONTROL 選取目標欄位]**&#x200B;視窗中，輸入您要將選取的來源欄位對應到的屬性名稱。 此處定義的屬性名稱將在匯出的CSV檔案中反映為欄標題。

   ![Experience Platform UI熒幕顯示目標對應熒幕。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-mapping.png)

   您也可以直接在&#x200B;**[!UICONTROL 目標欄位]**&#x200B;中輸入屬性名稱，以輸入屬性名稱。

   ![Experience Platform UI熒幕顯示目標對應熒幕。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-field.png)

新增所有需要的對應之後，請選取&#x200B;**[!UICONTROL 下一步]**&#x200B;並完成啟動工作流程。

## 匯出的資料/驗證資料匯出 {#exported-data}

您的資料會匯出至您設定的[!DNL LiveRamp - Onboarding]儲存位置（CSV檔案）。

匯出的檔案大小上限為1,000萬列。 如果選取的對象超過1,000萬列，Experience Platform會每次傳送產生多個檔案。 如果您預計會超過單一檔案限制，請聯絡您的[!DNL LiveRamp]代表，讓他們為您設定批次擷取。

將檔案匯出至[!DNL LiveRamp - Onboarding]目的地時，Experience Platform會為每個[合併原則ID](../../../profile/merge-policies/overview.md)產生一個CSV檔案。

例如，我們考慮以下對象：

* 對象A （合併原則1）
* 對象B （合併原則2）
* 對象C （合併原則1）
* 對象D （合併原則1）

Experience Platform會將兩個CSV檔案匯出至[!DNL LiveRamp - Onboarding]：

* 一個CSV檔案，包含對象A、C和D；
* 一個CSV檔案包含對象B。

匯出的CSV檔案包含具有所選屬性的設定檔和對應的對象狀態，位於獨立的欄上，並具有屬性名稱，以及作為欄標題的`audience_namespace:audience_ID`對，如以下範例所示：

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1_AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2_AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X_AUDIENCE_ID_X`

匯出檔案中包含的設定檔可符合下列其中一個對象資格狀態：

* `Active`：設定檔目前符合對象的資格。
* `Expired`：設定檔不再符合對象的資格，但過去已符合資格。
* `""`（空字串）：設定檔從未符合對象的資格。

例如，具有一個`email`屬性、兩個源自Experience Platform [分段服務](../../../segmentation/home.md)的對象以及一個[匯入](../../../segmentation/ui/audience-portal.md#import-audience)外部對象的匯出CSV檔案可能如下所示：

```csv
email,ups_aa2e3d98-974b-4f8b-9507-59f65b6442df,ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

在上述範例中，`ups_aa2e3d98-974b-4f8b-9507-59f65b6442df`和`ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f`區段說明源自細分服務的對象，而`CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e`說明匯入Experience Platform作為[自訂上傳](../../../segmentation/ui/audience-portal.md#import-audience)的對象。

由於Experience Platform會為每個[合併原則ID](../../../profile/merge-policies/overview.md)產生一個CSV檔案，因此也會為每個合併原則ID產生個別的資料流執行。

這表示[資料流執行](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)頁面中收到的&#x200B;**[!UICONTROL 身分啟用]**&#x200B;和&#x200B;**[!UICONTROL 設定檔]**&#x200B;量度，會針對使用相同合併原則的每個對象群組進行彙總，而非針對每個對象顯示。

由於為使用相同合併原則的對象群組產生資料流執行，對象名稱不會顯示在[監視儀表板](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)中。

![Experience Platform UI熒幕顯示已啟用的身分識別量度。](../../assets/catalog/advertising/liveramp-onboarding/liveramp-metrics.png)

## 將匯出的資料上傳至LiveRamp {#upload-to-liveramp}

在資料成功匯出至[!DNL LiveRamp - Onboarding]儲存體後，您必須將資料上傳至[!DNL LiveRamp]平台。

如需有關如何將檔案從[!DNL LiveRamp - Onboarding]儲存空間上傳到[!DNL LiveRamp]對象的詳細資訊，請參閱下列檔案： [將第一個檔案上傳到對象時的考量事項](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience)。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

如需如何設定[!DNL LiveRamp - Onboarding]儲存空間的詳細資訊，請參閱[正式檔案](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html)。

## Changelog {#changelog}

本節擷取此目的地聯結器的功能和重要檔案更新。

+++ 檢視變更記錄檔

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2024 年 3 月 | 功能和檔案更新 | <ul><li>已新增對傳遞給歐洲和澳洲[!DNL LiveRamp]個[!DNL SFTP]執行個體的支援。</li><li>更新檔案，說明新支援地區的特定設定。</li><li>將檔案大小上限從500萬列增加到1,000萬列。</li><li>更新說明檔案，反映檔案大小增加。</li></ul> |
| 2023 年 7 月 | 首次發行 | 已發佈初始目的地版本和檔案。 |

{style="table-layout:auto"}

+++
