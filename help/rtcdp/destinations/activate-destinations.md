---
keywords: activate destination;activate destinations;activate data
title: 將描述檔和區段啟用至目標
seo-title: 將描述檔和區段啟用至目標
description: 將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。
seo-description: 將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。
translation-type: tm+mt
source-git-commit: 22bca041673cec5eee54ed4234aba19eca470441
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 0%

---


# 將描述檔和區段啟用至目標

將區段對應至目標，以啟用您在Adobe即時客戶資料平台中擁有的資料。 若要完成此作業，請遵循下列步驟。

## 先決條件 {#prerequisites}

要將資料激活到目標，必須已成功 [連接目標](/help/rtcdp/destinations/connect-destination.md)。 如果您尚未這麼做，請前往目標目錄 [](/help/rtcdp/destinations/destinations-catalog.md)，瀏覽支援的目標，並設定一或多個目標。

## 啟動資料 {#activate-data}

啟動工作流程中的步驟在目標類型之間略有不同。 以下列出所有目標類型的完整工作流程。

### 選擇要啟動資料的目標 {#select-destination}

適用於：所有目標

1. 在Adobe即時CDP使用者介面中，導覽至「 **[!UICONTROL 目標]** >瀏覽 ****」，並選取您要啟動區段的目標。
   ![瀏覽到目的地](assets/oracle-eloqua-connect.png)
2. 按一下目標的名稱。 這會帶您進入啟動工作流程。
   ![activate-flow](assets/activate-flow.png)請注意，如果目的地已有啟動工作流程，您可以看到目前已啟動至目的地的區段。 選取 **[!UICONTROL 右側邊欄]** 「編輯啟動」，然後依照下列步驟修改啟動詳細資訊。
3. 選擇「 **[!UICONTROL 啟動]**」。

<br> 

### **[!UICONTROL 選取區段]** 步驟 {#select-segments}

適用於：所有目標

![選取區段步驟](/help/rtcdp/destinations/assets/select-segments-icon.png)


在「啟 **[!UICONTROL 動目標]** 」工作流程的「選 **** 取區段」頁面上，選取一或多個區段以啟動至目標。 按下 **[!UICONTROL 一步]** ，繼續下一步。
![區段到目的地](assets/email-select-segments.png)

<br> 

### **[!UICONTROL 身份映射]** 步驟 {#identity-mapping}

適用於：社交目的地與Google客戶符合廣告目的地

![身份映射步驟](/help/rtcdp/destinations/assets/identity-mapping-icon.png)

對於 *社交目標*，在「身分對 **[!UICONTROL 應」步驟中]** ，您可以選取來源屬性，將其映射為目標身分。 此步驟為可選或必選步驟，具體取決於您在架構中使用的主要身份。 <br> 

*電子郵件地址作為主要身份*:如果您在架構中使用電子郵件地址作為主要身份，則可以跳過「身份映射」步驟，如下所示：

![身分識別的電子郵件地址](assets/email-as-identity.gif)

<br> 

*另一個ID作為主要身份*:如果您使用其他ID(例如 *Rewards ID* 或 *Loyalty ID*)作為架構中的主要身分識別，您必須手動將您身分識別架構中的電子郵件地址映射為社交目標中的目標身分，如下所示：

![忠誠度ID身分](assets/rewardsid-as-identity.gif)


如果 `Email_LC_SHA256` 您根據電子郵件雜湊要求，將客戶資料擷取的電子郵件地址雜湊到Adobe Experience Platform中，請選 [!DNL Facebook][為目標身分](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)。 <br> 如果 `Email` 您使用的電子郵件地址未雜湊，請選取為目標身分。 Adobe Real-time CDP會雜湊電子郵件地址以符合 [!DNL Facebook] 要求。

![填入欄位後的身分對應](assets/identity-mapping.png)

<br> 

### **[!UICONTROL 設定步驟]** {#configure}

適用於：電子郵件行銷目的地和雲端儲存空間目的地

![設定步驟](/help/rtcdp/destinations/assets/configure-icon.png)

此步驟為選填。在「設 **[!UICONTROL 定]** 」步驟中，您可以設定要匯出之每個區段的檔案名稱。 預設檔案名稱包含目標名稱、區段ID和日期和時間指標。 例如，您可以編輯匯出的檔案名稱，以區分不同的促銷活動，或將資料匯出時間附加至檔案。

選擇「 **[!UICONTROL 下一步]** 」(Next)以使用預設檔案名，或按一下鉛筆表徵圖以開啟模態窗口並編輯檔案名。 請注意，檔案名稱的限制為255個字元。

![配置檔案名](assets/activation-workflow-configure-step.png)

在檔案名編輯器中，可以選擇要添加到檔案名中的不同元件。 無法從檔案名稱中移除目標名稱和區段ID。 除了這些外，您還可以新增下列項目：

* **[!UICONTROL 區段名稱]**:您可以將區段名稱附加至檔案名稱。
* **[!UICONTROL 日期和時間]**:選擇添加格 `MMDDYYYY_HHMMSS` 式或生成檔案時的Unix 10位時間戳。 如果您希望檔案在每次增量匯出時產生動態檔案名稱，請選取其中一個選項。
* **[!UICONTROL 自訂文字]**:新增自訂文字至檔案名稱。

選擇 **[!UICONTROL 應用更改]** ，以確認選擇。

>[!IMPORTANT]
> 
>如果您未選擇「日期和時間 **** 」元件，則檔案名將是靜態的，而新導出的檔案將用每次導出覆蓋儲存位置中的先前檔案。 當從儲存位置將重複匯入工作執行至電子郵件行銷平台時，建議使用此選項。

![編輯檔案名選項](assets/activate-workflow-configure-step-2.png)

<br> 

### **[!UICONTROL 區段排程]** 步驟 {#segment-schedule}

適用於：廣告目的地，社交目的地

![區段排程步驟](/help/rtcdp/destinations/assets/segment-schedule-icon.png)

在「區 **[!UICONTROL 段排程]** 」頁面上，您可以設定傳送資料至目的地的開始日期，以及傳送資料至目的地的頻率。

>[!IMPORTANT]
>
>對於社交目的地，您必須在此步驟中選取對象的來源。 您只能在選取下圖中的其中一個選項後，才可繼續下一步。

![選擇資料來源](assets/choose-data-origin.png)

<br> 

### **[!UICONTROL 排程步驟]** (Scheduling Step) {#scheduling}

適用於：電子郵件行銷目的地和雲端儲存目的地

![區段排程步驟](assets/scheduling-icon.png)

在「 **[!UICONTROL 排程]** 」頁面上，您可以看到傳送資料至目的地的開始日期，以及傳送資料至目的地的頻率。 無法編輯這些值。

<br> 

### **[!UICONTROL 選擇屬性]** 步驟 {#select-attributes}

適用於：電子郵件行銷目的地和雲端儲存目的地

![選擇屬性步驟](/help/rtcdp/destinations/assets/select-attributes-icon.png)


在「選 **[!UICONTROL 擇屬性]** 」頁上，選擇「 **[!UICONTROL 添加新欄位]** 」，然後選擇要發送到目標的屬性。

>[!NOTE]
>
> Adobe Real-time CDP會從您的架構中，使用四個建議的常用屬性來預先填入您的選擇： `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`。

檔案匯出會依下列情況而有所不同，視是否 `segmentMembership.status` 已選取：
* 如果選 `segmentMembership.status` 擇了該欄位，則導出的檔案在初始完整快照中包括 **Active** members，在後續增量導出中包括 **Active** 和 **Expired** members。
* 如果未 `segmentMembership.status` 選擇該欄位，則導出的檔案在初始完整快照和後續增量導出中僅包括 **Active** members。

![建議的屬性](/help/rtcdp/destinations/assets/recommended-attributes.png)


我們建議其中一個屬性是來自您 [架構的唯一識](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 別碼。 如需必要屬性的詳細資訊，請參閱「電子郵件行銷目標」 [文章中的「身分](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 」。

>[!NOTE]
> 
>如果任何資料使用標籤已套用至資料集內的特定欄位（而非整個資料集），在啟動時會在下列情況下強制執行這些欄位層級標籤：
>* 欄位會用於區段定義中。
>* 欄位被配置為目標目標的預計屬性。

>
> 
請考慮以下螢幕擷取。 例如，如果欄位有某些與目標的行銷使用案例 `person.name.firstName` 相衝突的資料使用標籤，則您會在檢閱步驟（步驟9）中顯示資料使用政策違規。 有關詳細資訊，請 [參閱即時CDP中的資料治理](/help/rtcdp/privacy/data-governance-overview.md#destinations)。

![目標屬性](assets/select-attributes-step.png)

<br> 

### **[!UICONTROL 審核步驟]** (Review step) {#review}

適用於：所有目標

![審閱步驟](/help/rtcdp/destinations/assets/review-icon.png)

在「審 **[!UICONTROL 閱]** 」頁面上，您可以看到您所選項目的摘要。 選擇 **[!UICONTROL 取消]** ，以劃分流程，選擇 **[!UICONTROL 返回]** ，修改設定，或選擇完 **[!UICONTROL 成]** ，確認選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，即時CDP檢查資料使用策略違規。 以下是違反原則的範例。 除非您解決違規問題，否則無法完成區段啟動工作流程。 有關如何解決違反策略的資訊，請參 [閱資料治理文檔部分](/help/rtcdp/privacy/data-governance-overview.md#enforcement) 中的策略實施。

![資料策略違規](assets/data-policy-violation.png)

如果未檢測到任何違反策略的情況，請選擇「完 **[!UICONTROL 成]** 」以確認您的選擇並開始向目標發送資料。

![確認選擇](assets/confirm-selection.png)


## 編輯啟動 {#edit-activation}

請依照下列步驟，在即時CDP中編輯現有的啟動流程：

1. 在左 **[!UICONTROL 側導覽列中選取]** 「目標」，然後按一下「 **[!UICONTROL 瀏覽]** 」標籤，然後按一下目標名稱。
2. 選取 **[!UICONTROL 右側欄]** 「編輯啟動」，以變更要傳送至目的地的區段。

## 確認區段啟動成功 {#verify-activation}

### 電子郵件行銷目的地和雲端儲存空間目的地 {#esp-and-cloud-storage}

對於電子郵件行銷目標和雲端儲存目標，Adobe即時CDP會在您提供的儲存位置 `.csv` 中 `.txt` 建立以定位點分隔或檔案。 希望每天在您的儲存位置中建立一個新檔案。 The default file format is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

請注意，您可以編輯檔案格式。 如需詳細資訊，請前往雲端儲 [存目的地](/help/rtcdp/destinations/activate-destinations.md#configure) 、電子郵件行銷目的地的設定步驟。

使用預設檔案格式，您在連續三天收到的檔案可能如下所示：

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

這些檔案在您的儲存位置即表示確認是否成功啟動。 若要瞭解匯出檔案的結構，您可 [以下載範例。csv檔案](assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv)。 此範例檔案包含描述檔 `person.firstname`屬性 `person.lastname`、 `person.gender`、 `person.birthyear`和 `personalEmail.address`。

### 廣告目的地

在您要啟動資料的各個廣告目的地檢查您的帳戶。 如果啟動成功，您的廣告平台會填入受眾。

### 社交網路目的地

例 [!DNL Facebook]如，成功啟動表示將在 [!DNL Facebook] Facebook廣告管理員中以程式設計方式建立自訂對象 [](https://www.facebook.com/adsmanager/manage/)。 當使用者符合已啟用區段的資格或被取消資格時，會新增及移除觀眾中的區段成員資格。

>[!TIP]
>
>Adobe即時CDP與支援歷史觀眾回填的 [!DNL Facebook] 整合。 當您將區段啟動至目的地 [!DNL Facebook] 時，所有歷史區段資格都會傳送至。

## 停用啟動 {#disable-activation}

若要停用現有的啟動流程，請遵循下列步驟：

1. 在左 **[!UICONTROL 側導覽列中選取]** 「目標」，然後按一下「 **[!UICONTROL 瀏覽]** 」標籤，然後按一下目標名稱。
2. 按一下 **[!UICONTROL 右邊欄]** 中的「已啟用」控制項，以變更啟動流程狀態。
3. 在「更 **新資料流狀態** 」視窗中，選 **取「確認** 」以停用啟動流程。
